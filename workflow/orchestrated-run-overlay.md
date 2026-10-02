# Orchestrated Run Overlay

> Applies only when a workflow phase is dispatched under Orchestrator Protocol v0.1.

This file adapts **invocation, durable-path, execution-history, and orchestrated terminal-handoff rendering semantics**. It does not replace the active phase's canonical authority, verification rules, required phase-owned evidence, or phase boundary.

## Precedence

When orchestration inputs are supplied, use:

```text
canonical phase prompt
+ this overlay for identity/path/history and orchestrated terminal-handoff rendering
```

If a canonical prompt assumes ordinal `{TASK_PATH}/1-exploration`, `2-techplan`, `3-build`, `4-code-review`, or `5-testing` locations, the explicit orchestrated inputs below take precedence **for where current/prior artifacts are read or written**.

For an orchestrated Participant Run, the `Structured Phase Handoff` section below takes precedence over a canonical prompt's portable Phase Handoff field labels/rendering only. The canonical phase still owns what evidence/results must be produced and what its completion/verification boundary means.

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

## Structured Phase Handoff

Every terminated orchestrated Participant Run MUST expose exactly one compact
`## Phase handoff` in its terminal outcome carrier. This does **not** require a
new artifact: the carrier may be an existing phase-owned immutable result such as
a Build report, Review findings, or Testing report, or a standalone Handoff when
no natural terminal result carrier exists.

Use these fixed continuation fields:

```text
Outcome
Result refs
Findings
Decision requests
Blockers
Open / unverified
Recommended continuation
Context refs
```

Field semantics:

- **Outcome** describes how the Run occurrence ended, not Work Unit completion,
  milestone state, or permission to continue downstream. Use concise occurrence
  semantics such as `COMPLETED`, `STALLED`, or `FAILED` when they fit the actual
  result.
- **Result refs** point to materially relevant terminal/stable outputs and exact
  revisions when later reliance requires them. They are not a touched-file
  inventory and must not copy stable artifacts into `RUN_PATH`.
- **Findings**, **Decision requests**, and **Blockers** remain semantically
  distinct. Use pointers to durable owning evidence when available; concise
  inline wording is acceptable when the handoff itself is the owning terminal
  evidence.
- **Blockers** identify the affected scope and safe unaffected work when known;
  do not silently widen a scoped blocker to the whole Work Unit.
- **Open / unverified** records material uncertainty, deferred evidence, or
  verification not yet established. Open/unverified work is not automatically a
  Blocker.
- **Recommended continuation** is Participant-local advice only. It does not
  create the next Run, choose project-wide routing, promote a milestone, or
  authorize downstream work.
- **Context refs** contain only the smallest durable pointers needed to reopen
  relevant evidence or authority context. Do not restate the full source set.

The structured Phase Handoff is an index into durable execution/project truth,
not a second report. Do not repeat detailed test output, full findings, copied
plans, source diffs, or evidence that already has an owning artifact.

The Orchestrator may reconcile or route directly from the structured handoff when
it is sufficient. When it is not sufficient, selectively open the referenced
evidence rather than requiring every terminal handoff to reproduce it.

Do not add a separate `Session transition` field to this terminal shape. Run
termination already ends the execution occurrence; subsequent Session/Run
posture is resolved by Orchestrator routing. Portable non-orchestrated workflow
handoffs may retain their existing canonical wording.

## Legacy compatibility

If orchestrated inputs are absent, the canonical prompt's existing `TASK_PATH` contract remains unchanged.

Existing historical Run layouts remain valid execution evidence. This overlay
does not require migration, renaming, deletion, or backfill of artifacts produced
under an earlier orchestrated layout, including historical handoffs that predate
the structured Phase Handoff shape.

Within a newly dispatched Run, do not mix implicit legacy ordinal paths and
explicit orchestrated bindings for the same artifact identity.
