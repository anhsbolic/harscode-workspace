> **Location:** `best-practices/pubsub/retry-and-dead-letter.md`

# Retry Policy & Dead-Letter Handling

## 1. No dead-letter topic means a permanently-failing message retries forever, silently

**Principle:** Without a dead-letter policy, a message that always fails processing (malformed payload, a bug that panics on this specific input) gets redelivered indefinitely — consuming processing capacity and cluttering logs with the same failure, with no forcing function to notice or fix it.

### Bad
```go
sub, _ := client.CreateSubscription(ctx, "orders-sub", pubsub.SubscriptionConfig{
    Topic: topic,
    // no DeadLetterPolicy — a poison message retries forever
})
```

### Good
```go
sub, _ := client.CreateSubscription(ctx, "orders-sub", pubsub.SubscriptionConfig{
    Topic: topic,
    DeadLetterPolicy: &pubsub.DeadLetterPolicy{
        DeadLetterTopic:     dlqTopic.String(),
        MaxDeliveryAttempts: 5,
    },
    RetryPolicy: &pubsub.RetryPolicy{
        MinimumBackoff: 10 * time.Second,
        MaximumBackoff: 600 * time.Second,
    },
})
```
After 5 failed delivery attempts, the message moves to the DLQ topic instead of retrying forever — and the DLQ needs its own subscriber (alerting, manual review queue, or automated reprocessing after a fix ships).

**Checklist:**
- Every production subscription handling messages with real business consequences should have a dead-letter policy configured — "no DLQ" should be a deliberate choice for genuinely disposable messages, not an oversight.
- A DLQ with nothing consuming it is equivalent to silently dropping messages after N attempts — set up monitoring/alerting on DLQ topic depth, not just its existence.

---

## 2. Retrying immediately with no backoff amplifies outages instead of absorbing them

**Principle:** If a downstream dependency (DB, external API) is degraded and every failed message retries immediately, the retry traffic itself can prevent the dependency from recovering — the retry storm becomes the reason the outage continues.

### Bad
```go
if err := processMessage(ctx, msg); err != nil {
    msg.Nack() // default nack behavior with no backoff config retries almost immediately
}
```

### Good
Configure exponential backoff on the subscription's retry policy (`MinimumBackoff`/`MaximumBackoff` as shown above), and consider handler-level circuit breaking: if a downstream dependency is clearly down (several consecutive failures), stop calling it entirely for a cooldown period rather than retrying every message against a service that's already struggling.

**Checklist:**
- Configure `MinimumBackoff`/`MaximumBackoff` deliberately based on the failure modes expected — don't leave retry timing at defaults without checking whether they fit the downstream dependency's actual recovery characteristics.
- For a handler that calls a single external dependency, consider a circuit breaker so a known-down dependency doesn't get hammered by every in-flight message's retry.