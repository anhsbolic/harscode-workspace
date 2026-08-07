> **Location:** `best-practices/postgresql/transactions-and-locking.md`

# Transactions & Locking

## 1. Long-running transactions block autovacuum and hold locks longer than intended

**Principle:** A transaction that does an external call (HTTP request, message publish, slow computation) *inside* a DB transaction holds row/table locks and prevents autovacuum from cleaning up dead tuples for the entire duration — not just the DB work.

**Why this happens:** wrapping "update DB, then notify downstream" in one transaction feels safer (atomicity), but a slow or hanging downstream call turns a millisecond-scale DB operation into a lock held for seconds or longer.

### Bad
```go
tx, _ := db.BeginTx(ctx, nil)
tx.Exec(ctx, "UPDATE orders SET status = $1 WHERE id = $2", "confirmed", orderID)
err := notifyClient.Publish(ctx, event) // network call, inside the transaction
if err != nil {
    tx.Rollback()
    return err
}
tx.Commit()
```
The row lock on `orders` is held for the entire network round-trip to the notification service.

### Good
```go
tx, _ := db.BeginTx(ctx, nil)
tx.Exec(ctx, "UPDATE orders SET status = $1 WHERE id = $2", "confirmed", orderID)
if err := tx.Commit(); err != nil {
    return err
}
// notify after commit — if this fails, handle via outbox/retry, not by rolling back a committed DB change
if err := notifyClient.Publish(ctx, event); err != nil {
    logger.Error(ctx, "notify failed, will retry via outbox", err)
}
```
For guaranteed delivery, use the transactional outbox pattern (write the event to an outbox table in the same transaction, publish it asynchronously afterward) rather than calling the external system inline.

**Checklist:**
- Never make a network call to an external system inside an open DB transaction.
- If "DB write + external notify" must be atomic in effect, use the outbox pattern, not a wider transaction.

---

## 2. Row-level locking (`SELECT ... FOR UPDATE`) without a consistent lock order causes deadlocks

**Principle:** When two transactions lock the same set of rows in different orders, Postgres detects the deadlock and kills one of them — but this shows up as a runtime error your application must handle, not a compile-time guarantee.

### Bad
```go
// Transaction A: locks order 1, then order 2
// Transaction B: locks order 2, then order 1
tx.Exec(ctx, "SELECT * FROM orders WHERE id = $1 FOR UPDATE", orderID1)
tx.Exec(ctx, "SELECT * FROM orders WHERE id = $1 FOR UPDATE", orderID2)
```
If two code paths lock the same rows in different orders, under concurrent load this deadlocks intermittently — hard to reproduce, easy to miss in review.

### Good
Always acquire locks in a consistent order (e.g., always by ascending primary key) across every code path that locks multiple rows:
```go
ids := []int{orderID1, orderID2}
sort.Ints(ids)
for _, id := range ids {
    tx.Exec(ctx, "SELECT * FROM orders WHERE id = $1 FOR UPDATE", id)
}
```

**Checklist:**
- Any code path that locks more than one row in the same table must lock in a fixed, deterministic order.
- Handle deadlock errors (`40P01`) with a bounded retry — don't treat them as unrecoverable.

---

## 3. Default transaction isolation (Read Committed) allows non-repeatable reads within one transaction

**Principle:** Postgres defaults to `READ COMMITTED`. Two `SELECT`s of the same row within the same transaction can return different results if another transaction commits a change in between — this is easy to forget when reasoning about "the transaction sees a consistent snapshot."

### Bad
```go
tx, _ := db.BeginTx(ctx, nil)
balance := getBalance(tx, accountID) // reads 100
// ... some other logic runs, another transaction commits a withdrawal ...
if balance >= 100 {
    debit(tx, accountID, 100) // still thinks balance is 100, now overdraws
}
```

### Good
Use `SELECT ... FOR UPDATE` to lock the row for the duration of the transaction when a read-then-write decision depends on a value staying consistent, or explicitly raise isolation to `REPEATABLE READ`/`SERIALIZABLE` for the transaction when the business logic requires a consistent snapshot across multiple statements — and handle the resulting serialization failure (`40001`) with a retry.

**Checklist:**
- If a transaction reads a value and later makes a decision based on that value still being true, either lock the row (`FOR UPDATE`) or use a stronger isolation level — don't rely on Read Committed's default behavior silently being "good enough."