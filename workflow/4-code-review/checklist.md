# Code Review Checklist

Run against the current diff. Skip an item only when it is genuinely not
applicable; do not invent findings to make a pass look complete.

## Safety

- [ ] Nullable/optional values are handled where absence is legitimate.
- [ ] Concurrent/async code has no unjustified shared mutable-state/lifecycle hazard.
- [ ] Errors are propagated, surfaced, or explicitly justified rather than silently swallowed.
- [ ] External calls propagate applicable timeout/cancellation context.
- [ ] Resources are released on all applicable return/error paths.
- [ ] Any newly discovered specialized concurrency/perf/security concern missing from the Techplan Test Focus Pointer is reported as Techplan drift.

## Quality

- [ ] No material duplicated logic that should use an existing/shared abstraction.
- [ ] Names/signatures describe behavior clearly.
- [ ] Observability exists at meaningful decision/failure points where target convention expects it.
- [ ] No dead/leftover code from the change.
- [ ] Complexity is proportionate to the problem and local precedent.

## Stack-Specific Best Practices

- [ ] Used `best-practices/index.md` as a clue map: targeted only trigger/security rows relevant to this diff rather than absorbing the full index by default.
- [ ] Opened and applied each matching best-practice authority.
- [ ] Findings cite their matching best-practice source, or the pass states explicitly that no trigger matched.

## Consistency

- [ ] Read the target repo's applicable convention/instruction source.
- [ ] Error handling matches target-repo convention where applicable.
- [ ] Logging/observability matches target-repo convention where applicable.
- [ ] Validation placement/shape matches existing project authority/precedent.
- [ ] New names/constants/messages/structure follow relevant local precedent.

## Scope / authority

- [ ] Review was performed against the actual current diff/changed-file scope, not inferred from the Build report alone.
- [ ] Reviewer did not modify production code; required fixes are expressed as findings/patch plan for Build authority.
