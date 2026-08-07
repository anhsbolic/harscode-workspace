# Guidelines

Runs after implementation exists, before it's considered done — either
during active work or right before opening a PR. Three review passes,
in order: Safety, Quality, Consistency.

## 1. Safety Review

> "Review this implementation for: nil/null pointer safety, concurrency
> safety, error handling, resource safety."

Look specifically for:
- Nil/null dereference when a dependency's data can legitimately be
  empty or missing.
- Race conditions in concurrent code — shared mutable state without
  synchronization, goroutines/tasks that outlive their expected scope.
- Errors silently swallowed (caught and discarded, or logged but not
  propagated when the caller needs to know).
- Missing cancellation/timeout propagation in code that calls out to
  another service.
- Resources not released on early-return paths (connections, file
  handles, locks).

## 2. Quality Review

> "Is this code optimized? Maintainable? Readable?"

Look for:
- Duplicated logic that should be extracted into a shared helper.
- Unclear function signatures (e.g. multiple same-typed return values
  with no way to tell which is which without reading the body).
- Naming that doesn't match what the thing actually does.
- Missing observability (no logging at decision points that matter for
  debugging later).

## 3. Consistency Check

> "Does this follow the existing codebase's own patterns?"

This one is NOT generic — it requires reading the target repo's own
convention file (AGENTS.md/README/CONTRIBUTING) first. Don't assume a
pattern from a different project applies here. Check specifically:
- Error handling convention (how errors are constructed/wrapped/typed).
- Logging convention (format, what gets logged at what level).
- Validation convention (where/how input validation happens).
- Naming convention for anything newly introduced (constants, error
  messages, etc.) — consistent with what already exists nearby, not
  just internally consistent with itself.

## Order Matters

Do Safety first — a beautifully consistent, well-named function that
has a nil pointer bug is still broken. Quality and Consistency are
about the code being good to live with; Safety is about the code being
correct at all.
