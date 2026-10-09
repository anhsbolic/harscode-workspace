# Orchestrator Kickoff Contract

> Status: Pilot Candidate
> Scope: Human-facing start / resume / transition intent for an Orchestrator Session. This contract does not replace project authority, workflow phase authority, or `protocol-v0.1.md`.

## Purpose

Allow the Human to express a natural intent without having to restate Harscode mechanics.

Examples of sufficient intent:

```text
"Continue from current durable state."

"The pre-engineering work for this commitment is ready. I want to continue into engineering. Prepare it."

"We finished planning for this bounded work. Prepare the next engineering step."
```

The Human kickoff message is intent, not the orchestration specification.

Core sequence:

```text
Human intent
→ read-only Orchestrator preflight
→ reconstruct + verify + validate
→ recommend the concrete next action
→ Human confirms
→ only then persist/prepare/dispatch the authorized action
```

## Preflight boundary

For a fresh Orchestrator start, resume, or material work/phase transition, the first response to Human intent is a **preflight**, not execution authorization.

During preflight, the Orchestrator should use the smallest applicable durable context to reconstruct and verify:

- target project / repository and current working context;
- current Harscode orchestration/workflow guidance;
- the near-term objective or bounded commitment implied by durable project state;
- current-effective upstream authority / handoff / workflow artifacts relevant to that objective;
- applicable project write/protected boundaries;
- existing orchestration state, if any;
- runtime/model readiness from Human-owned runtime configuration;
- material dependencies, blockers, approvals, or prerequisites that constrain the next action;
- whether the correct posture is initial bootstrap, bounded readiness reconciliation, existing-state resume, or another current route.

Use `pilot-2-candidate/project-orchestration-bootstrap.md` when initial or bounded bootstrap/readiness semantics are needed. Do not turn every kickoff into a full project bootstrap.

### Read-only by default

Before Human confirmation of the recommended next action, the Orchestrator MUST NOT:

- dispatch a Participant;
- begin a workflow phase;
- create or activate a new Run as authorized execution;
- create implementation changes;
- mutate Product / Design / Security / project-domain authority;
- perform deterministic reconciliation merely to make the proposed route look ready;
- create speculative Work Units, Work Graph detail, profiles, dashboards, or other scaffolding whose need has not yet been validated.

If the preflight discovers stale, conflicting, missing, or unsafe state, report it and route the smallest resolution. Do not silently repair it before the Human has seen the result.

Reading repository state, current guidance, runtime configuration, and existing durable artifacts is expected during preflight.

## Readiness result

The preflight should end with a compact Human-facing result containing:

- **Intent understood** — the bounded outcome / transition the Orchestrator believes the Human requested;
- **Verified baseline** — the material project, authority, workflow, runtime, and orchestration facts actually established;
- **Readiness verdict** — `READY`, `NOT_READY`, or a similarly precise plain-language result with the blocking reason;
- **Material findings** — only findings that affect the requested transition or its safety/correctness;
- **Recommended next action** — one concrete next step when evidence is sufficient;
- **Proposed orchestration delta** — the minimum Work Unit / Run / Role / Session / model posture that would be created or changed if approved, without speculative future topology;
- **Human decision** — the exact approval or decision required next.

Do not make the Human rediscover file paths, workflow phases, model choices, or routing mechanics that the Orchestrator can determine from durable evidence.

## Confirmation gate

A readiness result is a recommendation, not permission to execute.

For a fresh start or material transition, stop after the preflight and ask the Human to confirm the recommended next action.

Natural Human approval is sufficient when unambiguous; no fixed approval keyword is required.

After confirmation, the Orchestrator may:

1. persist only the minimum durable orchestration state required by the approved action;
2. create/prepare the applicable Work Unit / Run / Invocation when justified;
3. resolve the dispatch package under `run-contract.md`;
4. present the complete Human-Assisted dispatch package;
5. wait for the Human to perform the mechanical Participant dispatch when that posture applies.

If new material evidence appears between preflight and preparation, stop and reconcile the recommendation instead of treating the earlier confirmation as blanket authorization.

This kickoff confirmation gate does not replace later workflow-specific Human gates. It also should not become a ceremony repeated before every ordinary Run once the Human has already authorized the bounded next action, unless materially new evidence changes the route or authority boundary.

## Authority discipline

The Orchestrator verifies and routes authority; it does not gain authorship over it.

If a pre-engineering or other upstream handoff is current-effective, consume it as input. If engineering readiness validation exposes a material upstream semantic gap, route that gap back to the applicable owner instead of rewriting upstream authority from orchestration/engineering authority.

Project-specific authority and write boundaries remain owned by the target project.
