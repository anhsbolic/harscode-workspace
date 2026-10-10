# Pilot #2 Candidate Guidance Index

> Status: PILOT #2 CANDIDATE ROUTING INDEX / NON-AUTHORITATIVE
> Scope: discoverability and ownership inside the Pilot #2 candidate layer.
> This index does not override `orchestration/protocol-v0.1.md`, canonical
> `workflow/` guidance, target-project authority, or Human-owned runtime policy.

## Purpose

Prevent historical CRTV notes, earlier design checkpoints, and overlapping
candidate documents from becoming competing current guidance.

Use this order when reconstructing Pilot #2 guidance:

1. canonical protocol / workflow / target-project authority;
2. the **current candidate concern owner** named below;
3. supporting candidate guidance when the owner points to it or the current
   concern needs its deeper rationale;
4. historical CRTV notes / change maps only for evidence, regression analysis,
   or design history.

If a candidate document conflicts with canonical authority, canonical authority
wins. If two candidate documents overlap, use the narrower current concern owner
for mechanics in its scope and treat broader documents as coordination/routing
context unless they explicitly own the concern.

"Owner" below means **current routing owner inside the non-authoritative
candidate layer**. It does not grant project or Human decision authority.

## Current candidate concern owners

| Concern | Current candidate owner | Notes |
|---|---|---|
| Orchestrator responsibility, Human pairing posture, authority mapping, Decision propagation, scoped blockers, projection discipline, Human-Assisted coordination | `orchestrator-operating-model.md` | Cross-cutting coordination owner. Should route to narrower documents rather than duplicate their mechanics. |
| Run Invocation, Run/Participant/Session lifecycle, same-Run Session renewal, later re-entry, Handoff/reconciliation, Run artifact proportionality | `participant-execution-continuation.md` | Current execution/continuation mechanics owner. |
| Participant Profile lifecycle, evidence sufficiency, reusable capability boundaries, required/routed guidance | `participant-profile-discovery.md` | Profile semantics only; no hidden agent memory or decision authority. |
| Initial project orchestration bootstrap and bounded Slice readiness reconciliation | `project-orchestration-bootstrap.md` | Bootstrap/readiness owner; not a per-Run ceremony. |
| Generic Participant Run model/effort routing and escalation diagnosis | `model-routing-and-escalation.md` | Model names remain runtime/local data; candidate semantics should stay capability-based. |
| Run execution envelope and permission routing | `run-execution-envelope-and-permissions.md` | Authorization classes and Human/Orchestrator/Participant routing. |
| Dependency-driven parallelism, milestones, rendezvous, scoped invalidation | `parallelism-and-rendezvous.md` | Semantic parallelism is separate from machine-level concurrency. |
| Verification ownership, traceability, specialized verification triggers | `verification-strategy-and-traceability.md` | Complements canonical Techplan/Build/Testing guidance. |
| Workflow phase applicability, patch/re-entry routing, ordinary loop interpretation | `workflow-topology-and-applicability.md` | Does not override canonical phase prompts. When strict loop-health escalation triggers are met, route to `loop-health-audit.md` rather than duplicating the diagnostic protocol here. |
| Loop-health trigger thresholds, Human-gated independent diagnostic audit, audit verdict/resume contract | `loop-health-audit.md` | Experimental diagnostic owner only. Does not create a new protocol state, replace canonical `STALLED`, or authorize project mutations. |

## Supporting / contextual candidate documents

These documents remain useful, but they are not the first source for mechanics
already owned above.

| Document | Current interpretation |
|---|---|
| `session-fitness-continuation-and-recovery.md` | Supporting rationale/evidence for Session fitness, recovery, observability, and fresh-Orchestrator reconstruction. Active Run/Participant lifecycle mechanics are owned by `participant-execution-continuation.md`. |
| `observability-and-execution-hypothesis.md` | Supporting Pilot #2 observability and Human-Assisted execution hypothesis. Current coordination posture is owned by `orchestrator-operating-model.md` plus the applicable execution/permission documents. |
| `state-and-artifact-model.md` | Earlier state/artifact design snapshot. Canonical state semantics now come from `orchestration/protocol-v0.1.md`; current projection/current-state discipline is refined by `orchestrator-operating-model.md`. Physical layout examples are illustrative, not mandatory. |

## Historical / CRTV evidence

These are evidence/history, not current execution guidance:

- `consolidated-pilot-1-review-and-change-map.md`;
- `parallelism-and-rendezvous-crtv-notes.md`;
- `session-observability-crtv-notes.md`;
- `workflow-topology-crtv-notes.md`.

Do not promote a statement from these files into current Pilot #2 behavior merely
because it was true during Pilot #1 or an earlier checkpoint.

## Canonical boundaries that candidate guidance must preserve

Candidate documents in this directory must remain compatible with at least these
canonical invariants:

- `Run` is one execution occurrence of a workflow activity;
- re-entering a phase creates a new Run;
- Work Unit current-state fields have one current value;
- Work Graph owns cross-Work-Unit dependency topology;
- Events own material chronology, not current state;
- Control Surface is derived and never independent authority;
- terminal Work Units have no active scheduling posture;
- approved authority-affecting change flows
  `Finding → Decision → canonical authority update → downstream reconciliation`;
- model/runtime bindings are Human-owned runtime configuration.

When current CRTV evidence appears to require changing one of these, treat that
as a protocol/workflow change proposal rather than silently overriding it here.

## Maintenance rule

Before adding a new Pilot #2 candidate document, identify the real concern it
owns and verify that an existing owner cannot absorb the guidance cleanly.

Before extending `orchestrator-operating-model.md`, prefer a pointer to the
narrow current owner when the new text is implementation/mechanics detail rather
than cross-cutting Orchestrator behavior.

When a newer candidate document supersedes mechanics in an older checkpoint,
update this index and add a concise interpretation note to the older document if
direct reading could produce a materially wrong execution decision.
