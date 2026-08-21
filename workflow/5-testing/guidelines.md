# Guidelines

Testing catches what static review misses. This runs after code review,
using the actual interface (API call, CLI, UI) — not just reading code.

## Process

1. **Test every scenario from the techplan's Rules & Validation section
   (§ 4)** using the real interface — not a mental walkthrough. If a
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
