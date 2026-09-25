# Pilot #2 Candidate — Parallelism & Rendezvous

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group D checkpoint only. This document records CRTV conclusions about dependency-driven parallel work and rendezvous semantics. It does not override canonical workflow or target-project architecture.

## Purpose

Allow independent Work Units to progress without unnecessary lockstep while preserving truthful dependency, evidence, and integration boundaries.

Core principle:

> Parallel delivery is governed by dependency satisfaction and evidence boundaries, not by stack synchronization.

## Dependency-driven progress

A Work Unit may progress when its HARD dependency conditions are satisfied and no active blocker/required decision prevents execution.

Sibling progress alone does not block a Work Unit.

Example:

~~~text
CONTRACT_READY
├── Backend WU
├── Frontend WU
└── Topology WU
~~~

If all three require only CONTRACT_READY, all three are semantically runnable even when their internal implementation styles differ.

A sibling that remains active does not prevent another sibling from reaching its own verified milestone when its own completion condition is satisfied.

## Milestones are evidence boundaries

A Work Unit milestone should describe what its own evidence actually proves.

Example:

~~~text
Backend
→ BACKEND_VERIFIED

Frontend against contract-faithful substitute boundary
→ FRONTEND_MOCK_VERIFIED

Topology
→ TOPOLOGY_VERIFIED
~~~

These milestones do not claim whole-system integration.

Milestone names should not overclaim evidence scope.

## Two rendezvous points

### Early rendezvous — shared contract

Independent work can start once the relevant shared contract/authority is stable enough.

~~~text
product/domain truth
→ reconciled shared contract
→ independent implementation
~~~

The contract establishes what must be true without forcing local decomposition to match.

Reusable principle:

> Decomposition may remain local; shared contracts provide the coordination boundary.

Backend may remain domain-oriented while frontend remains surface/experience-oriented, provided both consume the same contract truth.

### Late rendezvous — real integration

Independent correctness does not prove composition.

A later integration/verification Work Unit proves that independently verified capabilities actually work together across the real runtime boundary.

~~~text
verified backend
+ verified frontend
+ verified topology/runtime
→ real integration
→ INTEGRATED_VERIFIED
~~~

Integration is a distinct evidence boundary, not merely “all branches appear complete.”

## Integration readiness

An integration Work Unit becomes runnable only when its declared HARD milestone dependencies are satisfied.

Example:

~~~text
Integration requires:
- BACKEND_VERIFIED
- FRONTEND_MOCK_VERIFIED
- TOPOLOGY_VERIFIED
~~~

If Backend and Frontend are done while Topology is still running:

~~~text
Backend = DONE
Frontend = DONE
Topology = RUNNING
Integration = PARKED
~~~

Do not reopen completed siblings merely because rendezvous is not ready.

Reopen only when new evidence invalidates a prior milestone claim.

## Soft vs hard dependencies

Dependency strength must reflect what evidence is required for the Work Unit's own completion condition.

A relationship is HARD when the Work Unit cannot credibly satisfy its own completion condition without that dependency.

A relationship is SOFT/coordination-only when work can proceed and the Work Unit can still prove its own bounded outcome independently.

Do not label a dependency SOFT merely because teams/components are different.

Do not label it HARD merely because components interact somewhere later.

## Contract-faithful substitute boundaries

A Work Unit may use a substitute boundary to remove unnecessary scheduling dependency when:

- the shared contract is stable enough;
- the substitute uses the same production-facing request/response/interaction shape;
- it does not invent separate business semantics;
- the real runtime path will still receive independent integration verification.

Examples may include network-boundary mocks, local fakes, emulators, or equivalent mechanisms chosen by the target project.

Harscode does not mandate a specific tool such as MSW.

## No second semantic truth

A substitute boundary is unhealthy when it becomes a separate semantic implementation.

Avoid:

~~~text
frontend-local eligibility logic
mock-only funding calculation
alternate error semantics
mock-only lifecycle state machine
~~~

Prefer:

~~~text
same contract
same types/schema
same status/error semantics
same production request boundary
different runtime provider only
~~~

The substitute exists to decouple scheduling, not to fork product/business truth.

## Integration is not a dumping ground

Independent Work Units must prove their own owned correctness before integration.

Healthy:

~~~text
Backend proves backend-owned behavior
Frontend proves frontend-owned behavior
Topology proves topology-owned behavior
Integration proves composition
~~~

Unhealthy:

~~~text
Backend partly verified
Frontend partly verified
Topology uncertain
→ hope integration reveals/fixes everything
~~~

Integration must not hide missing local verification obligations.

## Runnable frontier vs execution concurrency

Separate semantic runnable frontier from safe concurrent execution on the current machine/workspace.

Multiple Work Units may be READY semantically while the runtime scheduler still serializes their actual mutation.

Reasons may include:

- shared working tree;
- branch/worktree safety;
- shared mutable local environment;
- harness limitations;
- resource constraints.

Therefore:

> READY does not imply RUNNING immediately.

The Orchestrator may queue semantically parallel work when local execution safety requires serialization.

## Same-repository mutation safety

Pilot #2 uses Automated Visible Fleet and may expose true concurrent repository mutation for the first time.

Do not introduce a generic worktree/branch strategy before evidence requires it.

For now:

- preserve semantic parallelism in the Work Graph;
- allow the scheduler to serialize unsafe simultaneous mutation;
- treat repeated concurrency friction as CRTV evidence for later workspace-isolation design.

## Contract change during parallel work

A Participant must not silently change the shared contract while siblings execute against it.

When a material shared contract issue is discovered:

~~~text
Finding
→ contract/authority reconciliation
→ identify affected Work Units/evidence
→ pause/block only affected work
→ approve/reconcile contract change
→ refresh affected downstream artifacts/evidence
~~~

Do not freeze unrelated work automatically.

Use dependency-scoped invalidation.

## Evidence invalidation

When the shared contract changes materially, determine which prior artifacts/milestones are no longer current.

Potentially affected artifacts include:

- generated client/server types;
- substitute-boundary handlers/fixtures;
- frontend assumptions;
- backend handlers;
- topology routing/policy;
- prior verification evidence.

Do not assume all evidence becomes stale; invalidate only what the change materially affects.

## Orchestrator responsibilities

The Orchestrator owns:

- HARD/SOFT dependency representation;
- runnable-frontier computation;
- rendezvous readiness;
- scheduling/queuing decisions;
- scoped invalidation/reconciliation after material contract change;
- prevention of integration from starting before required milestone evidence exists.

The Orchestrator does not:

- force backend/frontend/topology to share one decomposition axis;
- invent contract semantics;
- treat terminal/window state as dependency truth;
- convert a SOFT relationship into a hidden global wait without evidence.

## Pilot #2 success signals

This model is working when:

- independent Work Units progress without unnecessary sibling waiting;
- integration starts only from earned milestone conditions;
- substitute boundaries reduce scheduling dependency without creating semantic forks;
- completed sibling milestones stay stable unless genuinely invalidated;
- the scheduler can serialize unsafe local concurrency without corrupting semantic readiness;
- contract changes pause/reconcile only affected work;
- integration verifies composition rather than compensating for missing local correctness.
