> **Location:** `best-practices/kafka/consumer-and-offset-management.md`

# Consumer Groups & Offset Management

## 1. Committing offsets before processing completes silently drops messages on crash

**Principle:** An offset commit tells Kafka "this consumer group has fully processed everything up to this offset." Committing before the message is actually processed (or with auto-commit on a short interval) means a crash between commit and completion permanently skips that message — no error, no retry, no trace of it happening.

### Bad
```go
for msg := range consumer.Messages() {
    consumer.MarkOffset(msg, "") // committed immediately on receipt
    processMessage(msg)          // if this panics or the process dies here, message is lost
}
```

### Good
```go
for msg := range consumer.Messages() {
    if err := processMessage(msg); err != nil {
        // handle via retry topic / DLQ — do not advance the offset past a failed message
        continue
    }
    consumer.MarkOffset(msg, "") // commit only after successful processing
}
```
This gives "at-least-once" delivery — process, then commit. Combined with idempotent message handling (see item 2), this is the standard safe default.

**Checklist:**
- Disable (or don't rely on) auto-commit for any consumer where message loss is unacceptable — commit explicitly, after processing.
- Decide and document per-topic whether "at-least-once with idempotent handling" or "exactly-once via transactional processing" is required — don't leave it implicit.

---

## 2. At-least-once delivery means your handler must be idempotent, not just "usually fine"

**Principle:** Kafka's at-least-once guarantee (the safe default from item 1) means a message *will* be redelivered — after a rebalance, a crash-and-restart, or a retry. A handler with a non-idempotent side effect (charge a card, send an email, increment a counter) will duplicate that effect on redelivery.

### Bad
```go
func processPayment(msg Message) error {
    return paymentClient.Charge(msg.AccountID, msg.Amount) // charges again on redelivery
}
```

### Good
```go
func processPayment(msg Message) error {
    return paymentClient.ChargeIdempotent(msg.AccountID, msg.Amount, msg.IdempotencyKey)
    // msg.IdempotencyKey derived from a stable message identifier (e.g. Kafka partition+offset,
    // or a business-level transaction ID), so redelivery is a safe no-op on the receiving system
}
```

**Checklist:**
- Any consumer handler with an external side effect needs an idempotency key derived from something stable in the message (not generated fresh per processing attempt).
- Don't assume "rebalances are rare, so duplicate processing is rare too" — rebalances happen on every deploy, every consumer scale event, and every transient network blip.

---

## 3. Consumer group rebalances pause the whole group, not just the joining/leaving member

**Principle:** During a rebalance (a consumer joins, leaves, or is considered dead by the group coordinator), partition assignment is recalculated and — depending on the rebalance strategy — the entire group may stop processing until the new assignment is settled.

**Checklist:**
- Slow message processing (long-running handler) increases the chance the consumer misses its `session.timeout.ms` heartbeat, gets marked dead, and triggers a rebalance — keep per-message processing time well under the session timeout, or offload slow work to an async path and ack the Kafka message once the work is durably queued.
- Consider cooperative rebalancing strategies (`CooperativeStickyAssignor` or equivalent) over eager rebalancing for consumer groups with many partitions, to reduce full-group pause duration.