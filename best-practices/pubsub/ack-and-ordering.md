> **Location:** `best-practices/pubsub/ack-and-ordering.md`

# Ack/Nack Semantics & Message Ordering

## 1. Acking before processing completes has the same failure mode as Kafka's early-commit problem

**Principle:** Pub/Sub redelivers a message if it isn't acked within the ack deadline. Acking immediately on receipt (before the handler actually finishes) means a crash mid-processing loses the message permanently — the same class of bug as committing a Kafka offset too early.

### Bad
```go
sub.Receive(ctx, func(ctx context.Context, msg *pubsub.Message) {
    msg.Ack() // acked before processing
    processMessage(msg)
})
```

### Good
```go
sub.Receive(ctx, func(ctx context.Context, msg *pubsub.Message) {
    if err := processMessage(ctx, msg); err != nil {
        msg.Nack() // triggers redelivery per the subscription's retry policy
        return
    }
    msg.Ack()
})
```

**Checklist:**
- Ack only after the handler has durably completed its work (written to DB, published downstream, etc.) — not on receipt.
- Nack explicitly on failure rather than letting the ack deadline silently expire — an explicit nack can trigger faster redelivery depending on the subscription's retry policy, instead of waiting out the full deadline.

---

## 2. Ack deadline too short for the handler causes duplicate processing even on the happy path

**Principle:** If message processing routinely takes longer than the subscription's ack deadline, Pub/Sub redelivers the message *while the original handler is still running* — not because anything failed, but because the deadline expired first. This produces duplicate processing under entirely normal conditions, not just crash scenarios.

**Checklist:**
- Set the ack deadline with margin above p99 processing time, not median — a deadline tuned to the average case triggers redeliveries during normal load spikes.
- For handlers with genuinely variable/long processing time, extend the deadline programmatically (`msg.ExtendAckDeadline` or client-library equivalent) rather than setting a single static deadline high enough to cover the worst case for every message.
- Because redelivery-during-normal-processing is possible even with a well-tuned deadline, handlers must be idempotent regardless — this isn't optional hardening, it's required for correctness under Pub/Sub's delivery model.

---

## 3. Pub/Sub standard subscriptions don't guarantee ordering — ordering keys must be explicit and consistent

**Principle:** Without an ordering key, Pub/Sub makes no ordering guarantee between messages, even ones published in sequence by the same publisher. Ordering keys enable per-key ordering, but only within the constraints of how they're used.

### Bad
```go
// two updates to the same entity, published without an ordering key,
// can be delivered to different subscribers out of sequence
topic.Publish(ctx, &pubsub.Message{Data: updatePayload})
```

### Good
```go
topic.Publish(ctx, &pubsub.Message{
    Data:        updatePayload,
    OrderingKey: entityID, // all messages for this entity are delivered in publish order
})
```

**Checklist:**
- Enable message ordering on the subscription explicitly — it's off by default even if publishers set ordering keys.
- A publish failure on an ordering key pauses that key's ordering guarantee until resumed (`ResumePublish`) — handle publish errors explicitly rather than assuming ordered publishing degrades gracefully on its own.
- Ordering keys have the same "hot key" risk as Kafka partition keys (see `kafka/producer-and-partitioning.md`) — a low-cardinality or skewed key concentrates load and throughput on one ordered stream.