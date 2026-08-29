# Guidelines

Runs after implementation exists, before it's considered done — either
during active work or right before opening a PR. Four review passes,
in order: Safety, Quality, Stack-Specific Best Practices, Consistency.

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

If this pass flags genuinely concurrency-sensitive or security-sensitive
code, cross-check the story's techplan § 12 Test Focus Pointer: does
this area appear there? If the code clearly warrants race/perf/security
coverage but the pointer table doesn't reflect it, report that as a
**techplan-drift finding**, separate from any code-level Safety finding
— the fix is updating the techplan (or confirming it's deliberately out
of scope), not just noting the code issue.

## 2. Quality Review

> "Is this code optimized? Maintainable? Readable?"

Look for:
- Duplicated logic that should be extracted into a shared helper.
- Unclear function signatures (e.g. multiple same-typed return values
  with no way to tell which is which without reading the body).
- Naming that doesn't match what the thing actually does.
- Missing observability (no logging at decision points that matter for
  debugging later).

## 3. Stack-Specific Best Practices Review

> "Does this follow known correctness patterns for the technology it
> touches?"

This one requires an external lookup before it can be judged — same
reason it's a separate pass and not folded into Quality. Steps:

1. Check `best-practices/index.md` and match its trigger keywords
   against the technology/area(s) touched by this diff (Go, PostgreSQL,
   GraphQL, REST API, Kafka, Pub/Sub, Redis).
2. Open only the matching file(s) — don't scan the whole folder.
3. Apply that file's checklist to the diff (e.g. a Kafka consumer
   change → `kafka/consumer-and-offset-management.md`; a new GraphQL
   resolver → `graphql/resolver-n-plus-one.md`).

This is domain knowledge, not project convention — don't substitute a
pattern from a different project's codebase for what the matching
best-practices file actually says. If no keyword matches, this pass is
a no-op; don't force a match that isn't there.

## 4. Consistency Check

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
has a nil pointer bug is still broken. Quality, Stack-Specific Best
Practices, and Consistency are about the code being good to live with;
Safety is about the code being correct at all.

Stack-Specific Best Practices comes after Quality and before
Consistency deliberately: it's domain correctness (is this right *for
this technology*), which is a different question from both "is this
well-built in general" (Quality) and "does this match what's already
here" (Consistency) — and like Consistency, it requires reading an
external reference before it can be judged, not just reading the diff.