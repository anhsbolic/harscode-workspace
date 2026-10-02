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
- `RUN_PATH` — durable root for Run-owned execution evidence
- `PRIOR_ARTIFACTS` — exact current-effective artifacts required by the phase; may be `none`
- `ROLE`
- optional `ARTIFACT_TARGET` — stable workflow artifact or artifact set this Run is authorized to create/update when the phase owns state-bearing output outside `RUN_PATH`
- optional `SPECIALIZATION`
- optional `PARTICIPANT`
- optional `SESSION`
- optional `WORK_UNIT_PATH` when a dedicated Harscode Space exists
- optional `TARGET_REVISION` and `WORKFLOW_REVISION`

`TARGET_REVISION` is normally the observed target-repository baseline used for
provenance/drift detection. It does not automatically pin every repository file
for the whole Run.

`WORKFLOW_REVISION` is workflow provenance. When available, it should identify
the Harscode/workflow revision actually resolved for dispatch so later
reconstruction can tell which current-effective guidance the Participant relied
on.

Recording `WORKFLOW_REVISION` does **not** by itself pin ordinary workflow
guidance. Ordinary applicable workflow guidance remains current-effective unless
the Invocation explicitly marks an exact workflow/guidance revision as
assignment-defining.

If the same Run later continues in a replacement Session and current-effective
workflow guidance has changed, preserve the prior observed revision and check the
material delta before continuing. A non-material guidance update may be adopted
with provenance; a material change that alters assignment meaning or safety must
be reconciled under the active Run rules rather than silently applied.

The target project still supplies its own authority/spec/task sources and live repository context.

## Path translation

`RUN_PATH` and `ARTIFACT_TARGET` have different meanings:

- `RUN_PATH` owns durable evidence about this execution occurrence;
- `ARTIFACT_TARGET`, when supplied, identifies stable workflow state that the
  Run is authorized to create or mutate without making that state a Run-owned
  copy.

A Run directory should contain evidence about the Run, not copies of every
workflow artifact the Run happened to touch.

Examples:

```text
Exploration Run
RUN_PATH/evidence/...

Planning Run
ARTIFACT_TARGET -> stable techplan.md or techplan.candidate.md
RUN_PATH -> Run-owned invocation/handoff/evidence only

Decomposition Run
ARTIFACT_TARGET -> stable tasks/manifest artifact set
RUN_PATH -> Run-owned invocation/handoff/evidence only

Build Run
RUN_PATH/report.md

Review Run
RUN_PATH/review-findings.md
RUN_PATH/patch-plan.md when needed

Testing Run
RUN_PATH/testing-report.md
RUN_PATH/patch-plan.md when needed
```

When no `ARTIFACT_TARGET` is supplied, a phase-owned durable output remains
Run-local only when the active canonical workflow/candidate guidance actually
defines that output as evidence of the execution occurrence.

A stable workflow artifact does not gain a new logical identity merely because a
later Run revises it. Preserve exact relied-upon revisions through durable
revision/provenance pointers rather than copying the whole artifact into each
Run directory.

A target project MAY choose different filenames inside `RUN_PATH` or a different
stable workflow-artifact layout when its orchestration manifest defines them
explicitly. The important rules are that one Run does not overwrite evidence
from an earlier Run and a Run does not duplicate stable workflow state merely
for execution chronology.

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
→ current-effective Techplan revision under review
  + current diff/scope
  + current batch/task artifact when applicable

Testing
→ current-effective Approved Techplan
  + latest relevant Build evidence
  + exact Test Focus evidence pointers
```

Do not rediscover the current-effective artifact by scanning all historical Runs if the orchestration state already names it.

## Run identity and provenance

Durable Run evidence should include `WORK_UNIT_ID` and `RUN_ID` in provenance when the artifact format permits it, plus Role/Specialization/Participant/Session when known and safe to persist.

When a Run reads or mutates a stable workflow artifact and exact identity matters
for review, approval, drift detection, or reconstruction, record a reconstructable
artifact revision/content identity in the applicable Invocation or execution
evidence. Do not create a full Run-local copy solely to obtain that provenance.

## Chronology and re-entry

Ordinal folder names are never execution chronology in orchestrated mode.

Returning to a phase after the prior execution occurrence ended requires a new
`RUN_ID`, new Participant identity, fresh Participant Session/context, and new
`RUN_PATH`. Preserve earlier Run evidence and reconstruct the new assignment
from durable inputs; do not resume the prior Participant's conversation as
hidden state.

A later Run may continue work on the same stable `ARTIFACT_TARGET` when normal
workflow lifecycle rules permit it. New Run identity does not imply a new copy of
that workflow artifact.

Immediate Session replacement while the same active Run/execution occurrence is
continuing is different: it preserves the Run and Participant and reconstructs
from the active Invocation plus the applicable continuation checkpoint.

## Findings, Decisions, and Blockers

When a phase surfaces a material item:

- observed problem/evidence → Finding;
- unresolved material authority question → Decision / human escalation;
- active inability to progress → Blocker with next-action owner.

The workflow phase reports the item; the target project's orchestration records/control surface own its current coordination state.

## Legacy compatibility

If orchestrated inputs are absent, the canonical prompt's existing `TASK_PATH` contract remains unchanged.

Existing historical Run layouts remain valid execution evidence. This overlay
does not require migration, renaming, or deletion of artifacts produced under an
earlier orchestrated layout.

Within a newly dispatched Run, do not mix implicit legacy ordinal paths and
explicit orchestrated bindings for the same artifact identity.
