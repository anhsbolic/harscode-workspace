# Orchestrated Run Contract

Use this contract when a target project runs Harscode under Orchestrator Protocol v0.1.

## Invocation identity

Keep these distinct:

```text
Work Unit → bounded delivery outcome
Run       → one workflow execution occurrence
Participant→ assigned executor identity
Session   → bounded execution context
```

## Required orchestration inputs

An orchestrated phase invocation should make these values discoverable:

- `WORK_UNIT_ID` — stable logical Work Unit identifier.
- `RUN_ID` — unique occurrence identifier for this workflow execution.
- `RUN_PATH` — durable write location for artifacts produced by this Run.
- `WORK_UNIT_PATH` — optional dedicated Harscode Space root when one exists.
- `PRIOR_ARTIFACTS` — explicit current-effective prior artifacts required by this phase.
- `ROLE` — canonical role for the Run.
- `SPECIALIZATION` — optional role specialization.
- `PARTICIPANT` — assigned executor identity when known.
- `SESSION` — execution-context identifier when known.
- `TARGET_REVISION` / `WORKFLOW_REVISION` — when known and safe to persist.
- `COMMUNICATION_LANGUAGE` — optional human-facing language selected by the target project.
- `COMMUNICATION_PROFILE_PATH` — optional path to additional project-specific communication guidance.
- `SELECTED_MODEL` — optional dispatch-time model resolved from Human-owned local runtime configuration.
- `REASONING_EFFORT` — optional dispatch-time reasoning/thinking level resolved separately from the model and constrained by the Human-owned registry.
- `MODEL_APPROVAL` — required approval evidence when the selected model is marked `approval_required: true`.
- `PHASE_ROUTE` — concrete workflow phase/re-entry being dispatched and its current applicability/routing posture; when an independent phase is not applicable, the Orchestrator records that N/A decision outside a nonexistent skipped-phase Run.
- `EXECUTION_ENVELOPE` — compact semantic authorization block or pointer describing authorized write scope, routine capabilities, known required commands, justified specialized verification, Orchestrator-routed actions, and Human/protected actions.
- `MODEL_ROUTING_RATIONALE` — concise minimum-capability and sufficiency rationale for the selected model/reasoning effort, plus escalation trigger when applicable.
- `CONTINUATION_CHECKPOINT` — optional pointer to durable continuation state; required when a new Session continues an already-active Run and the normal phase handoff is not sufficient.
- `SESSION_TRANSITION` — optional `CONTINUE` / `FRESH` routing result when relevant.
- `SESSION_TRANSITION_REASON` — explicit reason for the transition, such as independence, context hygiene, harness recovery, Human redirection, or another stated reason.

Project-specific authority/task sources remain explicit inputs to the phase.

Dispatch fields operationalize settled authority; they do not create new Product, security, interface, architecture, risk, verification, or workflow authority. When execution discovers a new material obligation, surface it through the applicable Finding/Decision/planning-reconciliation path instead of smuggling it into free-form invocation text.

Model availability/capability metadata and supported reasoning efforts are runtime context, not Work Unit authority. Resolve model and reasoning effort separately according to `orchestration/local-runtime-config.md`; do not copy the whole local registry into durable Run artifacts unless needed as pilot evidence.

`MODEL_ROUTING_RATIONALE` is dispatch evidence, not a model score. Before stronger-model escalation, distinguish capability insufficiency from missing context, guidance/routing gaps, authority gaps, and environment/harness gaps. A stronger model must not substitute for resolving one of those other causes.

When `COMMUNICATION_LANGUAGE` is present, it affects human-facing prose only. Canonical Harscode terms/enums and code/API/schema identifiers remain unchanged. `COMMUNICATION_PROFILE_PATH` is optional and MUST NOT be treated as a required dependency when absent or set to `none`.

The Run Execution Envelope is semantic. Harness sandbox/approval settings translate it; they do not create or expand authority. Use these authorization classes when the envelope needs an explicit class:

```text
PREAUTHORIZED
ORCHESTRATOR_DECISION
HUMAN_REQUIRED
```

- `PREAUTHORIZED` — routine, reversible, in-scope execution already justified by settled project/workflow authority.
- `ORCHESTRATOR_DECISION` — coordination or scope-expansion choice within settled authority that is not ordinary Participant autonomy and is not Human-owned.
- `HUMAN_REQUIRED` — protected, destructive, gated, authority-changing, or material risk-acceptance boundary owned by Human/project authority.

Do not turn these classes into an exhaustive command whitelist unless execution evidence later justifies stronger machinery.

## Compatibility with legacy TASK_PATH

Existing projects may still use `TASK_PATH`. Under orchestration:

- do not infer chronology from numbered child directories;
- prefer explicit `RUN_PATH` and `PRIOR_ARTIFACTS`;
- when a phase prompt still accepts `TASK_PATH`, it may be used as a compatibility root only if the project maps it unambiguously to the current Work Unit/Run and does not treat its folder order as execution truth.

## Session continuation

A fresh Session may continue the same active Run when it is continuing the same workflow execution occurrence. Session replacement alone does not create a new Run.

When a fresh Session continues an active Run and the normal phase handoff is not sufficient, `CONTINUATION_CHECKPOINT` should point to the smallest sufficient durable state needed to answer:

```text
What Run am I continuing?
What has been established?
What remains unresolved?
What current artifacts are authoritative?
Where should I continue?
```

A useful checkpoint makes discoverable the current Run purpose/stage, current-effective artifacts, settled relevant findings/decisions, open blockers/questions, relevant source anchors, and next intended action. Checkpointing is event-driven, not periodic ceremony.

Session-transition routing follows `workflow/context-management.md`. Do not derive it mechanically from token percentage, elapsed time, or read count.

## Durable output

A Run writes only its own durable evidence under `RUN_PATH`. It references prior artifacts rather than copying them.

A Run record should preserve, when known:

```text
Run ID
Work Unit ID
Phase
Phase route / applicability
Purpose
Role / Specialization
Participant
Session
Session transition / reason
Continuation checkpoint when applicable
Execution envelope or pointer
Selected model / reasoning effort
Model routing rationale / approval evidence
Trigger
Outcome
Produced artifacts
Findings / Decisions / Blockers raised
Next route
```

## Re-entry

Returning to Exploration, Planning, Build, Review, or Testing creates a new Run. Never overwrite the prior Run merely to make the directory look linear.

The current effective Artifact must be explicit when multiple versions/runs exist.

## Tiny work

A dedicated Harscode Space is not mandatory. A small Work Unit may be durable through its Work Unit record plus commit/PR/test evidence. Do not create empty history scaffolding for ceremony.
