# token-optimization.md (Claude Code)

**Last verified:** 2026-08-23 — see `../README.md` for re-verify cadence.

## What this translates

The semantic source is `../token-optimization.md`. Claude Code may enforce that
rule through a persistent `CLAUDE.md` instruction; this file does not create a
second output policy.

A compact translation is:

```md
## Output style

Default explanatory/process narration is direct and terse:
- no filler, hedging, repeated request restatement, routine tool narration, or sign-off;
- explain material trade-offs/human gates when that explanation affects a decision;
- do not mechanically shorten code, diffs, configuration, or required structured artifacts.

Deliverables remain complete for their audience/next phase. Terse process is
not permission to make Techplans, review/testing findings, human reports, or PR
descriptions incomplete.

Context loading is a separate concern. Follow Harscode
`workflow/context-management.md`; do not compensate for broad context loading
by making the final artifact skeletal.
```

Plain persistent instruction text is preferable to a conditionally-triggered
Skill for this default behavior. Do not install the same standing rule in
multiple Claude surfaces at once.

## Third-party tools evaluated

**Evaluation methodology used:** don't trust vendor-reported percentages;
prioritize independent, paired A/B benchmarks that report both cost and
quality delta.

| Tool | Vendor claim | Independently measured | Verdict (as of 2026-08-23) |
|---|---|---|---|
| **caveman** (compressed-output-style skill) | ~65% output token reduction | ~8.5% measured (paired A/B, task quality unchanged), `lite` mode | Modest real benefit, much smaller than advertised. Not adopted as a dependency; the persistent instruction gives the needed behavior without third-party supply-chain exposure. |
| **RTK / "Rust Token Killer"** (Bash-output compression proxy via `PreToolUse` hook) | 60-90% reduction | **+7.6% more expensive** at low reasoning effort (statistically significant), ~0% at high effort; task quality unchanged | **Not adopted.** It intercepts only part of tool traffic and measured neutral-to-negative cost while adding an external binary to the execution path. |

Source for the measured figures: an independent paired-trial benchmark
(SkillsBench methodology, Claude Code 2.1.201, `claude-sonnet-5`, dated
2026-07-20). Treat this as one dated data point; re-check before relying on it
past the verification window.

## Why no compression dependency is recommended

1. Measured benefit is small-to-negative relative to the added dependency.
2. Supply-chain/runtime exposure is unnecessary for a behavior expressible as
   persistent instruction text.
3. Generic compression cannot know which Harscode artifacts must remain
   semantically complete.
4. Output compression does not solve broad or redundant input-context loading;
   that is governed separately by `workflow/context-management.md`.

## Re-evaluation trigger

Re-check if the verification window passes, a tool shows a meaningful measured
quality-preserving benefit, or Claude Code ships a first-party mechanism that
changes this trade-off.
