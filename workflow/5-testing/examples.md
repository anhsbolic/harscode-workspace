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
