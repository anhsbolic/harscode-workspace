# Guidelines

The build/patch implementation loop: the tight edit → run → fix cycle
that happens after a techplan is approved and before code review.
Lightweight tier — same as `exploration/`, `code-review/`, `testing/`,
`pull-request/` — no protected files, no proposal process, corrected
in the moment.

## Default test scope (always, regardless of techplan content)

Run unit tests, mocked-service tests, and API-contract/functional
tests only. This is the fixed default for every iteration of this
loop — it does not vary by story, by techplan content, or by what the
Test Focus Pointer (techplan § 12, if present) says.

Race/concurrency (`-race`), performance/load, and security-class tests
never run inside this loop, even for an area the Test Focus Pointer
marks Y. A Y in that table is an instruction for the testing phase
(`workflow/5-testing/`) to schedule those test classes there — it is
not an instruction to run them here.

This boundary exists because of a real incident: a full-package
`-race` run combined with production-cost bcrypt inside this loop
caused a ~2-hour build stall (see
`best-practices/go/testing-concurrency.md` and
`best-practices/go/expensive-primitives-in-tests.md`).

## If you're about to reach for a heavier test class

Stop and ask: is this actually needed to confirm the current change
satisfies the API/interface contract? If the honest answer is "I want
extra confidence about concurrency/performance/security," that
confidence belongs in the testing phase, not here — note it as a
suggested Test Focus Pointer entry for the next techplan review
instead of running it now.

## Expensive primitives in test fixtures

Any fixture/helper created or touched in this loop that hashes a
password or runs a KDF must use a minimal test-time cost/work factor
(`bcrypt.MinCost`, not `bcrypt.DefaultCost`) — see
`best-practices/go/expensive-primitives-in-tests.md`. This matters
specifically here because it's the fast-iteration loop: a slow fixture
here is paid on every single iteration, not once.

## What this phase is not

Not where architectural decisions get revisited. If implementation
reveals the techplan's contract doesn't actually hold — a rule can't
be satisfied as written, an assumption turns out wrong — that's a
stop-and-ask moment (loop back to techplan), not a silent workaround
or a silent reinterpretation of scope.