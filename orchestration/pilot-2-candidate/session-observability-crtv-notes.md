# Pilot #2 Candidate — Group E CRTV Notes

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: concise Pilot #1 observations motivating the Group E candidate model.

## Note E1 — Run, Session, and terminal/process identity must remain separate

Pilot #1 already distinguished Work Unit, Run, and Session conceptually.

Pilot #2 Automated Visible Fleet adds another temptation: treating a visible Ghostty/Codex process as execution truth.

The reusable rule is:

> terminal/process existence is an operational signal, never the authoritative Run/Session state.

## Note E2 — Continuation fitness is stronger than a fixed context threshold

Existing Harscode guidance correctly rejects rules such as:

~~~text
80% context → always fresh
~~~

Pilot #1 did not provide evidence that one numeric cutoff would be reliable.

Continuation should remain based on authority clarity, focused context, dead ends, compaction/redirection, and independence needs.

## Note E3 — Over-reading must be diagnosed from relevance and consequence

Pilot #1 raised the question of whether agents were rereading too much, but existing artifacts did not provide enough direct read telemetry to answer it confidently.

Candidate direction:

- collect targeted retrieval signals;
- do not classify from count alone;
- treat repeated/broad reads plus authority confusion/context degradation as stronger evidence.

## Note E4 — Fresh Session within the same Run is legitimate

A fresh Session does not imply a new Run when it continues the same workflow execution occurrence.

Pilot #2 should preserve this so context hygiene does not inflate Run history artificially.

## Note E5 — Mid-Run replacement needs durable reconstruction state

Phase handoffs cover many normal boundaries, but a Session can degrade or be lost before a phase ends.

A minimal continuation checkpoint is therefore useful when needed.

It should remain event-driven, not mandatory periodic paperwork.

## Note E6 — Dedicated Orchestrator must itself be replaceable

Pilot #1 orchestration lived primarily in the ChatGPT conversation/operator.

Pilot #2 moves orchestration into a dedicated local Orchestrator Participant.

That Participant must survive its own Session replacement by reconstructing from:

- Parent Outcome;
- Work Graph;
- current Work Unit states;
- open Decisions/Blockers;
- active Run state/checkpoints.

A large Human-authored handover prompt should count as a recovery weakness, not a normal operating requirement.

## Note E7 — Human should not remain the routine session router

Pilot #1 required the Human/operator to decide and manually create many fresh/continued CLI Sessions.

Pilot #2 should move normal continuation/fresh-session routing to the Orchestrator.

Human intervention remains appropriate for real authority decisions, correction of wrong routing, launcher failures, or unusual recovery.

## Note E8 — Rescue prompts are valuable CRTV evidence

Existing Codex benchmarking guidance defines rescue prompts as extra workflow/project guidance the agent should have discovered itself.

Pilot #2 should preserve this distinction.

A high rescue-prompt rate may reveal:

- poor invocation;
- missing durable routing;
- authority ambiguity;
- context handoff weakness;
- harness limitations.

Ordinary Human approvals and genuinely new decisions are not rescue prompts.

## Note E9 — Visibility is not observability

Automated Visible Fleet provides strong Human debugging visibility during the pilot.

It does not replace durable observability.

The long-term value of Pilot #2 is to learn how much terminal visibility is still needed once Run lifecycle, retrieval, permission, and recovery evidence become reliable.

## Note E10 — Orchestrator self-recovery is a high-value Pilot #2 test

A deliberate or naturally occurring fresh Orchestrator Session should be used to test whether the Group A durable artifact model is sufficient.

Success means the new Session can reconstruct current orchestration state without depending on prior chat transcript.
