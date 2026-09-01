# 0010 — Claude Code frontend track, Tier 2: subagent phase mapping + protected-file hook

**Status:** Proposed
**Date:** 2026-08-23
**Triggered by:** Following 0006's Tier 1 translations, addressing the higher-value but higher-risk mechanisms (subagents, hooks) — including a concrete governance failure observed during this workspace's own session (a protected-file edit made directly instead of via proposal, caught only on manual review)
**Target area:** harness-optimization
**Target file(s):**
- New: `harness-optimization/claude-code/frontend/subagents.md`
- New: `harness-optimization/claude-code/frontend/hooks-protected-files.md`
- Depends on 0004/0005/0006 being accepted first

## Gap found

**Subagents:** `workflow/`'s "amnesiac contractor" framing — each phase
ideally starts from exactly the context it needs — is currently only a
discipline (an agent is asked to behave as if starting fresh). Claude
Code subagents make this a structural property (a genuinely separate
context window per phase) instead of a behavior the agent has to
maintain on its own. Combined with `best-practices/model-routing.md`'s
existing tier logic and this workspace's fencing/separation-of-authority
concept, a subagent-per-phase mapping is a stronger implementation of an
idea already present in this workspace, not new policy.

**Hooks:** protected-file governance (`best-practices/`'s entire tree,
`workflow/`'s high-ceremony phase files, `harness-optimization/` itself)
is currently enforced only by a line in each tree's `AGENTS.md` — prose
an agent is expected to read and honor. This exact failure mode already
happened during this session's own drafting process: a protected-file
edit (to `best-practices/index.md`) was made directly instead of via
`proposals/`, caught only because of manual review, not prevented by any
mechanism. This is the same class of gap this workspace already
formalized a fix for once (`workflow/2-techplan/retro.md` — a rule
restated as prose gets skipped regardless of model or person) — applied
here one layer up, at the harness level instead of the linter level.

## Proposed change

**`subagents.md`**: one Claude Code subagent per `workflow/` phase, each
with a `tools` list scoped to the minimum that phase's guideline files
actually require (mirroring existing separation-of-authority — e.g. a
code-review subagent should not have `Write` access to what it's
reviewing) and a `model` selected per `model-routing.md`'s tier logic
rather than defaulted. Documents that cross-subagent context handoff
(what a later phase needs from an earlier one) must be explicit — a file
path or identifier passed at invocation — since a genuinely separate
context window doesn't carry information forward implicitly the way a
single long session might.

**`hooks-protected-files.md`**: a `PreToolUse` hook pattern (matcher on
`Edit|Write`, a shell script doing a plain path/glob match against a
protected-path list, exit 2 to block) that enforces the *existing*
protected-file rule mechanically. Explicitly scoped as illustrative
pattern, not a fixed inventory — the protected-path list must track
whatever each tree's own `AGENTS.md` actually declares, since that
remains the real source of truth being enforced, not invented here.

## Rationale

Both files are Tier 2 because getting either wrong has real, mostly
silent blast radius: an under-fenced subagent can act outside its
intended authority; an over-fenced one silently loses context it needed
without an obvious symptom; a wrong hook can either over-block legitimate
work or under-block a real violation while appearing to provide
protection. Both files' checklists explicitly call for testing against
both a should-block and a should-not-block case before trusting either
mechanism, and for keeping hook logic to plain matching rather than
inferred/"clever" pattern detection, which is exactly where a hook
silently stops doing what it appears to do.

The hook file is a direct, concrete response to a real gap observed in
this workspace's own process this session, not a hypothetical — see
`proposals/0001-react-best-practices-category.md`'s note acknowledging
the same direct-edit gap, now given an actual enforcement mechanism
instead of just a documented lapse.

Neither file references a specific target repo; both describe the
reusable mapping/hook pattern generically, per
`harness-optimization/README.md`'s project-agnostic rule.