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

Changing terminal, harness, or model in a later pilot must not require changing Work Unit, Run, Decision, dependency, or authority semantics.

## Pilot #2 success signal

The operating model is healthier than Pilot #1 when:

- Human no longer acts as the normal per-Run prompt composer and session launcher;
- participant execution remains role-isolated;
- Human interaction focuses on genuine decisions/corrections;
- a fresh Orchestrator Session can resume from durable artifacts;
- failure of a terminal tab does not destroy orchestration truth.
