# token-optimization.md (harness-agnostic rule)

## Scope

This file states the rule. It does not say how to enforce it in any
particular harness — that translation lives in `<harness-name>/token-
optimization.md` (e.g. `claude-code/token-optimization.md`). This
separation exists so the rule itself has exactly one source of truth
regardless of how many harnesses eventually implement it.

## The rule

```
Default: terse.
  - No filler, no hedging, no restating the question, no sign-off.
  - Applies to explanatory/conversational output — never to code,
    diffs, or configuration content itself.

Exception — full completeness required, compression OFF — whenever
output:
  (a) crosses an audience boundary into human-facing content
      (a summary/digest section, a risk note, a PR description,
      anything a reviewer reads instead of the full underlying detail), OR
  (b) falls inside a section already governed by a formal, named
      self-check checklist in `workflow/` (i.e. a section that exists
      specifically because a prior gap recurred and got converted into
      an explicit mechanical check).
```

## Why this shape, not a flat rule or a per-phase list

**Not a flat "always be terse" rule:** tested against this workspace's own
history in about one minute of thought and immediately produced a
counterexample (a techplan Summary, or any section already protected by a
self-check checklist) — see `techplan/retro.md` for what happens when a
completeness-critical section gets under-specified. A flat rule with no
exception logic would either get manually re-litigated every time someone
hits an exception, or silently compress content this workspace already
went through multiple review passes to make *not* silently drop detail.

**Not a per-phase list (exploration/techplan/code-review/testing/PR each
get their own rule):** violates the same "single source of truth over
phase-split content" principle already established for `best-practices/`.
It also doesn't actually align with phase boundaries — a single phase
(techplan) contains both a zone that needs full completeness (the Summary)
and a zone that's fine to keep terse (the execution-grade detail sections,
which are agent-to-agent consumption, not human-facing). Keying the
exception to phase name would misclassify both zones.

**Why triggers (a) and (b) instead:** both are self-maintaining rather
than a static list that needs manual upkeep. If a future proposal adds a
new self-check-guarded section anywhere in `workflow/`, it's automatically
covered by trigger (b) without this file needing an edit — the exception
is defined by "does this section have a self-check guard," not by naming
every section that currently has one.

## What this file is not

Not a claim that any specific third-party token-compression tool is safe
or effective to install. Tool-specific evaluation (what's been measured,
what's been tried, current verdict) lives in each harness's own
`token-optimization.md`, dated and re-verifiable — those are empirical
claims about fast-moving external tools, which don't belong mixed into a
rule intended to be stable.