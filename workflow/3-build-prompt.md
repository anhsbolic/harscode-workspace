# Build / Patch Prompt

Canonical entrypoint for the edit → verify → fix implementation loop after Techplan approval.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}`
- `{TASK_PATH}`
- Approved `{TASK_PATH}/2-techplan/techplan.md`
- current task file when decomposition ran, otherwise the Techplan itself is the build target
- optional specific patch plan when re-entering from Code Review/Testing

## Prompt

```text
You are executing the Approved contract through Build/Patch authority.

Read:
- {HARSCODE_WORKSPACE_ROOT}/workflow/3-build/guidelines.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/3-build/checklist.md
- {TASK_PATH}/2-techplan/techplan.md as the authoritative spine
- the current task file only when decomposition exists
- the specific patch plan only when this is a Review/Testing re-entry

Do not load raw Exploration logs by default. If the Techplan explicitly points
to unresolved evidence, open that exact source only.

Before editing, reopen current live code/spec at the Techplan/task code anchors.
Earlier Exploration/Techplan descriptions are coordinates/evidence, not a frozen
copy of implementation reality.

Do not re-explore settled product/domain decisions. If live code contradicts a
material Techplan assumption (behavior, authority/security, architecture/
ownership, interface/data contract, risk/verification), stop and report it
instead of silently redesigning.

When task files exist, execute the current task with the parent spine. Do not
read unrelated sibling tasks unless a declared hard dependency requires one.

For patch re-entry, production fixes remain Build work even when the finding
came from Review/Testing. Re-ground on the parent Techplan + current task (if
any) + specific patch plan + relevant live code/diff; do not import the whole
Review/Testing conversation.

Run the Build-loop test scope defined in guidelines.md. Do not pull heavyweight
race/perf/security-class verification into this tight loop.

Process narration is terse; do the work. Write:
- initial: {TASK_PATH}/3-build/report.md
- patch: {TASK_PATH}/3-build/patch-report-<n>.md

Report format:

## What changed
[file → concise behavior/contract-relevant change]

## Tests run
[test/pattern → category → result]

## Contract check
- [ ] Current build target satisfied
- [ ] Live-code re-grounding did not invalidate a material contract assumption

## Deferred / not tested here
[heavyweight or independent verification intentionally left for Testing, with reason; "none" if none]

## Flagged for Techplan / Testing
[material assumption break or specialized concern; "none" if none]

## Phase handoff
- Completed: <build target/patch completed or what remains>
- Artifacts: <report path>
- Open / blocked: <material blocker or none>
- Recommended next step: Code Review after initial build; return to requesting phase after patch
- Session recommendation: CONTINUE for another Build iteration while focused; FRESH for Code Review/Testing
- Context pointers: parent Techplan + current task/patch plan + changed files/tests only
```

## Notes

Build is execution, not a second Exploration phase. Patch ownership stays here even when another independent phase discovered the defect.
