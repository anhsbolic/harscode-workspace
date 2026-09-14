# Build / Patch Guidelines

Build is the tight edit → run → fix loop after Techplan approval. Keep process narration terse and verification local enough for rapid iteration.

## Context boundary

Build starts from:

```text
Approved Techplan spine
+ current task slice when decomposed
+ specific patch plan when re-entering
+ relevant live code/spec at recorded anchors
```

Raw Exploration is not a default Build input. If a material contract assumption is missing, route back to Techplan rather than reconstructing product intent inside Build.

Reopen live code before editing. **Transfer coordinates, not cached facts.** If a code anchor moved, locate its current equivalent nearby; if its material contract premise no longer holds, stop/report.

## Default Build-loop test scope

Run ordinary fast verification appropriate to the target repo: unit, mocked-service/component, API/contract/functional tests that belong in the edit loop.

Race/concurrency, performance/load, and security-class sweeps belong to independent Testing when the Techplan/Test Focus Pointer requires them. Do not turn every Build iteration into final verification.

Expensive test fixtures (e.g. password KDFs) use test-appropriate cost/work factors where the applicable best practice requires it.

## Patch ownership

Review/Testing produce findings/patch plans; production code changes execute here. A patch may reuse a healthy Build session or start a fresh Build session re-grounded on the smallest sufficient durable state per `workflow/context-management.md`.

## Material contradiction rule

Do not silently choose between contradictory material instructions. Behavior, authority/security, data/interface shape, architecture/ownership, and verification strategy must be resolved in the authoritative Techplan/human gate.

Mechanical local ambiguity (naming/internal shape) may be resolved using current target-repo convention and live precedent, then recorded in the build report when useful.
