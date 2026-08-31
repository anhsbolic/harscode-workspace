# Guidelines

Testing catches what static review misses. This runs after code review
and any implementation loop that followed it (e.g. a rebuild driven by
review findings) — using the actual interface (API call, CLI, UI), not
just reading code.

## Process

0. **Read the latest implementation report first** (`3-build/report.md`, 
   `{TASK_PATH}/3-build/report.md` (or the most recent `patch-report-<n>.md` if the task looped back 
   through the implementation after code review). Treat its rule-coverage 
   table and named tests as *claims*, not settled fact — this step exists 
   so this phase doesn't silently redo work already proven, and doesn't
   silently trust work that was only claimed.

   - **Spot-check, don't rewrite.** For rules already backed by a named
     test, run the existing suite and confirm it still passes. Don't
     write a second test that exercises the same rule the same way —
     that's pure cost with no new signal.
   - **Close the report's own gaps first.** A good implementation
     report has a "what is not tested, and why" section — that's the
     highest-value place to spend this phase's effort, because it's a
     gap the implementer already flagged, not one you have to go find.
   - **Then do what only this phase can do**: real-interface exercise
     (not a unit test through a fake), backward compatibility, migration
     collision, and a fresh end-to-end techplan read for contradictions
     earlier passes might have introduced. These are structurally
     different from unit-level verification — no report claim
     substitutes for them.

   This phase is a final sweep, not a rerun: confirm what's already
   proven, close what was flagged, then cover the ground nothing else
   could.

   - **Extract the Test Focus Pointer.** Read techplan § 12's Test
     Focus Pointer table (`workflow/2-techplan/rules.md` § 9). For each
     area still marked relevant, cross-check the raw exploration docs'
     Sniffing Checklist Risk findings for the concrete detail behind
     *why* it's flagged, then build a concrete Test Execution Plan:
     - Concurrency/race: scope to the specific package(s)
       (`go test -race ./internal/<area>/...`), never a blanket
       `./...` sweep — see `best-practices/go/testing-concurrency.md`.
     - Perf/load: concrete scenario + threshold, not "check
       performance."
     - Security: the specific vulnerability class relevant to the area
       (e.g. an auth area gets IDOR/session checks, not a generic pass).
     - If any deliberately-slow primitive (bcrypt, other KDFs) is
       exercised, confirm the test uses a test-appropriate cost/work
       factor before running it under load or concurrency — see
       `best-practices/go/expensive-primitives-in-tests.md`.
     - If the pointer table is empty but you (as reviewer) suspect a
       genuinely sensitive area was scoped out silently — that's a
       techplan drift signal, not a testing-phase gap. Flag it back
       rather than quietly adding the test yourself; the techplan
       should record the decision either way
       (`workflow/2-techplan/guardrails.md` § 12).

1. **Test every scenario from the techplan's Rules & Validation section
   (§ 4)** using the real interface — but per step 0, this means
   confirming coverage exists and is real, not re-deriving every test
   from a blank slate when a named test already proves it. If a
   scenario in techplan § 4 can't be exercised through the real
   interface, that's itself worth flagging (either the rule is
   unreachable, or there's a missing entry point).

2. **Cover all four categories, not just the happy path:**
   - Happy path: valid input → expected success
   - Negative cases: missing required fields, invalid input, dependency
     failures
   - Edge cases: empty input, boundary values, nulls
   - Backward compatibility: old clients/old data still behave as
     expected

3. **Verify error responses precisely**, not just "an error happened":
   - Does the error category match expectation (e.g. client error vs
     server error)?
   - Is the error message something a caller can actually act on?
   - Does the error propagate correctly through the app's error-handling
     layer (not swallowed or re-wrapped into something generic)?

4. **When a bug is found**, don't just fix it — check `examples.md` for
   whether it matches a known recurring pattern, and note a new one in
   this file if it's genuinely new (see Threshold note below).

## Final Verification Before Considering Done

Run the target repo's own build/lint/test commands (read its own
README/Makefile — don't assume `go build`/`npm test`/etc., that's
project-specific). Then check:

- [ ] Every rule in techplan § 4 has a corresponding test
- [ ] Migration/schema version doesn't collide with anything landed
      since the techplan was written
- [ ] Backward compatibility explicitly verified, not just assumed
- [ ] A fresh read of the techplan end-to-end for gaps or
      contradictions the earlier passes might have introduced

## Threshold for Adding to examples.md

Add a new bug pattern entry only if it's the kind of thing that could
plausibly recur in unrelated features (a category of mistake), not a
one-off bug specific to this ticket's logic.