# financial-invariant-enforcement.md

**Location:** `postgresql/financial-invariant-enforcement.md`

**Principle**
Balance updates that can be hit concurrently (two requests reducing the same balance simultaneously) are vulnerable to double-spend if protected only at the application layer. Use `SELECT ... FOR UPDATE` for explicit row locking, or a constraint-level check (a `CHECK` constraint that rejects a negative balance) as defense-in-depth. Important invariants (e.g. "total in must equal total out" within a unit of transaction) should be verified at the database transaction level, not recomputed after the fact in application logic.

**Bad**
```go
// read-then-write with no locking — race condition between two concurrent requests
balance := getBalance(accountID)
if balance >= amount {
    updateBalance(accountID, balance-amount) // two goroutines can both pass this same check
}
```

**Good**
```sql
BEGIN;
SELECT balance FROM accounts WHERE id = $1 FOR UPDATE; -- explicit row lock
UPDATE accounts SET balance = balance - $2 WHERE id = $1 AND balance >= $2;
-- check rows affected; if 0, insufficient balance
COMMIT;
```
```sql
ALTER TABLE accounts ADD CONSTRAINT balance_non_negative CHECK (balance >= 0); -- defense-in-depth
```

**Checklist**
- [ ] Balance updates that can occur concurrently use row locking (`FOR UPDATE`) or a conditional update with a rows-affected check
- [ ] There is a DB-level constraint that prevents an invalid state (e.g. negative balance) as a second layer, not relying on application logic alone
- [ ] Cross-entity invariants (total in = total out) are verified within a single database transaction, not computed separately after commit
- [ ] There is a dedicated test for concurrent duplicate requests against the same financial resource (see `go/testing-concurrency.md`)