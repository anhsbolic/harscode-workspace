# Integration Testing Setup

Use real integration tests for behavior that cannot be credibly proven through unit/fake boundaries alone.

## Trigger

Integration testing is justified when correctness depends on a real runtime dependency or behavior such as:

- database constraints;
- transaction/rollback semantics;
- real query validity/driver behavior;
- migration/schema compatibility;
- connection-pool/resource behavior;
- another external/runtime contract that a fake cannot faithfully prove.

The existence of a database or external service alone is not a reason to integration-test every behavior.

## Test boundary

Keep integration tests explicitly separated from ordinary fast tests using the project's established mechanism (for example build tags, suites, targets, or environment gates).

Use isolated, reproducible test state and explicit cleanup.

## Transaction/resource safety

Every acquired transaction/resource must have a deterministic cleanup path.

For database-backed tests:

- guard `BeginTx`/equivalent acquisition immediately with rollback/cleanup unless ownership is intentionally transferred;
- commit explicitly only when the scenario requires it;
- ensure failed/aborted tests do not leave pooled resources, child processes, or containers alive.

## Failure visibility

Use bounded execution/timeouts for integration suites so leaked resources/deadlocks become visible failures rather than indefinite hangs.

After an abnormal timeout/abort, confirm test processes/runtime dependencies are actually terminated before interpreting later failures.

## Evidence discipline

Integration evidence should target the behavior that only the real dependency proves. Do not replace cheaper credible tests with real-runtime execution merely for ceremony.

Historical calibration/examples: `examples.md#for-integration-testing-setupmd`.
