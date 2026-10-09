# Pre-Engineering → Engineering Transition Kickoff

> Status: Pilot Candidate
> Scope: Orchestrator handling of a Human intent to move one bounded commitment from completed / ready pre-engineering into engineering preparation.
> This contract does not apply to generic Orchestrator start/resume, later engineering phase transitions, or unrelated work intents.

## Human intent

The Human should be able to state the transition naturally without restating Harscode mechanics.

Example:

```text
"The pre-engineering work for C1 is ready. I want to continue into engineering. Prepare it."
```

This message expresses **transition intent only**. It is not permission to start engineering execution and it is not a substitute for durable project authority.

## Required Orchestrator behavior

On this intent, the Orchestrator first performs a **read-only transition preflight**.

Use the smallest applicable durable context to reconstruct, verify, and validate:

- target project / repository and current working context;
- the bounded commitment the Human is referring to;
- current pre-engineering completion / handoff evidence;
- current-effective product / commitment-scoped behavior / requirements authority;
- the applicable engineering write/protected boundaries;
- the current Harscode orchestration and engineering workflow guidance;
- runtime/model readiness from Human-owned runtime configuration;
- existing orchestration state relevant to this commitment, if any;
- material blockers, unresolved authority gaps, or prerequisites that would make the transition unsafe or premature;
- the correct first engineering route for the commitment from current durable guidance.

Do not require the Human to restate information that is discoverable from the target repository and current Harscode guidance.

If a runtime/config path points to a pre-engineering artifact directory, use it only for discovery/navigation. It does not establish authority, active scope, read order, or permission to mutate those artifacts.

## Preflight boundary

Until the Human confirms the recommended engineering transition, the Orchestrator MUST NOT:

- dispatch a Participant;
- begin Exploration or any other engineering workflow phase;
- create or activate a new Run as authorized execution;
- make implementation changes;
- modify upstream Product / pre-engineering semantic artifacts;
- perform deterministic reconciliation merely to make the transition appear ready;
- create speculative Work Units, Work Graph detail, profiles, dashboards, or future execution topology.

If verification finds stale, missing, conflicting, or unsafe state, surface the smallest concrete issue and its owner. Do not silently repair upstream authority or continue as though readiness were established.

## Readiness result

The preflight response should be compact and decision-ready.

It should state:

- **Intent understood** — the bounded commitment and requested transition;
- **Verified pre-engineering baseline** — the current handoff / binding authority / completion facts actually established;
- **Verified engineering boundary** — the write/protected boundaries and applicable workflow entrypoint;
- **Runtime readiness** — the execution/runtime facts needed for the first engineering step;
- **Readiness verdict** — `READY` or `NOT_READY`, with the blocking reason when not ready;
- **Material findings** — only findings that affect this transition;
- **Recommended next action** — normally the first justified engineering route when readiness is established;
- **Proposed orchestration delta** — the minimum Work Unit / Run / Role / Session / model posture that would be prepared if approved;
- **Human decision** — the exact approval required to prepare the first engineering action.

## Human confirmation gate

A `READY` verdict is a recommendation, not execution authorization.

Stop after the preflight and ask the Human to confirm the recommended transition.

Natural Human approval is sufficient when unambiguous; no fixed approval keyword is required.

Only after confirmation may the Orchestrator:

1. persist the minimum durable orchestration state required for the approved engineering transition;
2. create/prepare the justified first Work Unit / Run / Invocation;
3. resolve the dispatch package under `run-contract.md`;
4. present the complete Human-Assisted dispatch package;
5. wait for the Human to perform the mechanical Participant dispatch when that posture applies.

If materially new evidence appears between preflight and preparation, stop and revalidate instead of treating the earlier confirmation as blanket authorization.

## Authority discipline

The transition consumes upstream handoff/authority; it does not grant engineering or orchestration permission to rewrite that authority.

If readiness validation exposes a material Product or pre-engineering semantic gap:

```text
preserve evidence
→ surface Finding / Decision / Blocker as applicable
→ route to the upstream owner
→ do not repair the semantic artifact from engineering/orchestration authority
```

Project-specific authority and write boundaries remain owned by the target project.
