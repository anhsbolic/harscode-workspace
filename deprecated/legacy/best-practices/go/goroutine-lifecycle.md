> **Location:** `best-practices/go/goroutine-lifecycle.md`

# Goroutine Lifecycle & Leaks

## 1. A goroutine with no exit path outlives the request/operation that spawned it

**Principle:** `go func(){...}()` starts a goroutine with an independent lifecycle from its caller. If that goroutine blocks on something (a channel send/receive, a long-running call) with no way to be told "the caller is gone, stop," it leaks — it stays alive, holding memory and any resources it references, for as long as the process runs.

**Why this happens:** the goroutine is written to solve "do this work concurrently," and the question "what happens to this goroutine if the caller times out or the request is cancelled" isn't part of the immediate problem being solved, so it's easy to skip.

### Bad
```go
func fetchWithFallback(ctx context.Context, primary, fallback func() (Result, error)) (Result, error) {
    ch := make(chan Result, 1)
    go func() {
        r, _ := primary() // if this blocks forever, this goroutine never exits
        ch <- r
    }()
    select {
    case r := <-ch:
        return r, nil
    case <-time.After(2 * time.Second):
        return fallback()
    }
}
```
If `primary()` never returns, the spawned goroutine leaks permanently — the `select` moves on via the timeout, but nothing ever tells the goroutine to stop, and `ch <- r` blocks forever on an unbuffered-in-spirit channel no one is reading from anymore (technically buffered here with size 1, so it doesn't block, but the goroutine and everything `primary()` holds onto is still never released if `primary` itself hangs).

### Good
```go
func fetchWithFallback(ctx context.Context, primary func(context.Context) (Result, error), fallback func() (Result, error)) (Result, error) {
    ctx, cancel := context.WithTimeout(ctx, 2*time.Second)
    defer cancel()
    r, err := primary(ctx) // primary must itself respect ctx cancellation
    if err != nil {
        return fallback()
    }
    return r, nil
}
```
Pushing `ctx` into `primary` itself (rather than racing it against a timeout from the outside) means `primary` can actually stop its own work when cancelled — the goroutine underlying it (if any) exits instead of leaking.

**Checklist:**
- Before writing `go func(){...}()`, identify how this goroutine ends: does it complete on its own in bounded time, or does it need a `ctx`/`done` channel to know when to stop?
- Racing a goroutine against a `select`/timeout from the *outside* doesn't stop the goroutine — it only stops the caller from waiting on it. The goroutine itself needs to observe the same cancellation signal to actually exit.

---

## 2. Unbounded goroutine spawning under load causes memory/scheduler pressure, not graceful degradation

**Principle:** Spawning one goroutine per incoming item (per request, per message, per row) with no concurrency limit means load spikes translate directly into goroutine count spikes — thousands of goroutines each holding their own stack and captured state, competing for the scheduler and memory.

### Bad
```go
for _, item := range items { // items could be 10 or 10 million
    go process(item)
}
```

### Good
```go
sem := make(chan struct{}, 20) // bounded concurrency
var wg sync.WaitGroup
for _, item := range items {
    wg.Add(1)
    sem <- struct{}{}
    go func(item Item) {
        defer wg.Done()
        defer func() { <-sem }()
        process(item)
    }(item)
}
wg.Wait()
```
Or use `golang.org/x/sync/errgroup` with `SetLimit` for the same effect with cleaner error propagation.

**Checklist:**
- Any loop that spawns a goroutine per element needs an explicit concurrency bound unless the element count is provably small and fixed.
- Use `errgroup.Group` (with `SetLimit` where bounding is needed) over raw `sync.WaitGroup` when goroutines can return errors — it gives you first-error propagation and context cancellation for free.