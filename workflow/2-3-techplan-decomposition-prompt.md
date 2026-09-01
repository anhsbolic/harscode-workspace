# Decomposition Prompt

## When To Use This

Optional step, run manually **after** the techplan contract has been
locked — not a default step for every techplan. Invoke this when either
of the following signals shows up:

- The techplan has multiple chunks of work that can be reviewed/executed
  separately (you don't have to finish reading one to start on another).
- The execution agent appears to "lose focus" because it has to hold the
  entire techplan context at once, even though it's only working on one
  part of it.

If the techplan is still small/linear and the execution agent can run
straight through from start to finish without losing focus, **skip this
step**. Premature decomposition is the same kind of liability as premature
structure.

## What This Must Not Do

- **Not compression.** Task files produced by this process must remain
  full-detail for their respective scope. If any detail gets "dropped" for
  the sake of being "lean," that's wrong — detail must be redistributed to
  the relevant task, never shortened or omitted.
- **Not reinterpretation.** The agent must not introduce new decisions,
  change scope, or resolve ambiguity that hasn't already been settled in
  the contract. Its job is purely to split, not to resolve.
- **Contract section stays untouched.** The original techplan (specifically
  the contract) remains a single file and stays the source of truth for
  human review. Only the derived section — the part consumed by the
  execution agent — gets split. `techplan.md` has no embedded Summary
  or digest section to worry about here (Proposal 0012 moved that to a
  separately-generated `report-techplan.md`, sourced from the approved
  techplan — decomposition does not touch or regenerate that file). §
  12's Test Focus Pointer table, if present, is a task-level pointer
  consumed by the testing phase after all tasks are done, not per-task
  detail — it stays with the contract, never redistributed or
  duplicated into individual task files.

## Inputs required before running

- A techplan that has already been locked (`Status: Approved` or later
  in `template.md`'s lifecycle — not `Draft` or `In Review`). Running
  this against an unlocked techplan risks decomposing content that's
  still going to change.
- `{TASK_PATH}` — root working directory for this specific task; the
  techplan under consideration is at `{TASK_PATH}/2-techplan/techplan.md`
  (see root `README.md` § Task Working Directory Structure).
- `{WORKSPACE_ROOT}` — path to this harscode-workspace's content
  relative to (or as an absolute path from) your project. Set once per
  project; see `workflow/README.md` § Path Variables Convention. Used
  below for the model-routing reference.

## Response Style

Full detail, no compression, when redistributing content into task
files — see "What This Must Not Do" above; that constraint IS this
phase's response-style rule. State the chosen splitting axis and
rationale explicitly, don't just apply one silently
({WORKSPACE_ROOT}/workflow/README.md § Response Style By Phase).

## Prompt

```
Read {WORKSPACE_ROOT}/workflow/2-3-techplan-decomposition-prompt.md in
full first — "When To Use This," "What This Must Not Do," and "Agent
Workflow" (steps 0-4) define what you're allowed to do here and what
you must not do (no compression, no reinterpretation, contract section
and any Test Focus Pointer table stay with the original techplan, not
redistributed).

Response style: full detail, no compression, when redistributing
content into task files. State the splitting axis you choose and why,
explicitly — don't apply one silently
({WORKSPACE_ROOT}/workflow/README.md § Response Style By Phase).

The techplan under consideration is at {TASK_PATH}/2-techplan/techplan.md
— its contract must already be locked (not Draft). Read it in full
before doing anything else.

Step 0 — Gate question (mandatory, answer explicitly before proceeding):
Is it worth it to decompose this techplan? Answer no and stop here,
reporting a one-line reason, if it's small/linear enough for an
execution agent to run through start to finish without losing focus,
or if splitting it would mostly produce trivial single-task
boundaries. Do not proceed to Step 1 on autopilot just because this
prompt was invoked.

If yes: read the full techplan (Step 1), choose one splitting axis
from "Agent Workflow" § 2 — defaulting to dependency/sequence chain
when it's ambiguous — and state your choice and rationale before
redistributing content (Step 3). Each task file must remain
full-detail for its scope; nothing gets shortened or summarized in the
split, only relocated. Include a back-reference to the originating
techplan in every task file.

Generate the manifest last (Step 4) — task list, splitting axis +
rationale, dependency graph (or an explicit "no hard dependency"
marker), back-reference to the techplan, and which model to route each
task to (see {WORKSPACE_ROOT}/best-practices/model-routing.md).

Write every task file plus the manifest to
{TASK_PATH}/2-techplan/tasks/. Report the gate-question answer and,
if you proceeded, the splitting axis chosen — I'll review the split
before any task is executed.
```

## Agent Workflow

### 0. Answer first: is it worth decomposing this techplan?

> **Is it worth it to decompose this techplan?**

Before doing anything else, read the techplan and answer this question
explicitly — state the answer and the reasoning behind it. Do not proceed
to Step 1 on autopilot just because this prompt was invoked.

Answer **no** (stop here, do not decompose) if:

- The techplan is small/linear enough that an execution agent can run
  through it start to finish without losing focus.
- Splitting it would mostly produce single-task manifests or trivial
  boundaries — decomposition for its own sake.

Answer **yes** (proceed to Step 1) only if at least one of the trigger
signals from "When To Use This" genuinely applies to this specific
techplan.

If the answer is no, stop and report that decomposition isn't warranted,
with a one-line reason. Don't generate task files or a manifest just
because the prompt was run.

### 1. Read the techplan in full

Don't start splitting before understanding the overall scope and the
dependencies between its parts.

### 2. Choose a splitting axis

Pick one of the following options (or a combination, if the techplan is
complex enough), based on the characteristics of the techplan you read:

- **Dependency/sequence chain** — tasks are split based on hard
  dependencies; task B cannot start until task A is done. Choose this when
  the techplan has stages that genuinely wait on each other.
- **Component/module boundary** — tasks are split along independent code
  boundaries (different package/service/domain). Choose this when there
  are multiple modules that don't technically depend on each other.
- **Layer (vertical slice)** — data layer → business logic → interface/API
  layer as separate tasks. Choose this when a single change cuts across
  multiple layers and each layer has a different review concern.
- **Review-able/PR-sized chunk** — tasks are split so each task equals one
  PR that can be merged independently. Choose this when the main goal is
  reviewability rather than execution efficiency.
- **Risk/blast-radius** — tasks are split so sensitive changes
  (security-critical, data-destructive, breaking-change) are separated
  from low-risk changes. Choose this when the techplan mixes high-risk and
  low-risk changes within a single scope.

**When it's ambiguous, default to dependency/sequence chain** — this axis
carries the least assumption compared to the others, especially
risk/blast-radius, which requires additional judgment.

State the chosen axis and a short rationale before moving to the next
step — this will go into the manifest.

### 3. Redistribute detail into task files

For each resulting task:

- Copy/redistribute the derived-section detail relevant to that task's
  scope — do not summarize it.
- Include a back-reference to the originating contract techplan
  (path/title), so the execution agent can cross-check high-level
  decisions whenever needed.
- Each task should be executable without needing to read other tasks
  first, except where dependency is genuinely required by the chosen
  splitting axis.

### 4. Generate the manifest

The manifest is a snapshot-at-generation-time, not a living document — it
does not track progress status (done/in-progress/blocked). Status tracking
belongs to the PR/ticket domain, not this workspace.

Minimum manifest contents:

- List of task files + a short title for each.
- The splitting axis used (+ brief rationale from step 2).
- Dependency graph between tasks (if the axis is sequence/dependency) — or
  an explicit "no hard dependency" marker if the axis is parallel
  (component/module).
- Back-reference to the originating contract techplan.
- llm models to execute each tasks, you can read {WORKSPACE_ROOT}/best-practices/model-routing.md

## Output

Write everything below to `{TASK_PATH}/2-techplan/tasks/` (see root
`README.md` § Task Working Directory Structure):

- N task files (count depends on the resulting split), each self-contained
  for its scope.
- 1 manifest file indexing all the tasks above.

## Cross-reference

- Source techplan: see `{WORKSPACE_ROOT}/workflow/2-1-techplan-synthesis-prompt.md`
  for the contract/derived authoring process that precedes this
  decomposition step.
- Task files produced here are still subject to the review checklist in
  `{WORKSPACE_ROOT}/workflow/4-code-review/checklist.md`, same as any
  other derived-section content.

## Notes

- The manifest and task files are a snapshot, not a living document —
  don't hand-edit them to reflect progress; that belongs in your
  PR/ticket tooling, not here.
- Treat the Step 0 gate answer as a real decision, not a formality: if
  the honest answer is "not worth it," stopping there and executing
  straight from the original techplan is the correct outcome, not a
  failure to produce output.
- If a later code-review or testing pass surfaces a decision that
  should have been in the original contract, that's a signal to update
  the techplan itself (and regenerate `report-techplan.md` if it's
  already Approved) — not to patch a task file in isolation.
- This file only covers splitting an already-locked techplan into task
  files. It does not cover generating the human-facing report — see
  `report-template.md` for that, which is independent of whether
  decomposition ran.