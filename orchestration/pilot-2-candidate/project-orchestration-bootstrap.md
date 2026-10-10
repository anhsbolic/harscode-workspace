# Pilot #2 Candidate — Project Orchestration Bootstrap

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: initial orchestration readiness for a target project. This guide does not override project authority, canonical workflow guidance, or `orchestration/protocol-v0.1.md`.

## Purpose

Establish the minimum durable orchestration state required to begin real project work safely.

Bootstrap is initial coordination preparation, not project completion and not a ritual that repeats before every Run or Work Unit.

Bootstrap MUST NOT require:

- project-wide documentation completeness;
- complete architecture discovery;
- enumeration of all future authority areas;
- creation of all future Participant Profiles;
- complete best-practice coverage;
- runtime/fleet automation;
- planning the entire project.

Bootstrap ends when the first justified real Work Unit / Run can be dispatched safely.

Core principle:

> Bootstrap should stop as soon as continuing bootstrap work has less value than starting the first real Run.

## Core rules

- initialize the minimum stable orchestration foundation justified by the near-term project shape and initial runnable frontier;
- prefer durable project evidence over assumption;
- discover progressively after bootstrap;
- block only the work whose correctness depends on missing state;
- bootstrap coordinates existing project truth and must not invent it;
- bootstrap artifacts record pointers/readiness, not replacement authority;
- no future-applicable setup is required merely for completeness;
- a complete Work Graph is not required at bootstrap.

## Project identity and orchestration context

Bootstrap must establish enough durable context for a fresh Orchestrator to identify the same project and working context.

At minimum, make discoverable:

- project identity;
- relevant repository or repositories;
- current working context such as branch, Slice, initiative, or delivery context when material;
- applicable Harscode protocol/candidate guidance;
- durable orchestration root or state location.

The purpose is not to freeze repository state permanently. The purpose is to answer:

> What project/work context is being orchestrated now?

If that is materially ambiguous, bootstrap is not yet safe.

## Current objective and near-term intent

Before broader discovery, the Orchestrator must establish the smallest durable statement of the near-term project objective.

The objective should answer:

> What real work is this project trying to start next?

Examples may include:

- deliver an approved MVP Slice;
- establish Product/technical Exploration for an initial MVP;
- reconcile an approved contract before Build.

Readiness for authority, Participant Profiles, runtime, and documentation is scoped to this near-term objective, not to the entire future project.

If the objective is insufficiently bounded, route the smallest necessary upstream clarification rather than inventing Product intent.

## Authority readiness

Bootstrap uses the current project Authority Map and existing Authority Discovery / Authority Sync semantics.

Bootstrap only needs to determine whether authority ownership is sufficiently known for the initial runnable frontier.

It does not require all future authority areas to be enumerated.

If a missing authority area does not affect the initial frontier, defer it.

If the initial frontier depends on a material decision whose owner is unknown or ambiguous, route Authority Sync before that dependent decision is required.

## Participant Profile readiness

Bootstrap must use `participant-profile-discovery.md` rather than duplicating Participant Profile discovery logic.

Input should remain limited to:

- near-term objective;
- current durable project evidence;
- initial work shape.

The output is the minimum reusable Participant Profile baseline justified by current durable evidence and near-term project shape.

Bootstrap may seed a small stable project team beyond the literal first Run when the near-term workflow/repository evidence already makes those recurring capabilities clear and reusable. For example, a project may justifiably establish baseline Explorer, Planner, Implementer, Reviewer, or Verifier Profiles when their expected use is already evidenced.

It is also valid for bootstrap to require only an Explorer profile if Exploration is the only capability currently justified.

Do not create specialist or future Profiles merely because they might become useful later. Bootstrap should establish an evidence-backed baseline team, not speculate about every future capability.

The Profile readiness guardrails remain:

- minimum material evidence, not complete project documentation;
- optional/future guidance must not block;
- prefer the least-specific safely supported profile before blocking;
- profile creation does not grant decision authority.

## Participant Profile Registry

The project should expose a discoverable registry/index for current Participant Profiles when reusable profiles exist.

The registry is a routing surface, not a Run-state database.

A minimal registry may expose:

- Profile ID;
- Role;
- Specialization;
- status;
- definition pointer;
- replacement pointer when applicable;
- short purpose when useful.

The registry should point to current-effective profile definitions rather than duplicate their capability/guardrail content.

Prefer Git history for profile evolution instead of creating a heavy profile-versioning system.

Suggested lifecycle semantics:

- `ACTIVE` — may be selected for new Runs;
- `DEPRECATED` — avoid for new Runs; replacement/transition exists;
- `RETIRED` — must not be selected for new Runs.

Do not create placeholder/DRAFT profiles merely because evidence is incomplete. Record a discovery gap instead.

The registry must not store:

- current Work Unit assignment;
- current Session;
- current Techplan/Open-Item state;
- prior Run outcomes as personal memory.

## Runtime and model readiness

For Pilot #2, runtime readiness is semantic and minimal.

Bootstrap only needs enough durable information to answer:

> Can the next Participant Run actually be dispatched?

Make discoverable when relevant:

- dispatch posture;
- execution harness;
- runtime/model registry or routing policy;
- reasoning options;
- project working directory or execution location.

For Human-Assisted Orchestration, runtime bootstrap does not require terminal/window/fleet automation, process supervision, prompt injection infrastructure, or live monitoring.

Those mechanics remain outside Pilot #2 success criteria unless narrowly required to unblock execution.

## Durable orchestration-state readiness

A fresh Orchestrator must know where durable orchestration truth can be reconstructed.

Bootstrap should establish pointers to currently material sources such as:

- Authority Map;
- Participant Profile Registry;
- runtime/model registry;
- Work Graph / orchestration state;
- Decision / Finding / Learning locations when applicable;
- Control Surface when applicable.

Discoverability does not require pre-creating every artifact.

A not-yet-materialized Work Graph or Control Surface is valid when no justified topology/state yet exists, as long as the future location/creation route is clear enough.

Do not create a tracker, dashboard, Control Surface, or other convenience
projection merely because bootstrap has a slot for durable state. Create a
projection only when it serves a concrete coordination/Human-readability need.
When created, it must remain derived from its owning state rather than becoming
a parallel source that must be reconciled independently.

## Initial Outcome and Work Decomposition

Bootstrap may derive a Parent Outcome from a sufficiently authoritative upstream objective.

The Parent Outcome is an orchestration representation of project intent, not a new source of Product authority.

It must preserve provenance to the upstream objective.

The Orchestrator may perform coordination-only decomposition.

It must not create new material Product, Design, Security/Privacy, Architecture, or interface obligations through decomposition.

Rules:

- derive only the minimum topology needed to expose the first runnable frontier;
- do not plan the entire project during bootstrap;
- if solution/decomposition evidence is insufficient, prefer an Exploration or Planning Work Unit over speculative implementation decomposition;
- expand Work Graph detail progressively as new durable evidence appears;
- a coordination-only split may be Orchestrator-owned;
- a split that establishes or changes material authority/contract/architecture obligations requires supporting authority/evidence first.

Bootstrap does not require a complete Work Graph.

A healthy bootstrap may produce:

```text
authoritative upstream objective
→ Parent Outcome
→ first bounded Work Unit
→ first justified Run
```

and stop there.

## Initial runnable frontier

The initial runnable frontier is the primary bootstrap completion output.

It should make discoverable at least:

- Work Unit;
- Run;
- Role;
- Participant Profile when used;
- short evidence-based rationale.

The rationale should establish that:

- the current objective is sufficiently known;
- required authority for this frontier is sufficient;
- required Participant capability is available;
- runtime dispatch is possible;
- no material prerequisite blocks the Run.

If no first Run can yet be justified, bootstrap remains incomplete and should classify the actual blocking cause.

## Gap handling

Useful bootstrap gap classes include:

- upstream objective ambiguity;
- authority gap;
- documentation/evidence gap;
- Exploration gap;
- Participant capability gap;
- runtime/environment gap.

Do not create a heavier taxonomy unless CRTV evidence requires it.

For each gap, ask:

> Does this materially block the initial runnable frontier?

If no:

- record it when useful;
- defer it;
- continue bootstrap.

If yes:

- route the smallest necessary resolution;
- block only the dependent work.

Do not use generic `Bootstrap blocked` when a specific gap and continuation route can be stated.

## Bootstrap Record

A Bootstrap Record is a thin routing/readiness artifact.

It is not a duplicate source of authority.

It should point to current-effective sources rather than copy their contents.

A minimal shape may include:

```yaml
bootstrap_id: BOOTSTRAP-001

project:
  id: <project-id>
  repositories:
    - <pointer>
  working_context: <branch/slice/initiative when relevant>

harscode:
  protocol: <pointer>
  candidate_guidance:
    - <pointer>

current_objective:
  summary: <near-term objective>
  source: <durable source>

authority:
  status: sufficient_for_initial_frontier
  source: <Authority Map pointer>

participant_profiles:
  status: sufficient_for_initial_frontier
  registry: <registry pointer>
  initially_required:
    - <profile-id>

runtime:
  status: ready
  source: <runtime/model registry pointer>
  dispatch_posture: human-assisted

durable_state:
  orchestration_root: <pointer>
  work_graph: <pointer or not-yet-materialized>
  control_surface: <pointer or not-yet-materialized>

initial_runnable_frontier:
  work_unit: <id>
  run: <id>
  role: <Role>
  participant_profile: <profile-id>
  rationale: <short evidence-based rationale>

deferred_gaps:
  - <material-but-non-blocking gap>

bootstrap_status: COMPLETE
```

The exact storage/layout remains project-defined.

Suggested bootstrap status semantics for Pilot #2:

- `IN_PROGRESS`;
- `BLOCKED`;
- `COMPLETE`.

These are candidate semantics, not canonical protocol enums.

`COMPLETE` means:

> The first justified real Run can now start safely.

It does not mean project orchestration setup is permanently finished.

## Post-bootstrap lifecycle

After initial bootstrap, normal orchestration should not repeat bootstrap or run a visible profile-readiness ceremony before every Run.

### Fresh Orchestrator Session resume

A new Orchestrator Session is a reconstruction event, **not** a new project
bootstrap and not a reason to require a detailed Human handover prompt.

When project identity and the active working context are already discoverable,
a simple Human continuation intent such as `Continue from current durable
state` should be sufficient. The Orchestrator owns the rest of the
reconstruction.

Before choosing a frontier or asking the Human to restate prior decisions, a
fresh Orchestrator should:

1. resolve the target project's current working context and durable
   orchestration root;
2. load current Harscode orchestration routing/guidance applicable to that
   context;
3. resolve the project's current communication profile/rule;
4. reconstruct Work Unit / Work Graph current state from their semantic owners,
   then read only the current-effective workflow artifact(s) needed for the
   frontier;
5. re-read the current Authority Map and material durable Decisions/Events that
   post-date or may invalidate the current-effective workflow artifact;
6. check whether derived projections agree with their semantic owners and
   regenerate/reconcile them only when needed;
7. inspect the recent material blocker/re-entry/recovery chain for the current
   bounded concern. When that chain shows suspected repeated causal routing or
   diminishing-return re-entry, consult `loop-health-audit.md` and evaluate its
   lightweight trigger threshold before selecting another ordinary Run. A trigger
   check is not the audit itself; do not create/dispatch the independent audit
   without the required Human approval;
8. recompute the runnable frontier before preparing a Run, surfacing a Human
   gate, or claiming a milestone.

Chat history may help orientation, but it must not be required to recover a
material decision, current blocker, dispatch route, or frontier.

The Human should not have to encode ordinary Harscode rules into the kickoff
prompt. In particular, do not require the Human to remind the Orchestrator to:

- use the project communication profile;
- facilitate a decision-ready Human question conversationally;
- reconcile a material post-approval Decision into the Techplan spine before
  dependent Build;
- show the Human-facing dispatch package;
- reconcile only affected task snapshots after a material parent revision.
- evaluate Loop Health trigger guidance when recent durable evidence shows repeated causal blocker/re-entry or routing-relevant recovery anomalies before proposing another ordinary cycle.

Those are Orchestrator responsibilities when the applicable current guidance
and durable evidence support them.

If the durable sources genuinely leave project/branch/work-context identity
ambiguous, ask the smallest clarifying question needed. Do not replace
reconstruction with a long checklist for the Human.



Use three operating layers:

```text
Project Bootstrap
→ one initial preparation of the durable orchestration foundation

New Slice / materially new work area
→ bounded readiness reconciliation against the existing foundation

Gap discovered during real work
→ just-in-time completion of the specific missing concern
```

### Slice readiness reconciliation

At the start of a new Slice or materially new work area, the Orchestrator should perform a lightweight bounded reconciliation rather than full re-bootstrap.

Check only concerns that could materially affect the Slice, such as:

- near-term objective/context;
- relevant authority ownership;
- whether existing Participant Profiles remain sufficient;
- newly required project/repository capability;
- runtime/model readiness when materially changed;
- Work Graph / durable-state discoverability.

Reuse existing bootstrap state and Profiles by default.

A new Slice does not by itself justify recreating Profiles, re-reading all project documentation, or rebuilding the orchestration foundation.

### Readiness evidence proportionality

Slice readiness reconciliation is required behavior, not a mandatory per-Slice
file.

Prefer existing durable owners for the result:

- Authority Map for current authority ownership;
- Participant Profile Registry/definitions for reusable execution capability;
- runtime/model configuration for runtime readiness;
- Work Graph and Work Unit current state for the current frontier;
- Events for material readiness decisions/transitions.

Create a dedicated readiness artifact only when it owns material transition
evidence that would otherwise be ambiguous or expensive to reconstruct, for
example a first-time bootstrap-to-Slice migration, a material foundation change,
or a bounded audit that needs one durable synthesis point.

When created, a readiness artifact is normally a **checkpoint/snapshot**, not a
live current-state projection. After its assessment is complete, do not keep
rewriting it merely to mirror later Runs, blockers, profile state, authority
state, or frontier changes. Point readers to the current owners instead.

A dedicated readiness artifact must not become a second Authority Map, Profile
Registry, Work Unit state record, Work Graph, or Control Surface.

### Just-in-time gap completion

During normal work, a missing capability, authority mapping, runtime prerequisite, or durable guidance gap may be discovered by the Orchestrator or surfaced by the Human.

Resolve only the specific proven gap.

Just-in-time completion is an exception/completion mechanism, not the normal pre-Run ritual. It should not make every Run re-prove project readiness.

Core rule:

> Profile suitability and orchestration readiness are invariants to preserve, not ceremonies to repeat before every Run.

## Post-bootstrap reconciliation

Bootstrap state is not immutable.

When material project conditions change, reconcile only the affected concern.

Examples:

- authority ownership changes;
- a new stack or repository is introduced;
- a new Participant capability is required;
- runtime/model availability changes;
- project structure changes materially.

Prefer targeted reconciliation over full re-bootstrap.

The normal lifecycle is:

```text
Initial Project Bootstrap
→ Normal Orchestration
→ bounded Slice readiness reconciliation when a new Slice/material work area begins
→ targeted just-in-time reconciliation only when real work exposes a gap
```

A full re-bootstrap is unnecessary unless the underlying project/orchestration identity materially changes.
