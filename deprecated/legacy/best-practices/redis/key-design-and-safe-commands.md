> **Location:** `best-practices/redis/key-design-and-safe-commands.md`

# Key Design & Production-Safe Commands

## 1. `KEYS` (and unscoped `SCAN` patterns) block the event loop under production load

**Principle:** Redis is single-threaded for command execution. `KEYS *` (or any broad pattern) walks the entire keyspace synchronously, blocking every other client's commands for the duration — on a large keyspace, this can be seconds of total unavailability.

### Bad
```go
keys, _ := redisClient.Keys(ctx, "session:*").Result() // blocks Redis for the full scan
```

### Good
```go
iter := redisClient.Scan(ctx, 0, "session:*", 100).Iterator()
for iter.Next(ctx) {
    key := iter.Val()
    // process incrementally
}
```
`SCAN` is cursor-based and non-blocking — it does bounded work per call and yields control back between iterations, at the cost of not guaranteeing a perfectly consistent snapshot if keys change during the scan (acceptable for most operational use cases like "find keys matching a pattern for cleanup").

**Checklist:**
- Never use `KEYS` in application code that runs against a production instance — restrict it to one-off manual debugging on a non-critical replica, if at all.
- Prefer designing key access patterns that don't need pattern-scanning in the first place (e.g. maintain an explicit index/set of relevant keys) over relying on `SCAN` as the primary access path for hot operations.

---

## 2. Missing TTLs turn Redis into an unbounded, unmanaged data store

**Principle:** A key written without an expiry lives forever unless explicitly deleted. Caches, session stores, and rate-limit counters written without a TTL accumulate indefinitely, eventually causing memory pressure and eviction of unrelated (possibly more important) keys once `maxmemory` is hit.

### Bad
```go
redisClient.Set(ctx, "session:"+sessionID, sessionData, 0) // no expiry
```

### Good
```go
redisClient.Set(ctx, "session:"+sessionID, sessionData, 24*time.Hour)
```

**Checklist:**
- Every key written by application code should have an explicit, deliberate TTL decision — even if the decision is "no TTL, because this is genuinely persistent state Redis is the source of truth for" (rare — usually a sign the data belongs in the primary DB instead).
- Check the instance's `maxmemory-policy` (e.g. `allkeys-lru`, `noeviction`) matches actual intent — `noeviction` with unbounded key growth causes writes to start failing outright once memory is full, rather than gracefully evicting old data.

---

## 3. Multi-key operations across a Redis Cluster need hash tags, or they simply fail

**Principle:** In Redis Cluster mode, keys are sharded across nodes by hash slot. A multi-key command (`MGET`, a transaction, a Lua script touching multiple keys) fails with a `CROSSSLOT` error if the keys involved hash to different slots — this is invisible in single-node development and only surfaces once deployed to cluster mode.

### Bad
```go
redisClient.MGet(ctx, "user:123:profile", "user:123:settings") // may hash to different slots
```

### Good
```go
// hash tag {user:123} forces both keys onto the same slot
redisClient.MGet(ctx, "{user:123}:profile", "{user:123}:settings")
```

**Checklist:**
- If the deployment target is (or might become) Redis Cluster, design multi-key access patterns with hash tags from the start — retrofitting key naming after cluster migration touches every caller.
- Test multi-key operations against a cluster-mode instance in staging, not just a single-node dev instance, since `CROSSSLOT` failures don't reproduce in non-cluster setups.