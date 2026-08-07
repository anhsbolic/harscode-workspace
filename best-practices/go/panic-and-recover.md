> **Location:** `best-practices/go/panic-and-recover.md`

# Panic & Recover Discipline

## 1. A panic in a goroutine that isn't the main goroutine crashes the entire process

**Principle:** `recover()` only works within the same goroutine where the panic occurred. An HTTP framework's top-level recover middleware protects the request-handling goroutine it wraps — but a goroutine spawned inside a handler (`go func(){...}()`) is not covered by that middleware's recover. A panic in that spawned goroutine crashes the whole process, taking down every other in-flight request too.

### Bad
```go
func (h *Handler) HandleRequest(w http.ResponseWriter, r *http.Request) {
    go func() {
        processAsync(r.Context()) // if this panics, the entire process crashes —
    }()                            // the HTTP framework's recover middleware doesn't cover this goroutine
    w.WriteHeader(http.StatusAccepted)
}
```

### Good
```go
func (h *Handler) HandleRequest(w http.ResponseWriter, r *http.Request) {
    go func() {
        defer func() {
            if r := recover(); r != nil {
                logger.Error(context.Background(), "panic in async handler", zap.Any("recover", r), zap.Stack("stack"))
            }
        }()
        processAsync(r.Context())
    }()
    w.WriteHeader(http.StatusAccepted)
}
```

**Checklist:**
- Every goroutine spawned with `go func(){...}()` that isn't immediately joined (via `WaitGroup.Wait()`, channel receive, etc. in a way that would propagate a panic) needs its own `defer recover()` at the top of the goroutine body — the outer request's recover middleware does not protect it.
- Log the recovered value and stack trace, don't just swallow it silently — a panic indicates a real bug; recovering without logging hides it from ever being fixed.

---

## 2. `recover()` scattered across many layers hides bugs instead of fixing them

**Principle:** Recover is for preventing a single failure from crashing the whole process at a well-defined boundary (top of a goroutine, top of an HTTP handler) — not for suppressing panics throughout the codebase as a substitute for fixing the underlying bug. Recovering deep inside business logic, layer after layer, means panics get silently swallowed with no consistent place logging or alerting on them.

### Bad
```go
func (s *service) step1() {
    defer func() { recover() }() // silently swallows panics with no logging at all
    // ...
}

func (s *service) step2() {
    defer func() { recover() }() // same pattern, repeated in every function
    // ...
}
```
A panic anywhere in `step1`/`step2` just silently vanishes — the caller has no idea anything went wrong, and there's no log entry to even start debugging from.

### Good
Recover at a small number of well-known boundaries (top of each goroutine, framework middleware for HTTP handlers) with mandatory logging — not scattered through internal functions. If a specific operation is expected to sometimes fail in a recoverable way, that's what returning an `error` is for, not `panic`/`recover` used as control flow.

**Checklist:**
- `panic`/`recover` should exist at a small, deliberate set of boundary points in the codebase, not sprinkled through business logic — if you're writing `defer recover()` inside an ordinary internal function, ask whether this should be an error return instead.
- Any `recover()` that doesn't log what it recovered is actively harmful — it converts a debuggable crash into a silent, untraceable failure.