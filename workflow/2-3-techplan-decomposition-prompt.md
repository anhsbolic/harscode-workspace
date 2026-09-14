# Techplan Decomposition Prompt

Optional post-Approval step for splitting execution detail when one Techplan contains multiple independently useful work units. Decomposition is an execution-context optimization, not a way to shorten or reinterpret the approved contract.

## When to use this

Run only after the parent Techplan is **Approved** (or later) and only when decomposition creates a real execution/review benefit.

Useful signals:

- multiple chunks can be executed or reviewed independently;
- hard dependencies create a meaningful sequence;
- different components/layers have clearly different implementation scope;
- sensitive/high-blast-radius work should be isolated from routine work;
- one Build agent would otherwise need substantial unrelated implementation detail in active context.

Skip decomposition when the Techplan is cohesive/linear enough to execute as one unit, or when splitting would mostly produce trivial one-file/one-function tasks. File length alone is not a reason to split.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — path to this Harscode workspace. Used to resolve Techplan/decomposition authority.
- `{TASK_PATH}` — root working directory for this task. The parent plan is `{TASK_PATH}/2-techplan/techplan.md`; generated task files/manifest go under `{TASK_PATH}/2-techplan/tasks/`.
- Approved `{TASK_PATH}/2-techplan/techplan.md` — authoritative parent spine. Do not run against Draft/In Review material that may still change materially.
- Applicable target-repo authority/spec/live-code sources when a proposed task boundary depends on current module/component ownership or dependency shape.

## Prompt

```text
You are deciding whether an Approved Techplan should be decomposed into
execution task files.

Read:
- {TASK_PATH}/2-techplan/techplan.md in full;
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/rules.md §10 (Techplan spine
  and decomposition invariant);
- the decomposition rules and splitting-axis guidance in this prompt.

Response style: be concise about the decomposition decision, but preserve full
execution detail inside any generated task file. This step redistributes scope;
it does not compress away required information.

STEP 0 — GATE (answer explicitly before generating anything)
Is decomposition genuinely useful for this Techplan?

Answer NO and stop when:
- the work is linear/cohesive enough to execute as one unit;
- the proposed split would create trivial boundaries with no context/review
  benefit;
- the only reason to split is document length.

Answer YES only when at least one real execution/review/context boundary exists.
State the signal(s) that justify the split.

STEP 1 — CHOOSE THE SPLITTING AXIS
Choose the least-surprising axis that reflects the actual work. Do not choose
an axis merely because it is available:

- Dependency / sequence — use when task B genuinely cannot execute until task A
  establishes a prerequisite contract/data/schema/component.
- Component / module — use when separate modules can be changed/reviewed with
  little implementation-context overlap and no hard dependency.
- Vertical layer — use when persistence/business/interface layers form useful
  independent execution/review steps; do not use if separating layers would
  hide a cross-layer invariant.
- Independently reviewable chunk — use when a coherent behavior slice can be
  implemented/reviewed on its own without inventing a new contract boundary.
- Risk / blast radius — use when sensitive/security/data-destructive/breaking
  work should be isolated from lower-risk work for review/authority reasons.

When more than one axis could work, prefer the one that makes dependencies and
contract ownership easiest for Build to understand. State the chosen axis and
why before generating task files.

STEP 2 — GENERATE TASK FILES
Write task files under {TASK_PATH}/2-techplan/tasks/.

Each task file must include:
- task purpose and exact scoped outcome;
- parent Techplan path/version/status back-reference;
- parent rule/decision/risk/contract IDs that govern the task;
- scoped implementation detail and code anchors needed for this task;
- hard dependency task(s), only when genuinely required;
- scoped verification obligations the task must satisfy before handoff;
- any explicit NOT-in-this-task boundary needed to prevent scope bleed.

A task must be executable from:

parent Techplan spine
+ this task file
+ declared hard-dependency task only when required
+ current live code/spec authority

It must not require unrelated sibling task files merely because they exist.

STEP 3 — PRESERVE THE SPINE
Do NOT move or rewrite material information so it exists only in a child task.
The parent Techplan remains authoritative for:
- material scope/rules;
- chosen/rejected decisions and rationale;
- risks/accepted exposure;
- interface/data/authority contracts;
- verification obligations;
- unresolved Open Items.

Child tasks may reference those IDs and add scoped execution detail. If the
split exposes a material decision/risk/contract/verification item missing from
the parent spine, STOP: the Techplan needs revision/human gate (and possibly
re-review), not a hidden child-task fix.

Do not reinterpret an approved decision while decomposing. Do not generate or
regenerate the human-facing report here; `report-techplan.md` is independent
of whether decomposition runs.

STEP 4 — GENERATE THE MANIFEST LAST
Write a manifest under {TASK_PATH}/2-techplan/tasks/ containing:
- task file list + short purpose;
- chosen splitting axis + rationale;
- dependency graph/order, or explicit `no hard dependency` where appropriate;
- parent Techplan back-reference;
- any shared contract/risk IDs that multiple tasks must coordinate around.

The manifest is an execution map at generation time, not a progress ledger.
Do not add done/in-progress status tracking. Model/client routing also does not
belong here unless an active target/harness execution profile explicitly owns
and requests that metadata.

At completion, report:

## Phase handoff
- Completed: decomposition gate + generated task set/manifest when warranted
- Artifacts: <task/manifest paths or none>
- Open / blocked: <contract gap discovered or none>
- Recommended next step: human check of the split, then Build
- Session recommendation: FRESH for Build
- Context pointers: parent Techplan + first/current task + declared hard dependency only
```

## Decomposition invariants

- **Not compression.** Required scoped execution detail remains complete.
- **Not reinterpretation.** Child tasks execute approved decisions; they do not make new material ones.
- **Spine first.** The Approved Techplan remains the cross-task authority.
- **No shadow contracts.** A material decision/risk/contract/verification obligation cannot live only in a child task.
- **No progress ledger.** The manifest describes execution structure, not project status.
- **No split-by-size rule.** Split only on independently useful execution/review/context boundaries.

## Notes

- A human should review the decomposition shape before Build begins; a syntactically valid split can still choose a poor boundary.
- If later Code Review/Testing shows that a child task depended on a material decision absent from the parent spine, reopen/fix the Techplan and regenerate affected task files. Do not patch one child into becoming a second source of truth.
- Task files are snapshots derived from an Approved plan. If a material parent contract changes, regenerate or explicitly reconcile affected task files before continuing.
