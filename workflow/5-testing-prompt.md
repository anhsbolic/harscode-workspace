# Testing Prompt

Independent verification after Build and Code Review.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}`
- `{TASK_PATH}`
- current Approved Techplan
- latest build/patch report
- real interface/entry point(s) where applicable
- target-repo build/lint/test commands

Raw Exploration is **not** a blanket input. Specialized Test Focus rows carry exact evidence anchors to open when needed.

## Prompt

```text
You are independently verifying the current implementation.

Read:
- {HARSCODE_WORKSPACE_ROOT}/workflow/5-testing/guidelines.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/5-testing/checklist.md
- {TASK_PATH}/2-techplan/techplan.md
- latest {TASK_PATH}/3-build/report.md or patch-report-<n>.md
- target repo's actual build/test/entry-point authority

Do not load testing examples by default; open examples.md only for a concrete
recurring-pattern/calibration need.

STEP 0 — SWEEP, DON'T REDO
Treat the Build report's named tests/coverage as claims:
- run/spot-check existing named coverage rather than rewriting equivalent tests;
- close its Deferred/not-tested and Flagged items first;
- identify what still requires independent real-interface/final verification.

TEST FOCUS
Read Techplan §12 Test Focus Pointer. For every relevant row, open the exact
Exploration evidence anchor recorded there—NOT the whole Exploration corpus—
and build the specialized execution plan from that evidence.

If a pointer is missing for an obviously concurrency/perf/security-sensitive
area, report Techplan drift instead of silently inventing the prior decision.

COVERAGE
Verify every §4 rule through the appropriate real/observable interface where
possible. Reuse confirmed existing coverage; spend new effort on missing,
failing, or independently verifiable behavior.

Cover applicable happy, negative, edge, and backward-compatibility cases.
Verify error categories/propagation precisely when error behavior is part of
the contract.

FINAL VERIFICATION
Run the target repo's own required build/lint/test commands. Check migration/
schema collisions when applicable, backward compatibility, and perform a fresh
end-to-end read of the current Techplan for contradictions/gaps. Keep this full
Techplan check during workflow-v2 dogfood; independence is part of the quality
baseline.

Do not fix production code here. Findings needing code changes become a patch
plan and return to Build authority.

Write {TASK_PATH}/5-testing/testing-report-<n>.md and, when needed,
{TASK_PATH}/5-testing/patch-plan-<n>.md.

Report:
## 0. Sweep Summary
## 0a. Test Focus Pointer Execution
[area | evidence anchor opened | specialized verification | result]
## 1. Test Coverage
[rule/scenario | category | observable verification | result]
## 2. Error Verification
## 3. Final Verification
## 4. New Recurring Bug Patterns
## Verdict
Pass | Pass with flagged follow-ups | Fail — send back to Build

## Phase handoff
- Completed: <verification scope + verdict>
- Artifacts: <testing report; patch plan if any>
- Open / blocked: <blocking failures/follow-ups or none>
- Recommended next step: PR when passed; otherwise Build/Patch
- Session recommendation: FRESH/CONTINUE for PR based on context fitness; BUILD authority for patches
- Context pointers: final Techplan + test report + patch plan/final diff as applicable
```

## Notes

Testing is a fresh independent verifier, not a full rerun of every earlier activity. Exact evidence anchors reduce rereading without weakening the specialized-risk rationale.
