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

## Pilot #2 execution posture

Pilot #2 now uses **Human-Assisted Orchestration**.

The primary goal of this pilot is orchestration correctness, not fleet/window automation.

Current operating model:

```text
Orchestrator decides and prepares
→ Human performs the mechanical Participant dispatch
→ Participant executes the assigned Run
→ Human reports a material problem or completion
→ Orchestrator reconciles durable artifacts and determines the next route
```

The Orchestrator still owns coordination. Human involvement is intentionally limited to mechanical execution and genuine authority/workflow gates.

For each Participant Run, the Orchestrator must provide enough concrete dispatch detail that the Human does not have to reconstruct the workflow:

- Role / Participant type;
- model and reasoning effort;
- target working directory when relevant;
- durable invocation path or exact minimal kickoff prompt;
- any required Session posture such as fresh vs continuation;
- what the Human should report back when the Participant blocks or completes.

The Human may open the requested terminal/session, select the requested model/effort, paste the Orchestrator-provided invocation pointer/prompt, and interact directly at genuine workflow Human gates. The Human should not invent the workflow route, compose a replacement task, or decide the next Run on behalf of the Orchestrator.

After dispatch, supervision remains lightweight:

- the Orchestrator MUST NOT continuously monitor, mirror, or poll the Participant transcript/progress as normal behavior;
- if the Human reports no problem, orchestration retains the last-known active state rather than claiming guaranteed realtime liveness;
- if the Human reports a material problem, the Orchestrator diagnoses/routes only as much as needed;
- if the Human reports that the Participant finished, the Orchestrator reads the durable Run artifacts/handoff, reconciles Work Unit/Event/Control Surface state, and determines the next route.

Direct Human ↔ Participant interaction remains valid at genuine workflow Human gates.

### Automated Visible Fleet hold

Automated Visible Fleet is **on hold for the remainder of Pilot #2**.

Ghostty/Codex spawning, prompt injection, native-window visibility, process supervision, split/tab/window control, and runtime-local permission mechanics are not Pilot #2 success criteria.

Do not spend Pilot #2 delivery effort building or debugging terminal/fleet automation unless a narrow diagnostic is required to unblock the Human-assisted path.

The observations already gathered remain CRTV evidence, but automation mechanics should be researched separately after Pilot #2 and before Pilot #3.

These mechanics are implementation choices, not orchestration semantics.

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

### Pilot #2 mechanical-dispatch boundary

The Orchestrator must treat Human-assisted dispatch as a deliberate Pilot #2 operating mode, not as a workflow failure.

A healthy handoff to Human should look like:

```text
Next Action
Run <RUN_ID> with <Role>.

Decision / Action By Human
1. Open a fresh/continuation Participant Session as instructed.
2. Use model <MODEL> with reasoning <EFFORT>.
3. Use working directory <PATH> when applicable.
4. Paste/run the provided invocation pointer or minimal kickoff prompt.
5. Report a material problem or completion back to the Orchestrator.
```

The Orchestrator should not ask the Human to rediscover canonical prompts, infer artifact paths, choose models, or decide routing mechanics that are already Orchestrator-owned.

Changing terminal, harness, or model in a later pilot must not require changing Work Unit, Run, Decision, dependency, or authority semantics.

## Pilot #2 success signal

Pilot #2 succeeds when orchestration correctness is demonstrated across real work:

- a fresh Orchestrator Session can resume from durable artifacts;
- Work Unit decomposition and dependency topology remain evidence-based;
- runnable frontier and workflow routing are correct;
- Role/Participant boundaries remain isolated;
- model/reasoning routing is explicit and justified;
- Human gates are surfaced correctly;
- workflow artifact ownership remains correct;
- Participant completion is reconciled correctly into Work Unit state, Events, Work Graph, and Control Surface;
- Decisions/Blockers/Findings are routed without inventing authority;
- milestones are not promoted prematurely;
- Human-assisted dispatch remains mechanical rather than turning the Human into the real Orchestrator.

Automated fleet/window mechanics are explicitly deferred from Pilot #2 success criteria.
