# rate-limiting.md

**Location:** `go/rate-limiting.md`

**Principle**
Per-key rate limiting (per-IP, per-user, per-endpoint) using a token bucket or sliding window must include cleanup for idle keys — a limiter map that grows without eviction is a memory leak that only becomes visible after enough traffic has accumulated. Apply a TTL or background sweep on the limiter map; never let it grow unbounded.

**Bad**
```go
var limiters = make(map[string]*rate.Limiter) // never cleaned up

func getLimiter(key string) *rate.Limiter {
    if l, ok := limiters[key]; ok { return l }
    l := rate.NewLimiter(1, 5)
    limiters[key] = l
    return l
}
```

**Good**
```go
type limiterEntry struct {
    limiter  *rate.Limiter
    lastUsed time.Time
}
var limiters sync.Map // key -> *limiterEntry

// background goroutine, run periodically
func sweepIdleLimiters(maxIdle time.Duration) {
    limiters.Range(func(k, v any) bool {
        entry := v.(*limiterEntry)
        if time.Since(entry.lastUsed) > maxIdle {
            limiters.Delete(k)
        }
        return true
    })
}
```

**Checklist**
- [ ] There is an eviction/TTL mechanism for idle limiter entries
- [ ] Limiter keys are granular to the need (per-IP for anonymous, per-user-ID for authenticated) — don't mix the two under the same key
- [ ] Limit and window are configurable, not hardcoded, so they can be tuned without a redeploy
- [ ] There is a test that verifies the limiter actually rejects the N+1th request