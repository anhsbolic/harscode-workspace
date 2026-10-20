> **Location:** `best-practices/kafka/producer-and-partitioning.md`

# Producer Configuration & Partitioning Strategy

## 1. Default producer settings favor throughput over durability

**Principle:** Kafka producer defaults (`acks=1`, no idempotence) are tuned for throughput, not guaranteed delivery. `acks=1` means "the partition leader accepted it" — if the leader crashes before replicating to followers, an acknowledged message can be lost.

### Bad
```go
producer, _ := sarama.NewSyncProducer(brokers, sarama.NewConfig()) // defaults: acks=1
```

### Good
```go
cfg := sarama.NewConfig()
cfg.Producer.RequiredAcks = sarama.WaitForAll // acks=all — wait for all in-sync replicas
cfg.Producer.Idempotent = true                 // prevents duplicate messages from producer retries
cfg.Net.MaxOpenRequests = 1                     // required for idempotent producer ordering guarantee
cfg.Producer.Retry.Max = 5
```

**Checklist:**
- For any topic where message loss is unacceptable (financial events, order state changes, audit trail), use `acks=all` with the topic's `min.insync.replicas` set to at least 2.
- Enable idempotent producer (`enable.idempotence=true` / `Producer.Idempotent`) to prevent the producer's own retries from creating duplicates on the broker side — this is a different concern from consumer-side idempotency (see `consumer-and-offset-management.md`) and both are usually needed together.

---

## 2. Partition key choice determines both ordering and load distribution — get it wrong in either direction

**Principle:** Kafka guarantees order only *within* a partition, not across partitions of a topic. The partition key determines which messages land together (and thus are ordered relative to each other) and how evenly load spreads across partitions.

**Why this is easy to get wrong both ways:**
- **No key (or random key):** messages round-robin across partitions — no ordering guarantee at all, even for messages that are logically related (e.g. two updates to the same order can be processed out of order by different consumers).
- **Low-cardinality key or a key with a "hot" value:** e.g. partitioning by `status` when 90% of messages are `status=pending` — most messages land on one partition, that partition's consumer becomes the bottleneck while others sit idle.

### Bad
```go
// no key — order-related events for the same order can be processed out of order
producer.SendMessage(&sarama.ProducerMessage{Topic: "order-events", Value: payload})
```

### Good
```go
// keyed by order ID — all events for one order go to the same partition, staying ordered
producer.SendMessage(&sarama.ProducerMessage{
    Topic: "order-events",
    Key:   sarama.StringEncoder(orderID),
    Value: payload,
})
```

**Checklist:**
- If any two messages have an ordering dependency (must be processed in the sequence they were produced), they must share a partition key that captures that relationship — usually the entity ID they both relate to.
- Check the key's cardinality and distribution against real production data, not assumptions — a key that seems diverse in a test environment can be highly skewed in production (e.g. one enterprise tenant producing 80% of traffic).