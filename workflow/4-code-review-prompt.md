# Code Review Prompt

Independent review of the current implementation after Build.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}`
- `{TASK_PATH}`
- explicit current diff/changed-file scope
- Approved Techplan spine (+ current task when decomposed)
- target-repo applicable convention/instruction path

## Prompt

```text
Run an independent four-pass review against the CURRENT diff:
1. Safety
2. Quality
3. Stack-specific best practices
4. Consistency with target-repo authority

Read:
- {HARSCODE_WORKSPACE_ROOT}/workflow/4-code-review/guidelines.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/4-code-review/checklist.md
- {TASK_PATH}/2-techplan/techplan.md
- current task file only if this diff implements one decomposed task
- target repo's applicable AGENTS/README/convention source

Use best-practices/index.md as a clue map: search/scan only trigger/security
rows relevant to technologies/concerns in this diff, then open matching
best-practice files. Do not absorb the full index by default.

Do not load raw Exploration logs. The Techplan is the reviewed execution
contract; if material evidence is missing from it, report Techplan drift rather
than rebuilding intent from history.

For each finding: location, problem, why it matters, suggested resolution, and
whether it is blocking. Do not invent findings to make a pass look thorough.
If Safety reveals a specialized concurrency/perf/security area absent from the
Techplan's Test Focus Pointer, report that separately as Techplan drift.

Do NOT edit production code in this session. When changes are needed, write a
patch plan for Build.

Write review findings to {TASK_PATH}/4-code-review/review-findings-<n>.md.
When code changes are required, also write
{TASK_PATH}/4-code-review/patch-plan-<n>.md.

Output sections:
## 1. Safety
## 2. Quality
## 3. Stack-Specific Best Practices
## 4. Consistency
## Verdict
Approve | Approve with minor comments | Request changes

## Phase handoff
- Completed: four-pass review + verdict
- Artifacts: <findings path; patch-plan path if any>
- Open / blocked: <blocking findings or none>
- Recommended next step: Testing if approved; otherwise Build/Patch
- Session recommendation: FRESH for Testing; BUILD authority for patches
- Context pointers: Techplan + specific findings/patch plan + diff anchors only
```

## Notes

Fresh review context is a correctness feature: the reviewer should not inherit Build's implementation reasoning as proof. Review independence does not require re-reading unrelated Exploration history.
