# Go Integration Testing with Real Dependencies

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** Go integration verification of database constraints, transactions, persistence, HTTP wiring or external adapters.
> **Triggers:** integration test, PostgreSQL, test database, migration, transaction, contract, build tag.

## 01 — Applicability

Use integration tests for behavior that fakes cannot establish: actual SQL, schema constraints, transaction visibility, concurrency across database connections, and end-to-end adapter/transport integration. Pure functions and isolated policies can use unit tests.

## 02 — Principle / Rule

- Run consequential integration tests against a suitably isolated real dependency and schema version; never point tests at production or reuse shared live data without explicit permission.
- Make environment prerequisites, invocation command, migrations and cleanup deterministic enough to reproduce evidence.
- **Build tags are a project choice**, not a universal Go requirement. If isolated with `//go:build integration`, use `go test -tags=integration ./...`; tests behind the tag do not run during ordinary `go test ./...`.
- Verify observable committed state and the relevant negative path, not just mocked method calls.
- Do not silently report integration PASS when a missing database caused tests to be skipped.

## 03 — Rationale & Risk

Mocks can conceal invalid SQL, migrations, isolation mistakes and lack of constraints. Non-isolated tests pollute state or produce order-dependent false positives. A misleading skipped suite is not evidence.

## 04 — Application Guidance

1. Define a separate, disposable test database/namespace; use a known migration state and intentionally nonproduction credentials.
2. Establish test preconditions and teardown. When tests run in parallel, isolate data per test or use independent databases; a shared cleanup can erase another test's evidence.
3. Prefer explicit fixture creation and assertions on committed rows, relationships, error categories and post-failure state.
4. For HTTP integration, exercise real handlers and service wiring; when authentication/authorization matters, test genuine trust boundaries rather than injecting an omnipotent fake.
5. Record commands, test environment and exact skipped/failing cases. Tag or separate heavy suites only if doing so helps predictable execution.
6. Keep previously documented historical Kencleng examples in historical evidence, not as portable primary test principles.

## 05 — Verification

At minimum run the focused integration command against the prepared database; check actual DB state after success and forced failure. For concurrent invariants launch truly overlapping transactions and assert one legal outcome; separately add `-race` where shared-memory races are plausible. State what did not run.

## 06 — Boundaries & Trade-offs

Real dependencies increase cost and setup. A small isolated unit test may be sufficient for pure behavior. Not every integration test needs a container runner or special build tag. Integration tests are necessary where DB correctness is claimed but not sufficient to prove full security/UX correctness.

## References

- https://pkg.go.dev/cmd/go#hdr-Build_constraints
- https://go.dev/doc/articles/race_detector
- https://www.postgresql.org/docs/current/transaction-iso.html
