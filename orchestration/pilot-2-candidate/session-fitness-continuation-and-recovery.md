# Pilot #2 Candidate — Session Fitness, Continuation & Recovery

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group E checkpoint only. This document records CRTV conclusions about Session fitness, continuation, and recovery. It does not override canonical context/session guidance.

## Purpose

Make Sessions replaceable without losing Run/orchestration truth, and move routine continuation decisions from the Human to the Orchestrator.

Core principle:

> Sessions are replaceable execution contexts. Runs and orchestration state must survive them.

## Identity separation

Keep these identities distinct:

~~~text
Work Unit
Run
Participant
Session
process / terminal
~~~

A Session replacement does not automatically create a new Run.

A new Run is created when the workflow execution occurrence is re-entered/restarted as a new execution event, not merely because the execution context changed.

Example:

~~~text
WU-S2-001
└── EXP-001
    ├── Session S-01
    └── Session S-02
~~~

Both Sessions may belong to the same Exploration Run when S-02 continues the same execution occurrence from durable state.

## Session fitness ownership

The Participant may report local execution signals such as:

- compaction/reset;
- context ambiguity;
- repeated rereads;
- lost working context;
- substantial dead ends;
- difficulty identifying current authority;
- recommendation to continue or move fresh.

The Orchestrator owns the final continuation-routing judgment:

~~~text
HEALTHY
DEGRADED
UNFIT
~~~

The Orchestrator should use current evidence and canonical context-management rules rather than mechanically trusting either a Participant recommendation or a numeric telemetry threshold.

## Session transition reasons

Record why a fresh Session is chosen.

At minimum distinguish:

- `INDEPENDENCE` — a fresh context is part of the next phase's value;
- `CONTEXT_HYGIENE` — current context is noisy/stale/compacted or otherwise less safe than re-grounding;
- `HARNESS_RECOVERY` — the prior Session/process was lost or cannot continue;
- `HUMAN_REDIRECTION` — material redirection invalidated the working context.

Examples:

~~~text
Build → fresh Code Review
Reason: INDEPENDENCE
~~~

~~~text
Build/Patch → fresh Build/Patch
Reason: CONTEXT_HYGIENE
~~~

A healthy Session may still be replaced for independence.

## No fixed threshold rule

Context/token occupancy, duration, and read count are signals only.

Do not define rules such as:

~~~text
context > 80% → fresh
10 minutes without output → stalled
file read 3 times → over-reading
~~~

Use observable consequence and semantic fitness.

A high-occupancy Session may remain HEALTHY when:

- authority remains clear;
- context is focused;
- active evidence is current;
- no substantial dead ends exist.

A lower-occupancy Session may be DEGRADED when:

- stale assumptions dominate;
- authority/current artifact identity is repeatedly confused;
- dead ends accumulated;
- retrieval is repeatedly broad/redundant without new value.

## Mid-Run reconstruction checkpoint

Before an intentional Session replacement inside an active Run, durable state must be sufficient for a fresh Session to continue safely.

Minimum reconstruction state should answer:

~~~text
Who am I?
What Run am I continuing?
What has been established?
What remains unresolved?
What current artifacts are authoritative?
Where should I continue?
~~~

Useful minimum fields/pointers:

- Run ID;
- Role / purpose;
- current stage/checkpoint;
- current-effective artifacts;
- settled decisions/findings relevant to continuation;
- open blockers/questions;
- relevant live-code/source anchors;
- next intended action.

Do not create a separate heavy artifact on every turn.

A continuation checkpoint is event-driven and written only when needed for safe replacement/recovery or when an existing phase handoff already satisfies the same need.

## Phase handoff relationship

Canonical phase handoff remains the normal durable boundary at meaningful stage/phase completion.

A mid-Run continuation checkpoint is needed only when the Session changes before a normal phase handoff is sufficient.

Do not duplicate the same information in multiple handoff artifacts.

## Fresh Participant reconstruction

A fresh Participant Session should re-ground from the smallest sufficient durable state:

~~~text
Run invocation
+ current-effective prior artifact(s)
+ continuation checkpoint when needed
+ current target-repo authority/live source
~~~

Do not replay the entire previous conversation or historical Run directory by default.

Historical Runs/events are conditional context for regression, audit, loop diagnosis, or a concrete unresolved ambiguity.

## Orchestrator self-recovery

The logical Orchestrator Participant must also survive Session replacement.

Example:

~~~text
Participant: ORCH-KENCLENG
├── Session ORCH-001
└── Session ORCH-002
~~~

A fresh Orchestrator Session should reconstruct progressively from durable orchestration state.

Preferred order:

~~~text
Parent Outcome
→ Work Graph
→ current Work Unit states
→ open Decisions / Blockers
→ active Run invocations/checkpoints
→ material recent Events only when ambiguity remains
~~~

The Control Surface may be used for fast orientation but must remain a derived projection, not the sole recovery source.

Deep event/history scanning is conditional, not the default bootstrap.

## Orchestrator recovery test

Pilot #2 should explicitly validate that a fresh Orchestrator Session can answer:

- what is active;
- what is ready;
- what is waiting/blocked;
- what needs Human attention;
- what current Runs/Sessions exist;
- what should be dispatched next;

without a large Human-written handover prompt.

A healthy bootstrap should be close to:

~~~text
Reconstruct the current Harscode Space from durable artifacts and continue routing.
~~~

rather than a prose replay of prior chat history.

## Visibility vs observability

Pilot #2 uses Automated Visible Fleet, but:

> Visibility is a debugging convenience. Observability is reconstructable execution evidence.

A visible Ghostty tab/process does not prove:

- the Run is still active;
- the Run is waiting on Human;
- the Run completed;
- the current artifact;
- Session fitness;
- next route.

Terminal/process references are operational handles only.

Run/Session/orchestration identity remains durable elsewhere.

## Process/session failure

A CLI process exit does not by itself define Run outcome.

Possible interpretations include:

~~~text
artifacts complete + expected exit
→ Run COMPLETED

process lost + sufficient checkpoint
→ Session lost / Run resumable

process lost + insufficient checkpoint
→ recovery required; strengthen durable state before safe continuation
~~~

Do not equate process existence with Session or Run state.

## Over-reading as a fitness signal

Repeated reads are not automatically defects.

Treat retrieval behavior as evidence.

A stronger degradation signal combines:

~~~text
repeated/broad reads
+ no material state change or new decision trigger
+ authority/current artifact confusion
+ stale references or context pressure
~~~

Possible repeated reads without negative consequence remain observations, not automatic intervention triggers.

## Rescue prompts

A rescue prompt occurs when the Human supplies workflow/project guidance that should reasonably have been discoverable from canonical durable authority solely to keep execution succeeding.

Examples may indicate:

- routing gap;
- durable-state gap;
- authority confusion;
- invocation gap;
- harness limitation.

Do not count genuine Human decisions, normal approvals, or clarification of genuinely new facts as rescue prompts.

Rescue prompts are CRTV evidence and should not be normalized into larger ad-hoc Human prompts.

## Stall detection

Time is a signal, not a sole rule.

A stronger STALLED signal is:

~~~text
no durable progress
+ repeated same operation/read/failure
+ no new evidence
+ no known legitimate external wait
~~~

Repeated unresolved causes should route to diagnosis rather than mechanical repetition.

## Automated Visible Fleet posture

Pilot #2 does not require continuous terminal surveillance.

Sufficient posture:

~~~text
launch
→ wait for durable completion/checkpoint signal
→ occasional status check when needed
→ inspect on timeout/stall/Human concern
~~~

If reliable completion/recovery cannot be achieved without stronger process integration, treat that as CRTV evidence before adding a supervisor/heartbeat system.

## Operational vs benchmark observability

Keep operational state separate from retrospective benchmarking.

Operational signals may influence routing/session fitness.

Benchmark data such as:

- token usage;
- allowance percentage;
- duration;
- turns;
- rescue/clarification counts;

exists for CRTV comparison and must not become required workflow authority.

A missing benchmark record must not prevent correct orchestration.

## Pilot #2 success signals

This model is working when:

- a fresh Participant Session can continue the same Run from durable state;
- a fresh Orchestrator Session can reconstruct current routing without chat-history handover;
- Human is not the normal session-transition scheduler;
- closing/losing a terminal does not lose Run identity/state;
- continuation decisions use fitness evidence rather than fixed thresholds;
- repeated retrieval can be diagnosed by consequence rather than file count;
- rescue prompts remain low and reveal durable guidance/routing weaknesses when they occur.
