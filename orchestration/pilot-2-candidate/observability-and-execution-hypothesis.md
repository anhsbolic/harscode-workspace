# Pilot #2 Candidate — Observability & Execution Hypothesis

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group A checkpoint only. This document captures the minimum CRTV observability and local execution hypothesis for Pilot #2.

## Execution hypothesis

Pilot #2 intentionally uses a specific, simple implementation:

- Ubuntu
- Ghostty
- Codex CLI
- Automated Visible Fleet

The Orchestrator should prepare Run identity, model/reasoning choice, scoped invocation, working directory, and authorization envelope before launch.

The intended experience is:

```text
Human starts Orchestrator once
→ Orchestrator determines runnable work
→ Orchestrator prepares/launches visible Participant CLI Run
→ Participant executes workflow
→ durable Run artifacts are produced
→ Orchestrator reconciles result
→ Human is involved only for real gates/corrections or launcher fallback
```

Pilot success does not require perfect terminal automation. Occasional manual recovery is acceptable. Routine Human per-Run setup is not the intended steady state.

Ghostty/tab state is never orchestration authority.

## Why visible execution for Pilot #2

Pilot #2 still performs CRTV of Harscode itself.

Visible Participant sessions provide a cheap debugging surface for:

- over-reading/repetitive source loading;
- permission friction;
- agent stalls/loops;
- verification ritual;
- unexpected context loss;
- invocation misunderstanding.

This is a pilot/debugging advantage, not a claim that visible terminals are the mature execution architecture.

## Observability principle

> Observe enough to explain execution quality, not enough to reconstruct every thought.

Pilot #2 should avoid building a full telemetry platform.

## Minimum signal classes

### 1. Run identity and lifecycle

Capture when exposed/available:

- Run ID;
- Work Unit ID;
- phase/Role;
- Participant;
- Session identity;
- model and reasoning effort;
- target/workflow revision;
- start/end;
- terminal result such as completed, failed, waiting-human, abandoned.

A terminal tab being open is not lifecycle state.

### 2. Retrieval/read signals

Capture enough to identify retrieval behavior:

- path/source;
- context class when known: Required, Routing, Conditional, Cold;
- trigger/reason when useful;
- repeated-read candidate.

Do not copy full file contents into telemetry.

Do not classify over-reading from a fixed count alone.

Suspicion should consider:

```text
relevance
+ repeated source/region
+ lack of material state change
+ lack of a new check/decision trigger
+ execution cost/consequence
```

Broad reading that violates progressive-disclosure routing is stronger evidence than merely reopening an important file.

### 3. Command and verification signals

For meaningful commands, capture:

- command;
- purpose;
- source obligation/risk when non-trivial;
- authorization class;
- result;
- duration when useful.

Non-trivial verification should be traceable to a real risk/contract/test-focus obligation.

Example:

```text
go test -race ...
purpose: shared-state verification
source: approved Techplan risk/test focus
```

A heavyweight command whose justification is only “extra confidence” is a CRTV signal worth reviewing.

### 4. Permission/intervention signals

Record material permission requests and disposition:

- requested action;
- why permission was requested;
- approved/denied/escalated;
- whether the action should already have been inside the Run authorization envelope.

This allows Pilot #2 to distinguish legitimate Human gates from avoidable harness friction.

### 5. Context/session fitness signals

Use available quantitative context data only as signals, never as fixed policy.

Useful signals may include:

- context/token utilization if exposed;
- compaction/reset;
- repeated rereads;
- accumulated dead ends;
- inability to identify current authority cleanly;
- references to superseded state.

Session fitness remains semantic:

```text
HEALTHY | DEGRADED | UNFIT
```

No rule such as “80% context means fresh session” should be introduced.

### 6. Run outcome

Every meaningful Run handoff should retain:

- artifacts;
- findings;
- blockers;
- Decision requests;
- next-route recommendation;
- Session transition recommendation where applicable.

The Orchestrator owns the coordination consequence.

## Telemetry locality

Detailed execution telemetry should live with the Run, conceptually:

```text
runs/<RUN-ID>/
├── invocation.md
├── telemetry.*
└── report / workflow-owned artifacts
```

Only material coordination consequences are promoted into the global Event log.

## Permission hypothesis

A Run invocation may eventually carry an explicit execution envelope, distinguishing:

- required/pre-authorized routine project commands;
- ordinary scoped diagnostics/tests;
- actions that still require Human/protected authorization.

Pilot #2 should first observe where permission friction occurs before creating a broad permanent permission policy.

## Orchestrator intervention posture

Do not turn the Orchestrator into a realtime efficiency policeman.

Default:

```text
observe
→ record
→ review at Run boundary
```

Interrupt during execution only for materially harmful behavior such as:

- destructive/protected action;
- authority violation;
- obvious infinite/stalled loop;
- runaway expensive verification;
- genuine security/permission boundary.

## Explicit non-goals

Pilot #2 does not need to record:

- private chain-of-thought;
- every token/message;
- every keystroke or mouse action;
- full terminal video;
- every line read;
- full stdout for every command;
- an artificial “agent efficiency score”.

## Candidate CRTV measures

Prefer raw signals over synthetic scores:

- Run duration;
- unique sources read;
- total read events;
- repeated-read candidates;
- commands executed;
- non-trivial verification commands and their justification;
- permission requests;
- avoidable-permission candidates;
- context/compaction signals when exposed;
- continuation-fitness result.

These are diagnostic evidence, not pass/fail thresholds.
