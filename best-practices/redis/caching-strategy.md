> **Location:** `best-practices/redis/caching-strategy.md`

# Caching Strategy & Stampede Prevention

## 1. Cache-aside without stampede protection lets concurrent misses hammer the DB simultaneously

**Principle:** When a hot cache key expires, if many concurrent requests miss the cache at the same moment, every single one falls through to the database at once — a "thundering herd" that can spike DB load far beyond what steady-state traffic would produce, sometimes enough to cause the DB to fail and take down the very cache-refill path meant to fix it.

### Bad
```go
func getProduct(ctx context.Context, id string) (*Product, error) {
    if cached, err := redis.Get(ctx, "product:"+id); err == nil {
        return deserialize(cached), nil
    }
    product := db.QueryProduct(ctx, id) // every concurrent miss hits the DB independently
    redis.Set(ctx, "product:"+id, serialize(product), ttl)
    return product, nil
}
```

### Good
```go
func getProduct(ctx context.Context, id string) (*Product, error) {
    if cached, err := redis.Get(ctx, "product:"+id); err == nil {
        return deserialize(cached), nil
    }
    // singleflight ensures only one goroutine per key actually queries the DB;
    // concurrent callers for the same key wait for and share that one result
    v, err, _ := sf.Do("product:"+id, func() (interface{}, error) {
        product := db.QueryProduct(ctx, id)
        redis.Set(ctx, "product:"+id, serialize(product), ttl)
        return product, nil
    })
    return v.(*Product), err
}
```
`golang.org/x/sync/singleflight` (or an equivalent distributed lock for multi-instance deployments) collapses concurrent identical requests into one DB call.

**Checklist:**
- Any cache key with high read concurrency and a real chance of simultaneous expiry-driven misses needs stampede protection (in-process singleflight for single-instance load, or a distributed lock/lease for multi-instance).
- Consider adding jitter to TTLs for keys that are all set at the same time (e.g. a bulk cache warm) — synchronized TTLs mean synchronized simultaneous expiry, which recreates the stampede risk even with per-key protection.

---

## 2. Cache invalidation on write is easy to get inconsistent, especially across multiple related keys

**Principle:** When a write updates data that's cached under multiple keys (the entity itself, plus any list/aggregate caches that include it), missing even one invalidation leaves stale data being served indefinitely — with no error to signal it happened.

### Bad
```go
func updateProduct(ctx context.Context, p *Product) error {
    db.Update(ctx, p)
    redis.Del(ctx, "product:"+p.ID) // only the single-entity cache is invalidated
    // "products:category:" + p.CategoryID list cache still has the stale version
    return nil
}
```

### Good
Either explicitly invalidate every known dependent cache key at write time (requires tracking which caches depend on which entities — brittle as the system grows), or prefer short TTLs with the write-through/cache-aside pattern for aggregate/list caches specifically, accepting a bounded staleness window instead of relying on invalidation completeness.

**Checklist:**
- Before adding a new cache key derived from an entity, identify every write path that changes that entity and confirm invalidation is added at each one — not just the primary update path.
- For list/aggregate caches (harder to invalidate precisely), prefer a short TTL with acceptable staleness over trying to track exact invalidation dependencies — the operational cost of getting invalidation wrong (silently stale data) is usually worse than a bounded staleness window.