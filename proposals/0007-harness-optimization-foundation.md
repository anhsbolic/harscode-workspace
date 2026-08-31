# 0004 — New `harness-optimization/` pillar: governance + harness-agnostic token-optimization rule

**Status:** Proposed
**Date:** 2026-08-23
**Triggered by:** Discussion of optimizing this workspace's usage under specific agent harnesses (Claude Code, OpenCode CLI) — surfaced that "how a harness executes/enforces workflow and best-practices decisions" doesn't fit cleanly into either existing pillar, and that a token-optimization default needed a stable, harness-independent home before any harness-specific enforcement could be written
**Target area:** new top-level directory
**Target file(s):**
- New: `harness-optimization/README.md`
- New: `harness-optimization/AGENTS.md`
- New: `harness-optimization/token-optimization.md`

This proposal establishes the pillar and its one cross-harness rule.
Harness-specific translations (Claude Code subagents, hooks, skills,
enforcement of this rule) are separate proposals (0005-0007) that depend
on this one being accepted first.

## Gap found

Two related gaps surfaced in the same discussion:

1. **No home for harness-execution knowledge.** `workflow/` describes what
   to do by phase; `best-practices/` describes what's correct by
   technology. Neither is the right place for "how does a specific agent
   harness (Claude Code, OpenCode) actually express phase boundaries,
   protected-file enforcement, or best-practices discovery as native
   mechanism (subagent, hook, skill)?" Forcing this content into
   `workflow/` would tie phase guidance to one harness's implementation
   details; forcing it into `best-practices/` mixes process-execution
   concerns into what's meant to be technology-domain knowledge.

2. **No stable home for a token-optimization default.** Evaluating
   whether third-party token-compression tools are worth adopting
   surfaced that any resulting rule needs to (a) not be harness-specific
   (the underlying "when is terseness safe vs risky" question doesn't
   depend on which harness is running), and (b) not be a flat rule — this
   workspace's own history (`techplan/retro.md`, the Summary/self-check
   pattern from proposals 0001-0003) immediately produces a
   counterexample to "always be terse."

## Proposed change

**New pillar**, `harness-optimization/`, governed identically to
`best-practices/` (agent-protected, proposal-gated) — not lighter-weight,
because content here is often executable (hooks, subagent tool
restrictions) rather than descriptive prose, and a wrong hook can silently
over- or under-block with no visible symptom.

**Core discipline, stated in `README.md`:** translation only, never
policy. If a file here would require inventing a new rule not already
established in `workflow/` or `best-practices/`, that's a signal the rule
belongs in one of those pillars first, as its own proposal.

**Structure convention:** `harness-optimization/<harness-name>/`, with an
optional `<track>/` subfolder only where a harness's translation genuinely
differs by track (e.g. which subagents exist for frontend vs backend).
Content that doesn't vary by track (like token-optimization enforcement)
stays at the harness root, not duplicated per track.

**Mandatory disclaimer convention:** every `<harness-name>/README.md`
must state "effective as of / last verified / re-verify" — harness
features move faster than this workspace's other content, and unverified
content past its window should be treated as a hypothesis, following the
same posture already used for `best-practices/model-routing.md`.

**The token-optimization rule itself** (`token-optimization.md`, root
level, harness-agnostic):
```
Default: terse (explanatory/conversational output only — never code,
diffs, or config content).

Exception, full completeness required:
  (a) output crossing an audience boundary into human-facing content
      (summary/digest, risk note, PR description), OR
  (b) output inside a section already governed by a formal self-check
      checklist in workflow/
```
Both exception triggers are defined structurally (does this content cross
an audience boundary; is this section self-check-guarded) rather than as
a static named list — self-maintaining as `workflow/` gains new
self-check-guarded sections in future proposals, no edit to this file
required.

## Rationale

The pillar boundary mirrors an ordering discipline this workspace already
enforces elsewhere (agents execute, humans own the guidance;
`best-practices/` stays generic while target-repo specifics live in the
target repo's own `AGENTS.md`) — applied here to a third axis: harness
mechanics stay separate from both process knowledge and domain knowledge,
so a harness config file is never the place a policy question gets
decided.

The token-optimization rule's two exception triggers were chosen over
both a flat rule (fails immediately against this workspace's own
Summary/self-check history) and a per-phase list (misclassifies techplan,
which contains both a completeness-critical zone and a safely-terse zone
within the same phase, and violates the existing "single source of truth
over phase-split content" principle).

Nothing in any of these three files is project- or harness-specific;
`<harness-name>/` subfolders (starting with `claude-code/`) are where
concrete translation happens, proposed separately.