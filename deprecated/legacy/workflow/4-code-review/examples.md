# Examples

Common finding patterns worth specifically hunting for — these recur
across unrelated features, which is why they're worth naming instead of
relying on a generic "review this" pass.

| Pattern | Why it hides | How to catch it |
|---|---|---|
| Silent skip when an error was expected | Looks like a no-op success path | Explicitly test the case where the expected input/dependency is missing entirely |
| Wrong error category (e.g. internal error vs invalid request) | Both "fail", so it's easy to not notice which one fired | Verify the error actually propagates through the app's error-handling layer, not just that *an* error occurred |
| Nil/null pointer when a shared dependency's data is empty | Works fine in the common case where the data exists | Test explicitly with the dependency returning no data |
| Unused parameters left after refactoring | Static analysis usually catches unused *variables*, not unused *parameters* | Manual check — grep for the parameter name inside the function body |
| Duplicated logic not caught automatically | No tool flags "this is basically the same as that other function" | Deliberately ask: "is there a helper-extraction opportunity here?" |
| Stack-specific correctness gap (e.g. GraphQL resolver missing a dataloader, Kafka consumer committing offset before the handler confirms success) | Passes Safety/Quality/Consistency review cleanly — it's not a null check or a naming issue, it's a known failure pattern specific to the technology | Match the diff's technology against `best-practices/index.md` keywords *before* judging it "done"; the matching file's checklist catches what generic review can't |