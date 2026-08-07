> **Location:** `best-practices/go/struct-copying-and-time.md`

# Struct Copying Pitfalls & Time Comparison

## 1. Copying a struct containing `sync.Mutex` creates two independent, broken locks

**Principle:** `sync.Mutex` (and `sync.RWMutex`) must not be copied after first use. A struct value containing a mutex, when copied (by value assignment, passing by value to a function, or returning by value), duplicates the mutex's internal state — the copy and the original are now separate locks guarding what looks like the same logical state, so locking one no longer excludes the other.

### Bad
```go
type Counter struct {
    mu    sync.Mutex
    value int
}

func (c Counter) Increment() { // value receiver — copies the whole struct, including mu
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++ // mutates the copy, not the original — this method doesn't even work as intended
}
```
This has two bugs at once: the mutex is copied (breaking the locking guarantee for any concurrent caller), and the value receiver means `c.value++` doesn't even affect the original struct.

### Good
```go
type Counter struct {
    mu    sync.Mutex
    value int
}

func (c *Counter) Increment() { // pointer receiver — no copy
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}
```

**Checklist:**
- Any struct containing a `sync.Mutex`/`sync.RWMutex` (directly or via an embedded type) must always be used via pointer — pointer receivers on all methods, passed by pointer, never returned or assigned by value.
- Run `go vet` as part of CI, not just locally — it flags `sync.Mutex` copying (via the `copylocks` check) and this is exactly the kind of issue that's easy to introduce in a quick refactor and easy for `go vet` to catch automatically.
- Watch for this specifically when a struct with a mutex is put into a slice or map by value (`items = append(items, myStructWithMutex)`) — this copies just as much as a direct assignment does.

---

## 2. `time.Time` equality with `==` breaks on monotonic clock differences; always use `.Equal()`

**Principle:** `time.Time` values returned by `time.Now()` carry a monotonic clock reading alongside the wall clock time, used for accurate duration measurement. Two `time.Time` values representing "the same instant" can still fail a `==` comparison if their monotonic readings differ (e.g., one came from `time.Now()`, the other was deserialized from a DB or JSON, which strips the monotonic component).

### Bad
```go
if scheduledTime == time.Now() { // virtually never true even at "the same" instant, and comparing
                                   // exact equality against Now() is rarely meaningful anyway
```
```go
var t1, t2 time.Time
t1 = someFunc() // has monotonic reading
t2, _ = time.Parse(time.RFC3339, t1.Format(time.RFC3339)) // round-tripped, monotonic reading stripped
fmt.Println(t1 == t2) // false, even though they represent the same wall-clock instant
```

### Good
```go
if t1.Equal(t2) { // compares the actual time instant, ignoring monotonic reading differences
```
For ordering, use `.Before()`/`.After()`, not manual comparison of underlying representations.

**Checklist:**
- Always use `.Equal()`, `.Before()`, `.After()` for `time.Time` comparisons — never `==`, `<`, `>`.
- When storing/transmitting `time.Time` (DB, JSON, gRPC), be deliberate and consistent about timezone: store and compare in UTC, convert to local time only at the presentation boundary. Mixing UTC-stored and locally-constructed `time.Time` values is a common source of off-by-hours bugs that only show up for users in certain timezones.