# Pilot #2 Candidate — Orchestration State & Artifact Model

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group A checkpoint only. This is a minimal durable-state hypothesis for Pilot #2, not a finalized storage/schema contract.

## Goal

Make current orchestration state unambiguous and reconstructable without turning Markdown history, Run reports, or the Control Surface into competing sources of truth.

## Minimal artifact roles

Pilot #2 needs six logical artifact roles:

1. **Parent Outcome**
2. **Work Graph**
3. **Work Unit record**
4. **Event log**
5. **Run directory**
6. **Control Surface**

A material Decision may additionally use a dedicated Decision artifact.

## Candidate layout

```text
.harscode-spaces/<outcome>/
├── outcome.md
├── work-graph.md
├── events.md
├── control-surface.md
├── decisions/
└── WU-.../
    ├── manifest.md
    └── runs/
        └── <RUN-ID>/
            ├── invocation.md
            └── <workflow-owned artifacts>
```

The exact serialization format is intentionally not settled. Pilot #2 should prefer boring human-readable files until stronger machinery is justified by evidence.

## Parent Outcome

Answers:

> What larger approved result is being coordinated?

It records a stable outcome identity, outcome statement, and authority pointers. It does not own detailed progress.

## Work Graph

Answers:

> What bounded Work Units are currently known, what do they depend on, and what milestone/rendezvous does each produce?

The Work Graph owns cross-Work-Unit orchestration topology:

- Work Unit identities;
- canonical causal HARD/SOFT dependency edges;
- produced milestone/rendezvous conditions;
- structural derivation/split/merge relationships where relevant.

The Work Graph must not become a shadow Techplan. It does not own implementation steps, API/schema details, file edits, or detailed verification procedures.

Dependency edges are not duplicated as independently maintained current truth inside each Work Unit record. A Work Unit may point to or display a derived dependency summary for readability, but the Work Graph remains the canonical cross-Work-Unit topology.

## Work Unit record

A Work Unit record separates stable definition from current mutable state.

Conceptual shape:

```text
Definition
- ID
- Type
- Parent
- Outcome
- Scope / out of scope
- Completion condition
- Coordination owner

Current State
- Execution status
- Scheduling state
- Readiness
- Horizon
- Current Run
- Current milestone
- Human gate
- Authority sync
- Active blocker
- Updated
```

### Critical rule

There is exactly one current value for each current-state field.

Current State is updated by replacement, not by appending a newer contradictory status section below an older one.

Previous state belongs in Events.

## Event log

The Event log is append-only coordination history.

Record material facts such as:

- Run dispatched/completed/failed;
- Work Unit state transition;
- Human Decision recorded;
- Blocker opened/closed;
- milestone promoted;
- Work Graph structurally amended.

Do not use the global Event log for every file read, shell command, or tool call. Detailed execution telemetry belongs with the Run.

## Run directory

A Run is one workflow execution occurrence.

Its directory owns:

- Orchestrator-generated invocation;
- workflow-owned durable artifacts;
- report/evidence produced by the assigned Participant;
- optional execution telemetry.

A Participant reports its workflow outcome. The Orchestrator reconciles that outcome into coordination state.

```text
Participant verdict/evidence
→ Orchestrator reconciliation
→ Work Unit state transition
```

Participants do not directly self-promote Work Units to project milestones.

## Decisions

Material governance questions/results remain Decisions, not pseudo-Work-Units.

A durable Decision should be used when the result matters beyond a transient Run, especially for Human Authority or protected authorization.

Approval evidence may cause an Orchestrator state transition, but Decision and Work Unit remain distinct objects.

## Control Surface

The Control Surface is a Human/operator projection of current state.

It may show:

- current Parent Outcome;
- NOW / NEXT / LATER;
- running/ready/blocked/stalled work;
- Human attention;
- active Sessions;
- next actions.

It must be regenerable from underlying orchestration records.

Loss of `control-surface.md` must not lose orchestration truth.

## Development tracker boundary

A project-level development tracker may own coarse delivery reporting, for example:

```text
Slice 1 = SLICE_FINALIZED
Slice 2 = NOT_STARTED
```

It should not become the execution database for Runs, Sessions, review rounds, or launcher state.

## Runnable frontier

The Orchestrator should be able to derive ready work from:

```text
Work Graph
+ current Work Unit states
+ dependency satisfaction
+ open Blockers
+ unresolved required Decisions
```

Independent Work Units may proceed without waiting for unrelated branches of the graph. Rendezvous/integration waits only on its actual HARD dependencies.

## State-model defect exposed by Pilot #1

Pilot #1 demonstrated why this separation is needed:

- several Work Unit manifests retained `NOT_STARTED` headers while later sections said `DONE`;
- the Control Surface retained a stale `NOT_YET_APPROVED` finalization claim while the same artifact also said `SLICE_FINALIZED`;
- the project tracker mixed completed history with current-gate wording.

The candidate model treats those as structural state/projection drift, not isolated copy-editing mistakes.

## Open item for later protocol revision

Scheduling currently has:

```text
PARKED | QUEUED | DISPATCHED | RUNNING
```

Pilot #1 incorrectly produced `Scheduling: DONE`.

Pilot #2 should not invent a new enum ad hoc. The protocol review should later decide how scheduling is represented when execution status is terminal (for example, non-applicable/null versus another explicit state).
