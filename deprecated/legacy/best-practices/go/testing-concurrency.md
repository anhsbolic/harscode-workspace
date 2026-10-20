# Go Concurrency and Race Verification

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** Go shared-memory concurrency, concurrent HTTP requests, transaction races and race-sensitive invariants.
> **Triggers:** goroutine, concurrency, data race, locking, duplicate request, transaction conflict, go test -race.

## 01 — Applicability

Use when goroutines share mutable data, requests can overlap, or correctness depends on ordering and concurrent effects. Distinguish *Go data races* from *database logical races*: neither test class replaces the other.

## 02 — Principle / Rule

- Avoid unsynchronized shared-memory read/write access; prefer clear ownership, synchronization or message passing as fits the actual design.
- Run `go test -race` on targeted packages/test suites when shared-memory concurrency matters. The race detector only detects races on **executed paths**, not all possible races.
- Test application/database invariants under genuinely overlapping operations (duplicate requests, concurrent claims, conflicting updates), not merely sequential calls or a race-detector pass.
- Bound goroutine lifetime and ensure tests wait for spawned work to finish; do not create timing-only tests that routinely pass without exercising the contested interleaving.

## 03 — Rationale & Risk

A concurrent map access can panic or corrupt state. A race-free Go program can still allow a database check-then-insert conflict, duplicate effect or lost update. Arbitrary sleeps make flaky tests and provide weak concurrency coverage.

## 04 — Application Guidance

1. Identify specific shared state and invariants, then choose synchronization/ownership intentionally.
2. Use barriers/channels or test-controlled coordination to cause meaningful overlap; assert legal final states and exactly-once outcomes only where required.
3. Run focused tests with `-race` when supported and repeat stress cases where useful; capture race reports and treat observed races as failures.
4. For PostgreSQL races, use real separate connections/transactions, actual isolation levels and constraints; see `../postgresql/transactions-and-locking.md` and `integration-testing-setup.md`.
5. Assert failure/timeout cleanup so goroutines and locks cannot survive the test unboundedly.

## 05 — Verification

Document test command, number/type of concurrent actors, whether actual overlap was demonstrated, invariant assertions, detector result and environment. A passing `-race` run is **not** proof that all interleavings or cross-process/DB races are safe.

## 06 — Boundaries & Trade-offs

Race instrumentation increases runtime/memory use and is not available identically on every platform. Pure single-threaded code need not acquire concurrency tests by ritual. Historical product-specific examples may illustrate one failure but must not replace portable normative guidance.

## References

- https://go.dev/doc/articles/race_detector
- https://go.dev/doc/security/best-practices
- https://www.postgresql.org/docs/current/transaction-iso.html
