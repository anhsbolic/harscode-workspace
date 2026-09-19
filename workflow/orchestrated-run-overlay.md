# Orchestrated Run Overlay

> Applies only when a workflow phase is dispatched under Orchestrator Protocol v0.1.

This file adapts **invocation and durable-path semantics only**. It does not replace the active phase's canonical prompt, authority, verification rules, or phase boundary.

## Precedence

When orchestration inputs are supplied, use:

```text
canonical phase prompt
+ this overlay for identity/path/history semantics
```

If a canonical prompt assumes ordinal `{TASK_PATH}/1-exploration`, `2-techplan`, `3-build`, `4-code-review`, or `5-testing` locations, the explicit orchestrated inputs below take precedence **for where current/prior artifacts are read or written**.

Do not reinterpret that precedence as permission to skip required phase artifacts or phase authority.

## Required orchestrated inputs

- `WORK_UNIT_ID`
- `RUN_ID`
- `RUN_PATH` — durable write root for this Run
- `PRIOR_ARTIFACTS` — exact current-effective artifacts required by the phase; may be `none`
- `ROLE`
- optional `SPECIALIZATION`
- optional `PARTICIPANT`
- optional `SESSION`
- optional `WORK_UNIT_PATH` when a dedicated Harscode Space exists
- optional `TARGET_REVISION` and `WORKFLOW_REVISION`

The target project still supplies its own authority/spec/task sources and live repository context.

## Path translation

Use `RUN_PATH` as the durable destination for artifacts created by the current Run.

Examples:

```text
Exploration Run
RUN_PATH/evidence/...

Planning Run
RUN_PATH/techplan.md

Build Run
RUN_PATH/report.md

Review Run
RUN_PATH/review-findings.md
RUN_PATH/patch-plan.md when needed

Testing Run
RUN_PATH/testing-report.md
RUN_PATH/patch-plan.md when needed
```

A target project MAY choose different filenames inside `RUN_PATH` when its orchestration manifest defines them explicitly. The important rule is that one Run does not overwrite evidence from an earlier Run.

## Prior artifacts

Where the canonical prompt says to read an artifact from an ordinal `TASK_PATH` phase directory, use the corresponding explicit entry in `PRIOR_ARTIFACTS`.

Examples:

```text
Techplan
→ current-effective Exploration artifacts

Build
→ current-effective Approved Techplan
  + current execution batch/task artifact when applicable
  + specific patch plan when re-entering

Review
→ current-effective Approved Techplan
  + current diff/scope
  + current batch/task artifact when applicable

Testing
→ current-effective Approved Techplan
  + latest relevant Build evidence
  + exact Test Focus evidence pointers
```

Do not rediscover the current-effective artifact by scanning all historical Runs if the orchestration state already names it.

## Run identity and provenance

Durable artifacts should include `WORK_UNIT_ID` and `RUN_ID` in provenance when the artifact format permits it, plus Role/Specialization/Participant/Session when known and safe to persist.

## Chronology and re-entry

Ordinal folder names are never execution chronology in orchestrated mode.

Returning to a phase requires a new `RUN_ID` and `RUN_PATH`. Preserve earlier Run evidence.

## Findings, Decisions, and Blockers

When a phase surfaces a material item:

- observed problem/evidence → Finding;
- unresolved material authority question → Decision / human escalation;
- active inability to progress → Blocker with next-action owner.

The workflow phase reports the item; the target project's orchestration records/control surface own its current coordination state.

## Legacy compatibility

If orchestrated inputs are absent, the canonical prompt's existing `TASK_PATH` contract remains unchanged.

Do not mix implicit legacy ordinal paths and explicit orchestrated Run paths within the same Run.
