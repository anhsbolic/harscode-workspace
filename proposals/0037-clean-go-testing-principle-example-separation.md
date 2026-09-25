# Clean Go testing principle/example separation

**Status:** Accepted
**Date:** 2026-09-25
**Protection Tier:** general
**Triggered by:** Kencleng Orchestrator Pilot #1 CRTV review found best-practice authority/example role contamination
**Target area:** best-practices
**Target file(s):**
- best-practices/go/testing-concurrency.md — replace historical example masquerading as authority with reusable principle guidance
- best-practices/go/integration-testing-setup.md — replace historical example masquerading as authority with reusable principle guidance
- best-practices/go/examples.md — create cold historical examples file and move the two Kencleng stories into it

## Gap found

Two files currently indexed as reusable Go best-practice authority are not principle guidance at all.

Both:

- begin with the heading `# go/examples.md`;
- describe specific Kencleng MFA testing incidents;
- present historical timing/process details;
- were apparently intended to live in a category-level examples file.

This conflicts with the existing best-practices governance rule that reusable principle files remain project-agnostic while concrete implementation stories live in `<category>/examples.md`.

Because `best-practices/index.md` routes agents directly to these filenames as authority, an agent can currently load project-specific history as if it were reusable runtime guidance.

## Proposed change

### 1. Create best-practices/go/examples.md

Create the category cold-reference file and move the existing historical content from both contaminated files into it.

Structure:

```markdown
# Go Examples

> Cold real-world references for reusable Go best-practice guidance.
> These examples calibrate the principle files; they are not runtime authority
> and should be opened only when a concrete ambiguity/history need warrants it.

## For: testing-concurrency.md

<existing Kencleng MFA race-scope example, preserved as historical evidence>

## For: integration-testing-setup.md

<existing Kencleng MFA transaction leak / orphan-process example, preserved as historical evidence>
```

Preserve the historical facts rather than deleting them.

### 2. Replace testing-concurrency.md with reusable principle guidance

Proposed semantic content:

```markdown
# Testing Concurrency

Use concurrency-specific verification only when the code or invariant actually involves concurrent access, shared mutable state, goroutine lifecycle, synchronization, or timing-sensitive behavior.

## Trigger

Use this guidance when a change touches:

- shared mutable state accessed concurrently;
- goroutine coordination/lifecycle;
- locks, atomics, channels, wait groups, or similar synchronization;
- invariants that can fail only under concurrent interleavings.

Go code by itself is not a reason to run the race detector.

## Verification

Prefer the smallest credible scope that exercises the real concurrency risk.

- Start with the relevant package/unit.
- Narrow further to relevant tests when unrelated sibling tests are expensive.
- Use invariant-asserting concurrent tests when a race-free execution alone would not prove the intended behavior.
- Run broader race coverage only when the changed risk is genuinely cross-cutting or project policy requires it.

The race detector is evidence for data races, not a substitute for behavioral concurrency assertions.

## Cost discipline

Race instrumentation can amplify unrelated test cost. Scope by both package and test selection where that preserves the required evidence.

Do not run broad `-race` sweeps merely because the project is written in Go.

Historical calibration/examples: `examples.md#for-testing-concurrencymd`.
```

### 3. Replace integration-testing-setup.md with reusable principle guidance

Proposed semantic content:

```markdown
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
```

### 4. Keep index routing unchanged unless wording needs minor clarification

The existing `best-practices/index.md` rows already route to the correct conceptual concerns:

- concurrency/race verification;
- DB-backed integration behavior.

After the principle files are restored, those rows become valid again.

No new mandatory read of `go/examples.md` should be added to the index.

## Rationale

This change restores the workspace's existing genericity and context-temperature rules:

```text
principle authority
→ reusable, project-agnostic, WARM/conditional

examples/history
→ concrete calibration, COLD
```

The reusable lessons are real and should be preserved:

- race verification should be risk-triggered and scoped;
- unrelated expensive tests can make broad race runs disproportionately costly;
- real integration tests should prove behavior fakes cannot;
- leaked transactions/resources can manifest as hangs and contaminate later test runs;
- explicit cleanup and bounded timeouts improve failure visibility.

But none of those lessons require Kencleng/MFA-specific history to sit inside the runtime authority files.

This is a documentation-role correction, not a change to project-specific testing policy.

---

*After human review: update the Status above. If Accepted, merge into the target document and leave this proposal in place (don't delete it) — it serves as this folder's changelog. See `proposals/README.md` for the Protection Tier distinction and numbering convention.*
