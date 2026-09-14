# Code Review Prompt

Independent one-shot review of the current implementation after Build. Run all four review passes against the same explicit current diff/scope; do not edit production code in this phase.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — path to this Harscode workspace, used to resolve Code Review and best-practice guidance.
- `{TASK_PATH}` — root working directory for this task. Review artifacts are written under `{TASK_PATH}/4-code-review/`.
- **Current diff / changed-file scope** — explicit repository state to review. A build report may help orient, but it is not a substitute for inspecting the actual current diff/code.
- Approved Techplan spine, plus the current task file when the diff implements a decomposed task. This is the execution contract the diff must satisfy.
- Target-repo applicable convention/instruction source — `AGENTS.md`, README, CONTRIBUTING, or equivalent needed for the Consistency pass. The path/source must be known; do not guess another project's convention.

## Prompt

```text
Run an independent four-pass review against the CURRENT diff/scope, in order:
1. Safety
2. Quality
3. Stack-specific best practices
4. Consistency with target-repo authority

Read:
- {HARSCODE_WORKSPACE_ROOT}/workflow/4-code-review/guidelines.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/4-code-review/checklist.md
- {TASK_PATH}/2-techplan/techplan.md
- current task file only if this diff implements one decomposed task
- target repo's applicable AGENTS/README/CONTRIBUTING/convention source

Do not skip a pass because an earlier pass is clean; each pass asks a different
question. Do not invent findings merely to make the review look thorough.

Use {HARSCODE_WORKSPACE_ROOT}/best-practices/AGENTS.md as routing authority for
Pass 3: search/scan only clue/security entries relevant to technologies and
concerns in this diff, then open the matching best-practice files. Do not absorb
the full index or browse the whole tree by default.

Do not load raw Exploration logs. The Techplan is the reviewed execution
contract; if material intent/evidence is missing from it, report Techplan drift
rather than rebuilding product intent from history.

For each finding state:
- location;
- problem;
- why it matters;
- suggested resolution;
- blocking vs non-blocking.

For Stack-Specific findings, cite the matching best-practice file. For
Consistency findings, cite the target-repo convention/precedent being violated.
If no best-practice trigger matches, say so briefly instead of silently skipping
Pass 3.

If Safety reveals a specialized concurrency/perf/security area absent from the
Techplan's Test Focus Pointer, report that separately as Techplan drift.

Do NOT edit production code in this session. When code changes are needed,
write a patch plan for Build.

Write:
- {TASK_PATH}/4-code-review/review-findings-<n>.md
- {TASK_PATH}/4-code-review/patch-plan-<n>.md only when code changes are required

Increment <n> per review round; do not overwrite prior review evidence.

Output sections:

## 1. Safety
[findings, or "No findings"]

## 2. Quality
[findings, or "No findings"]

## 3. Stack-Specific Best Practices
[findings + cited best-practice source, or explicit no-match/no-finding result]

## 4. Consistency
[findings + cited target-repo convention/precedent, or "No findings"]

## Verdict
Approve | Approve with minor comments | Request changes

If Request changes, identify which findings are blocking. Minor/non-blocking
comments must not be promoted into a patch loop merely to make the artifact
look cleaner.

## Phase handoff
- Completed: four-pass review + verdict
- Artifacts: <findings path; patch-plan path if any>
- Open / blocked: <blocking findings or none>
- Recommended next step: Testing if approved; otherwise Build/Patch
- Session recommendation: FRESH for Testing; BUILD authority for patches
- Context pointers: Techplan + specific findings/patch plan + diff anchors only
```

## Notes

- Fresh review context is a correctness feature: the reviewer should not inherit Build's implementation reasoning as proof.
- Review independence does not require re-reading unrelated Exploration history.
- `workflow/4-code-review/examples.md` is conditional calibration for a concrete recurring pattern, not mandatory startup context.
