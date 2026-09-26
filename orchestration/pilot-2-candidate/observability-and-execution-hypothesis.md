# Pilot #2 Candidate — Observability & Execution Hypothesis

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group A checkpoint only. This document captures the minimum CRTV observability and local execution hypothesis for Pilot #2.

## Execution hypothesis

Pilot #2 intentionally uses **Human-Assisted Orchestration**.

The Orchestrator prepares the coordination decision and dispatch package; the Human performs the mechanical Participant launch/prompt delivery.

The intended experience is:

```text
Human starts Orchestrator
→ Orchestrator reconstructs state and determines runnable work
→ Orchestrator prepares Run identity, model/effort, Session posture, invocation, and Human dispatch instructions
→ Human opens the requested Participant Session and delivers the invocation/prompt
→ Participant executes independently
→ Human reports only a material problem, genuine workflow gate, or completion
→ durable Run artifacts are produced
→ Orchestrator reconciles result and states the next route
```

Pilot #2 success does not depend on terminal spawning, prompt injection, CUA/native-window observability, process supervision, or other Automated Visible Fleet mechanics.

Those mechanics are deferred for dedicated research after Pilot #2 and before Pilot #3.

Terminal/window state is never orchestration authority.

## Human-assisted execution rationale

Pilot #2 still performs CRTV of Harscode itself, but the evidence priority is orchestration correctness.

Manual Participant launch/prompt delivery is acceptable when it preserves these boundaries:

- Orchestrator chooses and prepares the Run;
- Human performs only the mechanical dispatch requested;
- Participant owns phase execution/artifacts;
- Human reports problems/completion;
- Orchestrator owns reconciliation and next routing.

Visible terminals may still be useful for Human debugging, but their automation is not a Pilot #2 requirement.

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

Do not turn the Orchestrator into a realtime efficiency policeman or process supervisor.

Pilot #2 default after Human-assisted dispatch is **fire-and-forget**:

```text
Orchestrator prepares dispatch
→ Human launches Participant and delivers invocation
→ Human confirms dispatch when useful
→ retain last-known active state
→ no realtime transcript/progress polling
→ Human reports problem or completion
→ reconcile from durable artifacts/handoff
```

The Human is the lightweight liveness/problem/completion signal for this pilot. Silence from the Human means only that no problem has been reported; it does not prove current process liveness.

Do not continuously read Participant transcripts, mirror Participant reasoning, or poll Session state merely to report progress. Live inspection is diagnostic-only and should have a concrete trigger such as:

- Human reports a problem or asks for investigation;
- an immediate launch failure is suspected;
- an expected durable signal is missing after a completion claim;
- a genuine permission/security boundary requires diagnosis.

If direct evidence suggests materially harmful behavior such as destructive/protected action or authority violation, intervene through the applicable Human/protected path. Pilot #2 does not require autonomous detection of every stall, loop, or inefficient verification pattern.

### Mechanical dispatch evidence

For Human-assisted dispatch, the minimum useful evidence is that:

- the Human received the Run dispatch instructions;
- the invocation/prompt was delivered to the intended Participant Session;
- no immediate blocking problem was reported.

Do not require automated window/process telemetry merely to treat the Run as dispatched.

If the Human reports that launch or invocation delivery failed, record the real mechanical blocker and provide a corrected dispatch instruction. Do not turn the failure into a broad orchestration redesign during Pilot #2.

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
