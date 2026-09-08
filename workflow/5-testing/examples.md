# Examples

Recurring bug pattern log. Append new entries as they're found — see
`guidelines.md` § Threshold for when a bug is worth adding here vs just
fixing it.

| Bug Pattern | How It Hides | How to Catch It |
|---|---|---|
| Silent skip when an error was expected | Looks like a successful no-op | Test the case where the expected entry/dependency is missing entirely |
| Wrong error category returned (e.g. server error instead of client error) | Both surface as "an error happened" | Verify the specific error code/category through the actual error-handling layer |
| Nil/empty dependency data not handled | Works in the common case, breaks when a dependency legitimately returns nothing | Explicitly test with the dependency returning empty/null |
| Combined-change scenarios not tested (one field that should trigger re-validation + one that shouldn't, changed together) | Single-field tests all pass individually | Test scenarios where a "should trigger" and "should not trigger" change happen in the same request |
| A stack-specific "fix" (e.g. adding `ShouldQueue`) changes async/delivery behavior without re-checking the infra assumption the original design decision was based on | The change looks like a strict improvement in isolation, and the test suite's own environment config (e.g. a hardcoded sync queue override) makes the regression invisible to the test runner | Diff the change against the techplan's Decision Log for any entry it touches, and check the *real* env/infra config (not just the test config) for the assumption that decision was conditioned on |
| `SELECT ... FOR UPDATE` used to serialize "invalidate old, insert new" logic locks nothing when the query matches zero rows, so two concurrent first-time inserts both succeed | Passes every functional/sequential test (there's always a "before" row to lock when tests run one request at a time); only manifests when two requests race with no pre-existing row to lock | Explicitly test the *zero-prior-state* concurrent case, not just "two requests when one valid row already exists" — run the exact SQL/logic with two overlapping transactions/sessions against an empty starting state |
