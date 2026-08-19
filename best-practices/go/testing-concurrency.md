# testing-concurrency.md

**Location:** `go/testing-concurrency.md`

**Principle**
Code that touches shared state must be tested with `go test -race`, and ideally as part of the `make verify`/CI gate, not optional. Use a table-driven pattern for race scenarios: spawn N goroutines in parallel performing the same operation against the same state, then assert an invariant at the end — not just "it didn't crash," but an invariant that genuinely reflects correctness (e.g. the final total must equal the expected sum).

**Bad**
```go
func TestConcurrentUpdate(t *testing.T) {
    for i := 0; i < 10; i++ {
        go update(shared)
    }
    time.Sleep(time.Second) // no race detector, no invariant assertion
}
```

**Good**
```go
func TestConcurrentBalanceUpdate(t *testing.T) {
    // run with: go test -race
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
- [ ] `go test -race` runs as part of the verify step, not occasionally by hand
- [ ] Tests for shared-state code assert a clear invariant, not just "didn't crash"
- [ ] The number of parallel goroutines in the test is enough to realistically trigger a race (not just 2-3)
- [ ] Code protected by a mutex/atomic has a test that actually exercises that protection, not just the sequential happy path