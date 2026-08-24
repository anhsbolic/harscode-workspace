# token-optimization.md (Claude Code)

**Last verified:** 2026-08-23 — see `../README.md` for re-verify cadence.

## Enforcement mechanism

The root rule (`../../token-optimization.md`) is enforced in Claude Code
via a `CLAUDE.md` instruction, not via a hook or third-party tool — see
"Third-party tools evaluated" below for why.

```md
## Output style

Default: terse. No filler, no hedging, no restating the question, no
sign-off. Applies to explanatory/conversational text only — never to
code, diffs, or configuration content.

Exception — full completeness required, do not compress:
- Any human-facing summary/digest section
- Any risk note
- Any PR description
- Any section explicitly governed by a self-check checklist elsewhere
  in this workspace's `workflow/`
```

Plain instruction text, not a Skill: a Skill is conditionally triggered by
task-matching, but terseness is meant to be the *default* behavior with
named exceptions — the always-on / exception-driven shape maps to a
standing `CLAUDE.md` instruction, not something that should wait to be
triggered.

## Third-party tools evaluated

**Evaluation methodology used:** don't trust vendor-reported percentages;
prioritize independent, paired A/B benchmarks that report both cost
*and* task-quality delta, not cost alone. This mirrors the
"verifiability over trust" posture already applied elsewhere in this
workspace (an agent's own claim of correctness isn't taken at face value
either).

| Tool | Vendor claim | Independently measured | Verdict (as of 2026-08-23) |
|---|---|---|---|
| **caveman** (compressed-output-style skill) | ~65% output token reduction | ~8.5% measured (paired A/B, task quality unchanged), `lite` mode | Modest real benefit, much smaller than advertised. Not adopted as a dependency — equivalent gain achieved via the plain `CLAUDE.md` instruction above, with zero third-party supply-chain exposure and explicit awareness of the completeness exceptions this tool has no way to know about |
| **RTK / "Rust Token Killer"** (Bash-output compression proxy via `PreToolUse` hook) | 60-90% reduction | **+7.6% more expensive** at low reasoning effort (statistically significant), ~0% at high effort; task quality unchanged | **Not adopted.** Only intercepts `Bash` calls (33-50% hit rate even within Bash in the cited benchmark); `Read`/`Grep`/`Glob` — the tools an agentic coding session actually spends most of its context on — bypass it entirely by design. Net negative or neutral in measured use, plus an external binary running on every session |

Source for the measured figures: an independent paired-trial benchmark
(SkillsBench methodology, Claude Code 2.1.201, `claude-sonnet-5`, dated
2026-07-20). Treat this as one data point, not settled fact — re-run or
re-check before trusting it past the re-verify window above, especially
since both tools are actively changing (RTK in particular ships releases
on the order of days, not months).

## Why "build it ourselves" won over adopting either tool

1. Both measured effects are small-to-negative relative to their
   marketing — neither clears a bar that justifies the dependency.
2. Both are supply-chain exposure (an external binary or marketplace
   plugin executing every session) for a problem the `CLAUDE.md`
   instruction above solves at zero dependency cost.
3. Neither tool has any way to know this workspace's own exceptions
   (audience-boundary content, self-check-guarded sections) — a
   plain-text instruction can express that distinction directly; a
   generic compression tool cannot.

## Re-evaluation trigger

Re-check this file's verdicts if: (a) the re-verify window above has
passed, (b) a new tool claims a measured (not vendor-reported) benefit
above ~20% with unchanged task quality, or (c) Claude Code ships a native
first-party token-optimization feature that would obsolete a third-party
tool comparison entirely.