# Techplan Decomposition Prompt

Optional post-Approval step for splitting execution detail when one Techplan is too broad to execute/review as a single work unit.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}`.
- `{TASK_PATH}/2-techplan/techplan.md` at **Approved** or later.
- Applicable target-repo authority if task boundaries depend on it.

## Prompt

```text
You are deciding whether an Approved Techplan should be decomposed into
execution task files. Read:
- {TASK_PATH}/2-techplan/techplan.md in full;
- {HARSCODE_WORKSPACE_ROOT}/workflow/2-techplan/rules.md §10 (spine invariant);
- this prompt's decomposition rules below.

Gate — answer first:
Is decomposition genuinely useful?

Answer NO and stop when the plan is linear/cohesive enough to execute as one
unit or splitting would create trivial boundaries. File length alone is not a
reason to split.

Answer YES only when there are independently executable/reviewable chunks,
real dependency boundaries, materially different blast-radius/risk slices, or
an execution agent would otherwise need unrelated implementation detail in its
active context.

If YES:
1. Choose the least-surprising splitting axis that reflects the actual work:
   dependency/sequence, component/module, vertical layer, independently
   reviewable chunk, or risk/blast-radius. State the reason.
2. Create task files in {TASK_PATH}/2-techplan/tasks/.
3. Each task contains full scoped execution detail and code anchors needed for
   that task, plus explicit references to parent Techplan decision/risk/rule IDs.
4. Do not copy the whole parent contract into every task. The parent Techplan
   remains the authoritative spine.
5. Never move a material scope/rule, decision, risk, interface/data contract,
   verification obligation, or unresolved item so that it exists only in a
   child task. If decomposition reveals such a missing parent-spine item, stop
   and update/re-review the Techplan rather than hiding it in a task.
6. A task must be executable with: parent spine + this task + declared hard
   dependency task (only if needed) + live code/spec. It must not require
   reading unrelated sibling tasks.
7. Generate a manifest last: task list, splitting axis/rationale, dependency
   graph (or explicit no-hard-dependency), and parent Techplan back-reference.
   Model routing is not decided here unless the active target/harness execution
   profile explicitly owns it.

Do not compress away required execution detail and do not reinterpret the
approved contract.

At completion, report:

## Phase handoff
- Completed: decomposition gate + generated task set/manifest when warranted
- Artifacts: <task/manifest paths or none>
- Open / blocked: <contract gaps found or none>
- Recommended next step: human check of the split, then Build
- Session recommendation: FRESH for Build
- Context pointers: parent Techplan + first/current task + declared dependency only
```

## Decomposition rules

- **Not compression.** Required scoped execution detail stays complete.
- **Not reinterpretation.** Child tasks execute decisions; they do not make new material decisions.
- **Spine first.** The approved Techplan remains the always-authoritative cross-task contract.
- **No progress ledger.** Task manifest is a generated execution map, not project-status tracking.
- **No split-by-size rule.** Split by independently useful execution boundaries, not line count.

## Notes

If Code Review/Testing later shows that a child task depended on a material decision absent from the parent spine, fix/reopen the Techplan and regenerate affected task files. Do not patch one child into becoming a shadow contract.
