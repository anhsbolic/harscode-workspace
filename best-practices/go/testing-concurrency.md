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
