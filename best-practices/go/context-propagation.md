> **Location:** `best-practices/go/context-propagation.md`

# Context Propagation Discipline

## 1. `context.Background()`/`context.TODO()` mid-chain silently breaks cancellation and deadline propagation

**Principle:** When a function already receives a `ctx` from its caller, creating a fresh `context.Background()` partway through — instead of deriving from the received `ctx` — severs the chain. Cancellation, deadlines, and request-scoped values (trace IDs, auth info) from the original caller no longer reach anything downstream of that point.

**Why this happens:** it's usually not deliberate — a function is refactored, a new call is added inside it, and `ctx` isn't threaded through because the immediate code compiles fine with a fresh background context. The bug is invisible until someone relies on cancellation actually working.

### Bad
```go
func (s *service) ProcessOrder(ctx context.Context, order Order) error {
    // ctx respected here
    if err := s.validate(ctx, order); err != nil {
        return err
    }
    // new background context — if the original request is cancelled, this keeps running anyway
    return s.notifyClient.Send(context.Background(), buildNotification(order))
}
```
If the original HTTP request is cancelled (client disconnected) or times out, `validate` respects that — but `notifyClient.Send` doesn't, because it's not using the same context chain.

### Good
```go
func (s *service) ProcessOrder(ctx context.Context, order Order) error {
    if err := s.validate(ctx, order); err != nil {
        return err
    }
    return s.notifyClient.Send(ctx, buildNotification(order))
}
```

**Checklist:**
- If a function receives `ctx` as a parameter, every downstream call it makes that accepts a context should receive that same `ctx` (or one derived from it via `context.WithTimeout`/`WithCancel`/`WithValue`) — never a fresh `Background()`/`TODO()`.
- `context.Background()` belongs at genuine root points only: `main()`, the entry point of a background worker with no upstream request, or test setup. If you're writing `context.Background()` inside a function that already has a `ctx` parameter, that's a signal something's wrong.

---

## 2. Storing `ctx` in a struct field defeats its per-call scoping and risks using a stale/cancelled context

**Principle:** `context.Context` is designed to flow through call chains as an explicit parameter, scoped to one request/operation. Storing it on a struct makes it live as long as the struct does — outliving the request it came from — and makes it easy for a later method call to unknowingly use a context that was already cancelled by a previous operation.

### Bad
```go
type worker struct {
    ctx context.Context // stored at construction time
}

func (w *worker) DoWork() error {
    return w.repo.Query(w.ctx, ...) // whose request's ctx is this, by the time DoWork runs?
}
```

### Good
```go
type worker struct {
    repo Repository
}

func (w *worker) DoWork(ctx context.Context) error {
    return w.repo.Query(ctx, ...)
}
```

**Checklist:**
- `ctx` should be the first parameter of any method that needs it, not a field set once at construction — this is explicit in Go's own standard library conventions (`context.Context` as first param, named `ctx`).
- If a long-lived object (a background worker, a connection pool) genuinely needs a "lifetime" context distinct from any single call's context, name that field something other than `ctx` (e.g. `shutdownCtx`) to make clear it's not meant to represent "the current operation."

---

## 3. Long-running work must poll `ctx.Done()`, not just accept `ctx` as a formality

**Principle:** Accepting a `ctx` parameter doesn't automatically make a function cancellable — if the function's body is a tight loop or a blocking call that never checks `ctx.Done()`, cancellation has no effect until the function's own blocking operation happens to return on its own.

### Bad
```go
func processLargeDataset(ctx context.Context, rows []Row) error {
    for _, row := range rows { // ctx accepted but never checked — runs to completion regardless
        transform(row)
    }
    return nil
}
```

### Good
```go
func processLargeDataset(ctx context.Context, rows []Row) error {
    for _, row := range rows {
        select {
        case <-ctx.Done():
            return ctx.Err()
        default:
        }
        transform(row)
    }
    return nil
}
```

**Checklist:**
- Any loop or long-running operation that accepts `ctx` should periodically check `ctx.Done()` (or use a context-aware blocking call, like a DB query using `QueryContext`) — accepting `ctx` as a parameter without ever reading `Done()` gives the appearance of cancellability without the substance.