# Build Prompt

Manual-invoke prompt for the build/patch implementation loop — the
tight edit → run → fix cycle after a techplan is approved, one
iteration/scope slice at a time.

## Inputs required before running

- `{WORKSPACE_ROOT}` — path to this harscode-workspace's content
  relative to (or as an absolute path from) your project. Set once per
  project; see `workflow/README.md` § Path Variables Convention.
- `{TASK_PATH}` — root working directory for this task in the target
  repo. Set once per task; see root `README.md` § Task Working
  Directory Structure.
- Build target: `{TASK_PATH}/2-techplan/tasks/<task-file>.md` if
  decomposition ran, otherwise `{TASK_PATH}/2-techplan/techplan.md`
  directly. § 4 (Rules & Validation) and § 10-11 (Implementation
  Details) are the contract to build against, whichever file it's in.

## Prompt

```
You are implementing against an approved techplan, one iteration of
the build/patch loop at a time. Don't revisit architectural decisions
already made in the techplan — if something genuinely doesn't hold as
written, stop and report it instead of silently working around it.

Guidance folder for this phase: {WORKSPACE_ROOT}/workflow/3-build —
guidelines.md and checklist.md referenced below resolve relative to
this.

Response style: keep your own narration minimal during this
iteration — do the work efficiently, don't narrate each step. The
output format below is the one place to be complete
({WORKSPACE_ROOT}/workflow/README.md § Response Style By Phase).

Build target: {TASK_PATH}/2-techplan/tasks/<task-file>.md if
decomposition ran, otherwise {TASK_PATH}/2-techplan/techplan.md
directly. One task per iteration when tasks exist; the whole techplan
in one go when they don't — don't ask for a separate scope on top of
that, the right-sized unit of work was already decided at
decomposition's Step 0 gate (or by its absence).

Test scope for this loop — fixed, not negotiable per task:
{file:{WORKSPACE_ROOT}/workflow/3-build/guidelines.md#default-test-scope-always-regardless-of-techplan-content}

Full checklist: {file:{WORKSPACE_ROOT}/workflow/3-build/checklist.md}

---

Write your output below to {TASK_PATH}/3-build/report.md for the
initial build, or {TASK_PATH}/3-build/patch-report-<n>.md if this
iteration is executing a patch plan from code-review or testing (see
root README.md § Task Working Directory Structure) — increment <n>
per patch, don't overwrite a previous one.

Output format:

## What changed
[files touched, one line each]

## Tests run
[test name/pattern → category (unit/mocked/API-contract) → result]
Confirm explicitly: no `-race`, perf/load, or security-class test was
run in this iteration.

## Contract check
- [ ] This iteration satisfies its build target in full (the task
      file's scope, or techplan § 4 in full if there's no task file)
- [ ] No contract assumption broke — or, if one did, flagged below
      instead of worked around

## Flagged for techplan/testing review (if any)
[Concurrency/perf/security concern noticed but not tested here, or a
contract assumption that didn't hold — one line each]
```

## Notes

- This prompt does not decide which model runs it — see
  `best-practices/model-routing.md` (draft) for tier × stage routing.
- This fills a real structural gap: `workflow/` numbers phases
  1 (exploration) → 2 (techplan) → 4 (code-review) → 5 (testing) →
  6 (pull-request), with no formal phase 3 (build) guidance in this
  workspace despite target repos already using a `3-build/` path
  convention for reports (see
  `best-practices/go/examples/integration-testing-setup.md`). This
  fills that gap with the minimum ceremony the loop's stakes warrant —
  a fixed test-scope boundary and a flag-back mechanism — nothing
  heavier, consistent with "weight matches stakes."
- Project-specific build conventions (token-terseness instructions,
  build tool invocation, etc.) still belong in the target repo's own
  `AGENTS.md`/`CLAUDE.md`, not here — this file only owns the one
  cross-project rule this workspace has evidence for: the default test
  tier boundary.