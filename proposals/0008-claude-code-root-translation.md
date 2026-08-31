# 0005 — Claude Code root translation: disclaimer convention + token-optimization enforcement

**Status:** Proposed
**Date:** 2026-08-23
**Triggered by:** First harness added under `harness-optimization/`, following 0004's acceptance; immediate need to enforce the token-optimization rule in a concrete harness and record the evaluation of two third-party candidates (caveman, RTK)
**Target area:** harness-optimization
**Target file(s):**
- New: `harness-optimization/claude-code/README.md`
- New: `harness-optimization/claude-code/token-optimization.md`
- Depends on 0004 (`harness-optimization/README.md`, `token-optimization.md`) being accepted first

## Gap found

0004 establishes the harness-agnostic token-optimization rule but
deliberately doesn't say how any specific harness enforces it — that
split was intentional (rule stability vs harness-specific, fast-moving
detail). Without this proposal, the rule has no concrete Claude Code
implementation, and the evaluation of caveman/RTK (done as part of this
same discussion) had nowhere durable to live.

## Proposed change

**`claude-code/README.md`** — the mandatory disclaimer this workspace now
requires of every harness subfolder (effective-as-of, last-verified,
re-verify cadence), plus a short index of what lives under `claude-code/`.

**`claude-code/token-optimization.md`** — enforces 0004's rule via a
`CLAUDE.md` instruction snippet (plain text, not a Skill — terseness is
default behavior with named exceptions, not a conditionally-triggered
task). Also records dated, sourced verdicts on two evaluated third-party
tools:

- **caveman**: vendor claim ~65% output-token reduction; independently
  measured ~8.5% (task quality unchanged) — real but modest, not adopted
  as a dependency since the equivalent gain is achievable via the
  `CLAUDE.md` instruction alone
- **RTK**: vendor claim 60-90%; independently measured +7.6% *more*
  expensive at low reasoning effort, ~0% at high effort — not adopted;
  only intercepts `Bash` calls and misses `Read`/`Grep`/`Glob`, which
  dominate an agentic coding session's context cost

Both verdicts cite a specific independent benchmark (paired A/B,
SkillsBench methodology, dated 2026-07-20) rather than vendor marketing,
consistent with the evaluation methodology stated in the file itself:
prioritize measured cost *and* task-quality delta over vendor-reported
percentages.

## Rationale

**Why build the token-optimization enforcement ourselves rather than
adopt either tool:** both measured effects are small-to-negative relative
to marketing claims; both introduce supply-chain exposure (external
binary or marketplace plugin executing every session) for a problem a
zero-dependency `CLAUDE.md` instruction already solves; and critically,
neither tool has any way to know this workspace's own audience-boundary
and self-check-guard exceptions — a plain instruction can express that
distinction directly, a generic compression tool cannot.

This is explicitly framed as one data point, not settled fact — the file
includes an explicit re-evaluation trigger (verify-window lapse, a new
tool clearing a real bar, or Claude Code shipping first-party token
optimization) so the verdict doesn't calcify past its useful life, same
posture already used for `best-practices/model-routing.md`.

Nothing in either file references a specific target repo; the
`CLAUDE.md` snippet and tool verdicts apply to any project using this
workspace under Claude Code.