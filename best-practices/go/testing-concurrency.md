# testing-concurrency.md

**Location:** `go/testing-concurrency.md`

**Principle**
Code that genuinely touches shared state must be tested with `go test -race`, and this stays mandatory once a feature is done — but scope *where* that gate fires deliberately. The fast build/patch iteration loop (edit → run → fix) should default to unit + mocked-service + API-contract tests only; race-detector runs belong in the testing phase's final sweep or a dedicated CI job, scoped to the specific package(s) that actually have shared-state code — never as a blanket `go test -race ./...` fired on every build-loop iteration. Not every feature needs a race test either: reserve it for areas genuinely identified as concurrency-sensitive (shared mutable state, goroutines operating on the same resource), not as a default for every package.

Use a table-driven pattern for the race scenarios that do warrant it: spawn N goroutines in parallel performing the same operation against the same state, then assert an invariant at the end — not just "it didn't crash," but an invariant that genuinely reflects correctness (e.g. the final total must equal the expected sum).

**A common cause of multi-hour build stalls:** running `-race` inside the tight iteration loop, especially on code that also calls a deliberately-slow primitive (password hashing, KDFs — see `expensive-primitives-in-tests.md`). Race-detector instrumentation overhead multiplies across every parallel goroutine in the test; combined with production-cost bcrypt/argon2/scrypt calls, this compounds into hours, not minutes. That's a test-environment configuration problem (wrong gate, wrong cost factor), not a reason to weaken or skip race testing itself — fix the scoping and the cost factor, don't drop the test.

**Bad**
```go
func TestConcurrentUpdate(t *testing.T) {
    for i := 0; i < 10; i++ {
        go update(shared)
    }
    time.Sleep(time.Second) // no race detector, no invariant assertion
}
```

**Also bad — right test, wrong place/cost**
```go
// This test is correct in isolation, but running it with `-race` inside
// every build-loop iteration, against a bcrypt cost factor meant for
// production, is what turns a 2-second test into a multi-hour stall.
func TestConcurrentLoginAttempts(t *testing.T) {
    // run with: go test -race ./internal/auth/...  (testing-phase gate only)
    hash, _ := bcrypt.GenerateFromPassword(pw, bcrypt.DefaultCost) // DefaultCost == 10, production setting
    var wg sync.WaitGroup
    for i := 0; i < 50; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            _ = bcrypt.CompareHashAndPassword(hash, pw)
        }()
    }
    wg.Wait()
}
```

**Good**
```go
func TestConcurrentBalanceUpdate(t *testing.T) {
    // run with: go test -race ./internal/ledger/...
    // scoped to this package, run in the testing-phase gate — not on
    // every build-loop iteration.
    var wg sync.WaitGroup
    account := newAccount(0)
    for i := 0; i < 100; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            account.Add(1) // same operation, in parallel
        }()
    }
    wg.Wait()
    assert.Equal(t, int64(100), account.Balance()) // invariant, not just "didn't panic"
}
```

**Checklist**
- [ ] `go test -race` is scoped per-package to areas with genuine shared-state/concurrency risk — not a blanket `./...` sweep, and not applied to packages that aren't concurrency-sensitive at all
- [ ] `-race` runs as part of the testing phase's final sweep or a dedicated CI job — not inside the fast build/patch iteration loop
- [ ] Tests for shared-state code assert a clear invariant, not just "didn't crash"
- [ ] The number of parallel goroutines in the test is enough to realistically trigger a race (not just 2-3)
- [ ] Code protected by a mutex/atomic has a test that actually exercises that protection, not just the sequential happy path
- [ ] Any deliberately-slow primitive exercised inside a concurrent test (bcrypt, argon2, scrypt, other KDFs) uses a test-appropriate minimal cost/work factor, never the production setting — see `expensive-primitives-in-tests.md`
