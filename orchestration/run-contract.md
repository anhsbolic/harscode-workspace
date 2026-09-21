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

Project-specific authority/task sources remain explicit inputs to the phase.

Model availability/capability metadata and supported reasoning efforts are runtime context, not Work Unit authority. Resolve model and reasoning effort separately according to `orchestration/local-runtime-config.md`; do not copy the whole local registry into durable Run artifacts unless needed as pilot evidence.

When `COMMUNICATION_LANGUAGE` is present, it affects human-facing prose only. Canonical Harscode terms/enums and code/API/schema identifiers remain unchanged. `COMMUNICATION_PROFILE_PATH` is optional and MUST NOT be treated as a required dependency when absent or set to `none`.

## Compatibility with legacy TASK_PATH

Existing projects may still use `TASK_PATH`. Under orchestration:

- do not infer chronology from numbered child directories;
- prefer explicit `RUN_PATH` and `PRIOR_ARTIFACTS`;
- when a phase prompt still accepts `TASK_PATH`, it may be used as a compatibility root only if the project maps it unambiguously to the current Work Unit/Run and does not treat its folder order as execution truth.

## Durable output

A Run writes only its own durable evidence under `RUN_PATH`. It references prior artifacts rather than copying them.

A Run record should preserve, when known:

```text
Run ID
Work Unit ID
Phase
Purpose
Role / Specialization
Participant
Session
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
