# Testing Prompt

Independent verification after Build and Code Review. Testing confirms observable correctness and closes verification gaps; it is not a replay of every earlier phase.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — path to this Harscode workspace, used to resolve Testing and matching best-practice guidance.
- `{TASK_PATH}` — root working directory for this task. Testing artifacts are written under `{TASK_PATH}/5-testing/`.
- Current Approved `{TASK_PATH}/2-techplan/techplan.md` — Rules & Validation defines required behavior; the Testing Checklist records planned evidence/primary ownership/rationale and the Test Focus Pointer carries specialized evidence pointers.
- Latest relevant build/patch report under `{TASK_PATH}/3-build/` — Step 0 treats its named tests/coverage as claims to verify and its deferred/flagged items as priority gaps.
- Real observable interface/entry point(s) where the product exposes one: API route, CLI command, UI flow, job/event boundary, or equivalent. If no direct external interface applies, use the nearest meaningful observable boundary and state why.
- Target-repo build/lint/test authority — the actual README/Makefile/package scripts/CI-equivalent source that defines required final commands. Do not assume generic commands.

Raw Exploration is **not** a blanket input. Specialized Test Focus rows must carry exact evidence anchors; Testing opens those specific sources when the underlying risk rationale is needed.

## Prompt

```text
You are independently verifying the current implementation after Build and
Code Review.

Read:
- {HARSCODE_WORKSPACE_ROOT}/workflow/5-testing/guidelines.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/5-testing/checklist.md
- {TASK_PATH}/2-techplan/techplan.md
- latest relevant {TASK_PATH}/3-build/report.md or patch-report-<n>.md
- target repo's actual build/test/entry-point authority

Do not load testing examples by default; open examples.md only for a concrete
recurring-pattern/calibration need.

Process narration is terse; the testing report is complete evidence.

STEP 0 — SWEEP, DON'T REDO
Treat the Build report's named tests/coverage as claims:
- run/spot-check existing named coverage rather than rewriting equivalent tests;
- close its Deferred/not-tested and Flagged items first;
- execute verification whose Techplan primary owner is Testing;
- identify what still requires independent real-interface/final verification.

Do not trust a Build claim merely because it is written, and do not redo a
proven test from scratch merely because Testing is a fresh session.

Use the Techplan's `Why / risk if skipped` rationale to decide the minimum
credible independent execution. A tool name is not a ritual: run the evidence
because the approved contract/target-repo requirement/risk justifies it.

When re-entering Testing after a narrow patch, verify the affected gap/finding
first. Re-run broad/final suites when they are assigned to Testing by the
Techplan/target repo, when the patch materially changes the relevant risk/scope,
or when a broader suite is necessary to establish final compatibility. Do not
replay unrelated expensive checks solely because another Testing round began.

TEST FOCUS
Read the Techplan Test Focus Pointer. For every row still marked relevant,
open the exact Exploration evidence anchor recorded there — NOT the whole
Exploration corpus — and recover the concrete reason/detail needed to design
the specialized verification.

Build a concrete execution plan appropriate to the flagged concern (for
example scoped race/concurrency coverage, a performance scenario + threshold,
or a security check matched to the actual authority boundary). Route to
matching best-practice files through
{HARSCODE_WORKSPACE_ROOT}/best-practices/AGENTS.md only when the concern
triggers them.

If a pointer is missing for an obviously concurrency/perf/security-sensitive
area, report Techplan drift instead of silently inventing the prior decision.

COVERAGE
Verify every Rules & Validation rule through the appropriate real/observable
interface where possible. Reuse confirmed existing coverage; spend new effort
on missing, failing, stale, or independently observable behavior.

Respect the Testing Checklist's primary ownership:
- Testing-owned rows require independent final evidence here unless an
  authoritative target-repo mechanism already supplies equivalent current
  evidence and the report can cite it credibly;
- Build-owned rows may be spot-checked according to risk rather than blindly
  rerun in full;
- Human-owned rows must remain an explicit external decision/gate; agent
  automation cannot mark them passed.

Cover applicable:
- happy path;
- negative cases;
- edge/boundary cases;
- backward compatibility.

Verify error category, caller-visible/actionable behavior, and propagation when
error semantics are part of the contract. If a contracted rule cannot be
exercised through a meaningful observable entry point, report that mismatch
instead of silently marking it covered.

FINAL VERIFICATION
Run the target repo's own required final build/lint/test commands according to
its authority. Check migration/schema collision when applicable, backward
compatibility, and broader-suite coverage when a cross-cutting change/target-
repo rule requires it.

Perform a fresh end-to-end read of the current Techplan for contradictions/gaps;
keep this whole-contract check during the initial workflow-v2 validation runs
because independence is part of the current quality baseline.

Do not fix production code here. Findings needing code changes become a patch
plan and return to Build authority; affected verification must be rerun after
the patch according to the proportional re-entry rule above.

Write:
- {TASK_PATH}/5-testing/testing-report-<n>.md
- {TASK_PATH}/5-testing/patch-plan-<n>.md when code changes are required

Increment <n> per testing round and preserve earlier evidence.

Every durable Testing artifact must start with compact provenance using only
known/exposed values: Phase, Author, Created/Updated, and where safe/available
Model, Reasoning, Session, target revision, and workflow revision. Do not
invent missing metadata or persist account/credential identifiers. Git history
is the default version history.

Report format:

## 0. Sweep Summary
- Confirmed: <rule/scenario → existing test/verification → result>
- Closed from prior gap/deferred list: <gap → verification/result>
- Still requires fresh Testing: <item → why>

## 0a. Test Focus Pointer Execution
| Area | Evidence anchor opened | Specialized verification | Result |
|---|---|---|---|

If no Test Focus row applies, say so. If a sensitive area appears to be
missing from the pointer, record it explicitly as Techplan drift.

## 1. Test Coverage
| Rule / scenario | Category | Observable verification | Result |
|---|---|---|---|

Cite Rules & Validation rule IDs where applicable. Do not silently omit an
unexercisable rule.

## 2. Error Verification
| Error case | Expected behavior/category | Actual | Actionable/propagated correctly? |
|---|---|---|---|

Use `N/A — reason` when the contract genuinely has no error path exercised in
this round.

## 3. Final Verification
- Target repo required final build/lint/test commands: <command/evidence + result>
- Broad checks intentionally not rerun: <check + reason/risk ownership; "none" if none>
- Migration/schema collision: <result or N/A — reason>
- Backward compatibility: <evidence/result or N/A — reason>
- Broader-suite requirement for cross-cutting change: <result or N/A — reason>
- Fresh Techplan consistency read: <gap/contradiction found or none>

## 4. New Recurring Bug Patterns
Only reusable categories belong here. Ticket-specific defects stay in this
report; do not grow examples.md for every bug.

## Verdict
Pass | Pass with flagged follow-ups | Fail — send back to Build

If not a clean Pass, distinguish blocking failures from non-blocking follow-up
and state whether each is a new gap or a regression of previously claimed
coverage.

## Phase handoff
- Completed: <verification scope + verdict>
- Artifacts: <testing report; patch plan if any>
- Human decision: <human-owned acceptance/decision needed now or "none">
- Open / deferred: <blocking failures/follow-ups or "none">
- Recommended next step: PR when passed and human gates are satisfied; otherwise Build/Patch using the specific patch plan
- Session transition: if patching, explicitly say whether to return to the existing healthy Build session or start a fresh Build/Patch session and why; for PR, state whether a fresh session is useful based on context fitness
- Context pointers: final Techplan + test report + patch plan/final diff as applicable
```

## Notes

- Testing is a fresh independent verifier, not a full rerun of every earlier activity.
- Runtime instructions refer to evolving Techplan sections by semantic name rather than remembered ordinal number.
- Exact evidence anchors reduce rereading without weakening specialized-risk rationale.
- The fresh whole-Techplan verification remains deliberately conservative during the initial workflow-v2 validation runs; narrow it only after evidence shows quality is preserved.
- Verification economy means justified evidence, not fewer tests by default. If a broad check is genuinely release-critical, run it once in the phase that owns the final evidence rather than ceremonially repeating it everywhere.
