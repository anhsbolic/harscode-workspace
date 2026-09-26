# Pilot #2 Candidate — Orchestrator Operating Model

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group A checkpoint only. This document records CRTV design hypotheses and does not override `orchestration/protocol-v0.1.md`, canonical workflow guidance, or project authority.

## Purpose

Define the minimum operating boundary for a dedicated local Orchestrator in Pilot #2 without turning the Orchestrator into a hidden Planner, Implementer, Reviewer, or Verifier.

## Responsibility boundary

### Human Authority

Owns material authority and protected decisions, including Product, Design, security/privacy, protected-path authorization, and other explicitly Human-owned gates.

Human approval should remain a decision, not routine orchestration mechanics.

### Orchestrator

Owns coordination:

- reconstruct current orchestration state from durable artifacts;
- derive and maintain Work Units and their dependency graph;
- determine the runnable frontier;
- choose the next applicable workflow route;
- select the Participant execution profile allowed by Human-owned runtime configuration;
- prepare Run invocation and scoped context pointers;
- dispatch Participant Runs;
- reconcile Run outcomes into Work Unit state;
- register material Decisions, Blockers, and cross-Work-Unit Findings;
- evaluate Session continuation fitness when telemetry/evidence is available;
- surface Human gates;
- maintain the Human-facing Control Surface as a derived projection.

The Orchestrator may narrow and operationalize already-settled obligations. It must not silently invent new material requirements.

### Participant

Executes the assigned workflow Role and Run.

Participants produce Run-owned artifacts and evidence. They may recommend the next route, raise Findings, request Decisions, or report Blockers. They do not own project-wide routing or self-promote their Work Unit to a milestone/completion state.

## Orchestrator is not a super-agent

The Orchestrator must not replace:

- Explorer for Exploration;
- Planner for Techplan synthesis;
- Implementer for Build/Patch;
- Reviewer for independent Code Review;
- Verifier for independent Testing;
- Human Authority for material authority decisions.

Derived Human-facing workflow artifacts should be produced by the workflow participant that owns their source semantics, not silently authored by the Orchestrator.

For Pilot #2, make the ownership boundary explicit:

- `techplan.md` is Planner-owned;
- `report-techplan.md` is Planner-owned and is generated only when the current-effective Techplan reaches the Human approval gate after any invoked review/resolution path converges;
- Code Review verdict/evidence is Reviewer-owned;
- Testing verdict/evidence is Verifier-owned;
- the Orchestrator may dispatch, route, reconcile, and project these artifacts, but must not author them on behalf of the owning workflow Role.

## Downstream Work Unit decomposition

The Orchestrator owns orchestration decomposition after sufficient upstream evidence exists.

Exploration/Planning may discover capabilities, ownership boundaries, gaps, and rendezvous points. The Orchestrator translates that evidence into bounded Work Units, dependencies, completion conditions, and scheduling state.

A coordination-only split may be performed by the Orchestrator. A split that establishes or changes material Product/security/interface authority requires the corresponding Human Authority decision first.

## Invocation augmentation boundary

Invocation additions fall into three classes:

1. **Routing metadata** — Run ID, Role, Session posture, model/reasoning selection, working directory, artifact paths. Orchestrator-owned.
2. **Derived execution focus** — a narrow restatement of an already-settled obligation, with provenance to the source artifact. Orchestrator-owned.
3. **New substantive obligation** — a new requirement, risk, test obligation, or design assumption not already settled. Must not be injected silently; route it through the appropriate Finding/Planning/Authority mechanism.

## Dedicated local Orchestrator

Pilot #2 assumes one logical dedicated Orchestrator Participant.

A single Session is not required to live forever:

```text
Orchestrator Participant
├── Session A
└── Session B after A becomes DEGRADED/UNFIT
```

A replacement Session must reconstruct from durable orchestration state rather than chat memory.

## Pilot #2 execution hypothesis

Pilot #2 uses an **Automated Visible Fleet** execution style:

- Host OS: Ubuntu
- Terminal surface: Ghostty
- Harness: Codex CLI
- Human manually bootstraps the Orchestrator Session.
- The Orchestrator should prepare and, when safely possible, launch Participant CLI Sessions/Runs.
- Human per-Run terminal setup is fallback/diagnostic behavior, not the intended steady state.

These mechanics are Pilot #2 implementation choices, not orchestration semantics.

### Fire-and-forget Participant coordination

Pilot #2 intentionally keeps Participant supervision lightweight.

Normal dispatch posture:

```text
Orchestrator determines the Run
→ prepares durable invocation
→ launches a visible Ghostty + interactive Codex CLI Participant Session
→ confirms minimum successful dispatch
→ records last-known Run state as RUNNING
→ stops monitoring by default
```

Minimum successful dispatch means:

- the Ghostty/Codex Participant process or surface was launched;
- the durable Run invocation was delivered to the Participant;
- no immediate launch failure is known.

After successful dispatch:

- the Orchestrator MUST NOT continuously monitor, mirror, or poll the Participant transcript/progress as normal behavior;
- the Human acts as the lightweight problem/completion signal;
- if the Human reports no problem, orchestration retains the last-known `RUNNING` state rather than claiming guaranteed realtime liveness;
- if the Human reports a material problem, the Orchestrator diagnoses/routes only as much as needed;
- if the Human reports that the Participant finished, the Orchestrator reads the durable Run artifacts/handoff, reconciles Work Unit/Event/Control Surface state, and determines the next route;
- direct Human ↔ Participant interaction remains valid at genuine workflow Human gates.

This is deliberately not a monitoring daemon, transcript-mirroring system, or autonomous process supervisor.

### Human-facing continuation contract

At every meaningful coordination boundary, the Orchestrator must make continuation explicit rather than leaving the Human to infer the next step from raw state.

The Human-facing response should always make these three things discoverable:

1. **Current State** — the smallest current orchestration truth needed to understand where the work stands;
2. **Next Action** — the next coordination action implied by the current durable state and workflow;
3. **Decision / Action By Human** — the smallest concrete Human decision or action required now, or `None` when no Human action is needed.

Rules:

- do not stop at labels such as `WAITING_HUMAN`, `BLOCKED`, or `RUNNING` without explaining the continuation consequence;
- if a Human decision is required, state the concrete choice/action and what the Orchestrator will do after it;
- if no Human decision is required, state `Decision / Action By Human: None` and continue owning routine coordination;
- after a fire-and-forget dispatch, make clear that the next Human interaction is only to report a material problem or Participant completion;
- after a completion signal and reconciliation, state the newly computed next route and surface any new Human gate immediately;
- do not turn this response contract into a duplicate Control Surface or verbose status report; keep it concise and current.

Example:

```text
Current State
WU-S2-002 is waiting at the Techplan review-route gate.

Next Action
Choose the review route for the current-effective Techplan.

Decision / Action By Human
Choose one:
- independent Techplan review
- direct Human review

After the choice, the Orchestrator will prepare the applicable next Run/gate.
```

### Pilot #2 visible-launch recovery posture

The normal Pilot #2 Participant path is visible Ghostty + interactive Codex CLI. A background/non-visible launcher is not an equivalent silent fallback.

When GUI or Codex runtime-local access is blocked by the outer sandbox/environment:

1. verify that the visible launch remains the intended path;
2. request the narrow managed escalation/capability needed;
3. retry the same visible launcher path;
4. if visible dispatch still cannot be established, record a Pilot deviation and stop/reroute rather than silently substituting background execution.

Process/session existence alone is not proof of visual visibility. Use direct window/screenshot evidence when available; otherwise record the limitation truthfully.

Changing terminal, harness, or model in a later pilot must not require changing Work Unit, Run, Decision, dependency, or authority semantics.

## Pilot #2 success signal

The operating model is healthier than Pilot #1 when:

- Human no longer acts as the normal per-Run prompt composer and session launcher;
- participant execution remains role-isolated;
- Human interaction focuses on genuine decisions/corrections;
- a fresh Orchestrator Session can resume from durable artifacts;
- failure of a terminal tab does not destroy orchestration truth.
