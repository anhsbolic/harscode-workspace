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

Use the Techplan Testing Checklist's verification ownership/rationale to keep the loop proportional:

- run Build-owned checks that provide fast confidence for the behavior being edited;
- when Build adds or materially changes an automated test, run it enough to establish that the authored test is executable and actually exercises the intended state, even when independent Testing owns the final/broad evidence;
- do not replay broad Testing-owned suites merely for extra confidence unless target-repo authority explicitly requires them at this point, the current edit materially changes the relevant risk, or the broader suite is the only credible way to validate the change;
- after a narrow Review/Testing patch, rerun the affected verification first and broaden only when the patch changes scope/risk or wider regression evidence is necessary.

Race/concurrency, performance/load, and security-class sweeps belong to independent Testing when the Techplan/Test Focus Pointer requires them. Do not turn every Build iteration into final verification.

For a non-trivial check, preserve the Techplan's reason/risk rather than treating the tool name itself as authority. Browser automation, production builds, race detectors, or other expensive verification should be run here only when the Build loop genuinely needs that evidence; their final verification ownership may remain Testing/Human.

Expensive test fixtures (e.g. password KDFs) use test-appropriate cost/work factors where the applicable best practice requires it.

## Patch ownership

Review/Testing produce findings/patch plans; production code changes execute here. A patch may reuse a healthy Build session or start a fresh Build session re-grounded on the smallest sufficient durable state per `workflow/context-management.md`.

When handing the patch back, state the requesting phase explicitly. A narrow patch should normally return to the phase that requested it rather than automatically starting a new full review loop.

## Material contradiction rule

Do not silently choose between contradictory material instructions. Behavior, authority/security, data/interface shape, architecture/ownership, and verification strategy must be resolved in the authoritative Techplan/human gate.

Mechanical local ambiguity (naming/internal shape) may be resolved using current target-repo convention and live precedent, then recorded in the build report when useful.
