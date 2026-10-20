> **Location:** `best-practices/go/defer-pitfalls.md`

# Defer Pitfalls

## 1. `defer` inside a loop accumulates until the enclosing function returns, not per-iteration

**Principle:** `defer` schedules a call to run when the *enclosing function* returns — not when the current loop iteration ends. A `defer` inside a loop that runs many iterations accumulates all those deferred calls, holding their resources open until the whole function exits.

### Bad
```go
func processFiles(paths []string) error {
    for _, path := range paths {
        f, err := os.Open(path)
        if err != nil {
            return err
        }
        defer f.Close() // doesn't close until processFiles returns, not after each file
        if err := process(f); err != nil {
            return err
        }
    }
    return nil
}
```
With thousands of files, this holds thousands of file descriptors open simultaneously until the function finally returns — potentially hitting the OS's open-file-descriptor limit.

### Good
```go
func processFiles(paths []string) error {
    for _, path := range paths {
        if err := processOneFile(path); err != nil {
            return err
        }
    }
    return nil
}

func processOneFile(path string) error {
    f, err := os.Open(path)
    if err != nil {
        return err
    }
    defer f.Close() // now scoped to this function, closes after each file
    return process(f)
}
```
Extracting the per-iteration body into its own function gives `defer` a tight scope. Alternatively, close explicitly without `defer` if extracting a function isn't practical.

**Checklist:**
- If a `defer` is written inside a loop, ask whether the loop can run many iterations in practice — if so, extract the loop body into its own function so the defer's scope matches "one iteration," not "the whole loop."

---

## 2. Deferred function arguments are evaluated immediately, not at defer-execution time

**Principle:** In `defer f(x)`, the arguments to `f` are evaluated the moment the `defer` statement runs — not when `f` actually executes at function return. If `x` changes after the `defer` line, `f` still sees the value `x` had at the time of the `defer` statement.

### Bad
```go
func doWork() (err error) {
    start := time.Now()
    defer logDuration(start, err) // err is captured as its zero value here, always "nil" in the log
    err = riskyOperation()
    return err
}
```
`err` is captured by value at the `defer` line, before `riskyOperation()` even runs — so `logDuration` always logs `nil`, regardless of what `riskyOperation()` actually returns.

### Good
```go
func doWork() (err error) {
    start := time.Now()
    defer func() {
        logDuration(start, err) // closure reads err at execution time, after the named return is set
    }()
    err = riskyOperation()
    return err
}
```
Wrapping in a closure defers the *read* of `err` to execution time, not just the call. This requires `err` to be a named return value so the closure and the `return` statement refer to the same variable.

**Checklist:**
- If a deferred call needs to observe a value that changes later in the function (especially an error being returned), wrap it in a closure (`defer func() { ... }()`) rather than passing the value directly as an argument to the deferred call.
- Pair this pattern with a named return value when the deferred closure needs to see (or modify) the function's actual return error.

---

## 3. Deferred cleanup order is LIFO — matters when multiple resources depend on each other

**Principle:** Multiple `defer` statements in one function execute in last-in-first-out order. This is usually what you want (close in reverse order of acquisition — mirrors typical resource dependency direction), but it's worth being deliberate about when resources have a specific teardown order requirement.

### Good (illustrating correct LIFO reliance)
```go
tx, _ := db.BeginTx(ctx, nil)
defer tx.Rollback() // runs last if Commit wasn't called — safe no-op after a successful Commit

lock, _ := acquireLock(ctx, key)
defer lock.Release() // runs first, before the rollback defer above

// ... work using both tx and lock ...
```
`lock.Release()` runs before `tx.Rollback()` because it was deferred second (LIFO) — releasing the lock before the transaction's rollback/commit state is finalized is often the correct order when the lock's purpose was only to serialize access, not to guard the transaction itself.

**Checklist:**
- When a function defers cleanup for multiple resources with a dependency between them, verify LIFO order actually produces the correct teardown sequence — don't assume it's automatically right just because it's idiomatic.
- `defer tx.Rollback()` immediately after `BeginTx` is a common, safe idiom — `Rollback` on an already-committed transaction is a documented no-op in `database/sql`, so this pattern doesn't need an `if !committed` guard.