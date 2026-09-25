# Pilot #2 Candidate — Consolidated Pilot #1 Review & Change Map

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: consolidated CRTV checkpoint covering Groups A–F plus confirmed Pilot #1 defects.

## Purpose

Separate proven Harscode changes from Pilot #2 hypotheses so the next pilot starts from a clean, intentional baseline.

Classification:

- **KEEP** — current Harscode behavior/guidance is materially healthy; preserve it.
- **CANONICAL_CHANGE** — a proven defect/structural gap should be corrected before or as part of Pilot #2 preparation.
- **PILOT_2_CANDIDATE** — a plausible design hypothesis should be validated through Pilot #2 before promotion.
- **DEFER** — insufficient evidence or unnecessary scope for the next pilot.

## Executive view

Pilot #1 broadly validated the Harscode phase model, authority separation, independent Review/Testing, contract-parallel delivery, proportional re-entry, and current model-selection philosophy.

The largest proven weaknesses were not in engineering-phase semantics themselves. They were in:

- current-state representation and projection drift;
- Human Techplan report timing/ownership inconsistency;
- best-practice authority/example contamination;
- missing executable Orchestrator operating contract and Work Graph semantics;
- missing generalized phase-applicability ownership;
- missing Run execution authorization envelope;
- insufficient durable observability/recovery for a dedicated Orchestrator.

Pilot #2 should therefore validate **orchestration execution**, not redesign the engineering workflow from scratch.

---

## Group A — Orchestrator Architecture, State, Artifacts, Observability

### KEEP

- Core protocol distinction: Work Unit != Run != Participant != Session.
- Human Authority remains separate from Orchestration Operator and execution Roles.
- Control Surface remains a derived projection, never source of truth.
- Decisions remain distinct from Work Units.
- Project Learning remains evidence, not authority.
- Progressive disclosure and durable state over chat memory.

### CANONICAL_CHANGE

#### A-C1 — Unambiguous current orchestration state

Confirmed Pilot #1 defect: Work Unit manifests and Control Surface contained contradictory historical/current state.

Canonical direction:

~~~text
Work Unit Definition
+ one mutable Current State
+ append-only material Event History
+ derived Control Surface
~~~

Current State values must be replacement semantics, not append-based chronology.

Cross-Work-Unit dependency topology should have one canonical owner: the Work Graph.

#### A-C2 — Human Techplan report timing and ownership

Confirmed contradiction:

- Techplan rules/template/synthesis say generate the Human report after review/resolution converges and **before** Human approval;
- Techplan guardrails §8 says only after Approval.

Canonical correction:

- current-effective Techplan converges;
- Planner/appropriate planning participant generates the derived Human report;
- Human approves/rejects/revises the Techplan, not a separate report authority object;
- material Techplan revision regenerates the report;
- report never overrides Techplan.

#### A-C3 — Best-practice authority/example contamination

Confirmed documentation defect: reusable Go testing guidance includes historical Kencleng example material inside principle-authority files.

Canonical correction:

- principle files contain reusable guidance only;
- historical task stories move to cold examples/history;
- examples calibrate but do not become required runtime authority.

### PILOT_2_CANDIDATE

- Dedicated local Orchestrator Participant with replaceable Sessions.
- Parent Outcome → Work Graph → Work Unit Definition/Current State → Events → Runs → Control Surface.
- Dynamic Work Graph owned by Orchestrator.
- Orchestrator-generated invocation as dispatch artifact, not authority.
- Invocation augmentation classes: routing metadata, derived focus, new substantive obligation.
- Automated Visible Fleet on Ubuntu + Ghostty + Codex CLI as Pilot #2 mechanics.
- Minimal Run telemetry: lifecycle, retrieval, command/verification, permission, session-fitness, outcome.

### DEFER

- state database;
- orchestration schema engine;
- queue framework;
- generic multi-harness launcher/adapter;
- continuous terminal supervision;
- synthetic orchestration efficiency score.

---

## Group B — Workflow Topology & Applicability

### KEEP

- Techplan decomposition is already correctly optional and post-Approval.
- Build owns production fixes even when Review/Testing discovers the defect.
- Code Review and Testing are distinct independent concerns.
- Proportional patch re-entry is already present in Build/Testing guidance.
- repeated unresolved cause → STALLED.

### CANONICAL_CHANGE

#### B-C1 — Generalized phase-applicability ownership

Current workflow has conditional gates for some phases but no general orchestration rule for applicability.

Canonical direction:

- conservative default lifecycle remains;
- concrete applicability resolved just-in-time by Orchestrator;
- Participant may recommend but may not self-waive independent phases;
- concrete resolution is REQUIRED or NOT_APPLICABLE;
- NOT_APPLICABLE requires explicit workflow-grounded rationale;
- uncertainty resolves conservatively toward the independent phase.

#### B-C2 — Distinguish orchestration decomposition from Techplan decomposition

Make explicit:

~~~text
Parent Outcome → Work Units
= Orchestrator-owned coordination decomposition

Approved Techplan → executable task slices
= optional planning decomposition
~~~

The absence of Techplan decomposition in Pilot #1 was not itself a defect.

### PILOT_2_CANDIDATE

- just-in-time phase applicability at each frontier;
- classify loop causes: IMPLEMENTATION_DEFECT / EVIDENCE_GAP / PLAN_GAP / AUTHORITY_GAP / ENVIRONMENT_GAP;
- use loop cause, not raw loop count, for CRTV diagnosis;
- treat Testing's whole-Techplan reread as a validation-era conservative rule to reevaluate with Pilot #2 evidence.

### DEFER

- giant phase × Work Unit × risk applicability matrix;
- fixed numeric loop-count threshold.

---

## Group C — Verification Strategy & Permissions

### KEEP

- Techplan Rule → evidence → owner → why/risk-if-skipped structure.
- Build = focused edit-loop confidence.
- Testing = independent final/specialized evidence.
- Human-owned evidence stays Human-owned.
- specialized verification requires real risk/contract rationale.
- tool name is not authority.
- Codex sandbox/approval is translation, not policy.

### CANONICAL_CHANGE

#### C-C1 — Run execution authorization envelope

Current permission guidance is healthy but not integrated into Orchestrated Run dispatch.

Canonical direction:

Each Run can carry a lightweight semantic envelope containing:

- authorized write scope;
- routine capability classes;
- known required repo commands;
- already-justified specialized verification;
- Orchestrator-routed scope expansion;
- Human-required/protected boundaries.

Candidate classes:

~~~text
PREAUTHORIZED
ORCHESTRATOR_DECISION
HUMAN_REQUIRED
~~~

The Human should not be the routine shell permission broker.

### PILOT_2_CANDIDATE

- trace meaningful verification commands to Rule/Risk/Test Focus/repo requirement/current finding;
- permission telemetry distinguishes avoidable prompts from expected Human gates;
- broader verification expansion can route to Orchestrator when authority remains settled.

### DEFER

- permission DSL;
- exhaustive command whitelist;
- generic authorization engine;
- verification-specific ID system beyond existing Rule/Risk/Test-Focus identifiers.

---

## Group D — Parallelism & Rendezvous

### KEEP

- Kencleng integration-map principle: decomposition is local, contracts are shared.
- frontend contract-faithful MSW/network-boundary mocking pattern.
- separate Backend, Frontend, Topology, Integration milestones.
- Integration cannot substitute for missing local verification.

### CANONICAL_CHANGE

#### D-C1 — Explicit rendezvous/runnable-frontier semantics

Canonical orchestration should state:

- Work Units wait only on HARD dependency conditions;
- sibling unfinished != blocked;
- integration becomes runnable from earned milestones, not branch/process presence;
- dependency strength follows evidence required for the Work Unit's own completion condition.

#### D-C2 — Separate semantic parallelism from execution concurrency

Multiple WUs may be READY while local scheduler serializes actual Runs for workspace/runtime safety.

~~~text
READY
!= automatically RUNNING
~~~

This should be explicit before Automated Visible Fleet can create real same-repo concurrent mutation.

### PILOT_2_CANDIDATE

- contract-faithful substitute boundaries as generic scheduling-decoupling mechanism;
- dependency-scoped evidence invalidation after material shared-contract change;
- scheduler may serialize semantically parallel Runs until workspace-isolation evidence justifies more concurrency.

### DEFER

- generic git-worktree strategy;
- branch-per-Run architecture;
- mandatory stack-based parallelism.

---

## Group E — Session Fitness, Recovery & Observability

### KEEP

- continuation fitness instead of fixed context threshold;
- fresh Review/Testing for independence;
- durable artifacts over chat memory;
- benchmark usage as evidence, not workflow authority;
- rescue-prompt concept.

### CANONICAL_CHANGE

#### E-C1 — Session fitness ownership

Participant may report local Session signals; Orchestrator owns continuation routing and Session fitness classification.

Candidate fitness:

~~~text
HEALTHY
DEGRADED
UNFIT
~~~

#### E-C2 — Mid-Run reconstruction checkpoint

A fresh Session inside the same Run needs sufficient durable continuation state when normal phase handoff is not yet available.

Minimum information:

- Run identity/purpose;
- current stage;
- current-effective artifacts;
- settled relevant findings/decisions;
- blockers/open questions;
- relevant source anchors;
- next action.

Checkpointing is event-driven, not periodic ceremony.

#### E-C3 — Orchestrator self-recovery

A fresh Orchestrator Session must reconstruct progressively from durable orchestration state without a large Human-authored handover.

Preferred bootstrap:

~~~text
Parent Outcome
→ Work Graph
→ current WU states
→ open Decisions/Blockers
→ active Run checkpoints
→ recent Events only when needed
~~~

### PILOT_2_CANDIDATE

- explicit transition reasons: INDEPENDENCE / CONTEXT_HYGIENE / HARNESS_RECOVERY / HUMAN_REDIRECTION;
- over-reading diagnosis from relevance + repetition + consequence, not count;
- terminal/process references as operational handles only;
- deliberate fresh-Orchestrator recovery test;
- Human should stop being normal Session-transition operator.

### DEFER

- heartbeat daemon;
- terminal/process supervisor;
- continuous screen capture;
- fixed time/context/read thresholds.

---

## Group F — Model Routing

### KEEP

- Human-owned, Orchestrator-read-only model registry.
- least-cost sufficiently capable model.
- lowest sufficient supported reasoning effort.
- gated model requires explicit Human approval.
- pairing model separated from Participant Run model.
- model names remain runtime configuration, not Harscode semantics.

### CANONICAL_CHANGE

#### F-C1 — Short model-routing rationale

Orchestrated Run dispatch should preserve a concise rationale:

- selected model;
- reasoning effort;
- minimum capability need;
- why sufficient;
- approval reference when required.

#### F-C2 — Diagnose before escalation

Before stronger-model escalation, classify whether the failure is actually:

- capability insufficiency;
- missing context;
- workflow/routing gap;
- authority gap;
- environment/harness gap.

Stronger models must not mask system defects.

#### F-C3 — Non-sticky Run-scoped escalation

Approval/escalation is scoped to the concrete Run unless Human policy says otherwise.

Future Runs return to normal fit-for-purpose selection.

### PILOT_2_CANDIDATE

- selectively route genuinely routine Runs to lower-cost models;
- collect routing outcome evidence before expanding capability taxonomy.

### DEFER

- numeric model capability scoring;
- model rankings;
- phase-specific mandatory model mapping;
- automatic strongest-model fallback.

---

## Proven defects that should be fixed before Pilot #2 execution

These are the highest-confidence preconditions.

### P0-1 — Techplan Human-report timing contradiction

Fix protected Techplan guidance through the proposal mechanism so report timing and ownership are unambiguous.

### P0-2 — Current-state / projection drift model

Promote a canonical representation that separates Work Unit Definition, Current State, Event History, and derived Control Surface.

Pilot #2 should not start using the old append-based state pattern as its durable foundation.

### P0-3 — Best-practice authority/example contamination

Clean reusable Go testing authority so historical Kencleng stories no longer live inside principle files.

### P0-4 — Orchestrated Run contract lacks execution envelope/model rationale/session-recovery hooks

Extend the orchestrated Run contract or adjacent canonical orchestration guidance just enough to carry the new semantics needed by Pilot #2.

Do not implement a large runtime framework.

## Changes that can be validated during Pilot #2 instead of fully canonicalized first

- exact Work Graph file shape;
- exact Work Unit Current State file syntax;
- exact Event record shape;
- exact telemetry serialization;
- exact Automated Visible Fleet launcher mechanics;
- exact session/process detection mechanics;
- exact permission-envelope translation into Codex flags/config;
- lower-cost model routing heuristics;
- same-repo concurrency/worktree strategy.

These should remain candidate mechanics until real execution proves what is necessary.

## Recommended pre-Pilot #2 sequencing

~~~text
1. Fix confirmed documentation contradictions/contamination
2. Promote minimum orchestration semantic changes required for Pilot #2
3. Keep storage/launcher/telemetry mechanics as candidate/simple files
4. Re-verify current Codex model/runtime capabilities
5. Prepare Slice 2 Harscode Space using the candidate artifact model
6. Launch dedicated Orchestrator
7. Validate through real Slice 2 delivery
~~~

## Promotion discipline

Do not promote every candidate document wholesale into canonical Harscode.

For each candidate concept:

~~~text
Pilot evidence
→ contradiction/friction/benefit assessment
→ smallest reusable rule
→ proposal/Human review where required
→ canonical promotion
~~~

Pilot #2 is successful even if some candidate concepts are rejected, simplified, or remain project-local.

## Consolidated Pilot #2 hypothesis

> A dedicated local Orchestrator can coordinate Slice 2 from durable Work Graph/state artifacts, dispatch visible Codex CLI Participant Runs with scoped context/authorization/model routing, preserve independent engineering workflow quality, and materially reduce Human prompt/session-launch toil without introducing a heavyweight orchestration platform.
