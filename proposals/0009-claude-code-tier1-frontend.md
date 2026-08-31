# 0006 — Claude Code frontend track, Tier 1: slash commands + skills wrapper

**Status:** Proposed
**Date:** 2026-08-23
**Triggered by:** Following 0004/0005's foundation, translating the two lowest-risk mechanisms first (slash commands, skills) before the higher-risk Tier 2 mechanisms (subagents, hooks)
**Target area:** harness-optimization
**Target file(s):**
- New: `harness-optimization/claude-code/frontend/slash-commands.md`
- New: `harness-optimization/claude-code/frontend/skills-wrapper.md`
- Depends on 0004/0005 being accepted first

## Gap found

Two of this workspace's existing structures have a near-1:1 native
counterpart in Claude Code that isn't being used yet:

1. `workflow/`'s phase-kickoff prompt files are already standalone
   Markdown meant to be handed to an agent verbatim — this is close to a
   file-format change, not new content, to become Claude Code slash
   commands.
2. `best-practices/index.md`'s keyword-trigger table is manually scanned
   today (an agent reads the table, matches a row, opens that file).
   Claude Code Skills auto-discover via a `description` field — the same
   information already sitting in `index.md`'s columns, unused for
   automatic triggering.

Both are low-effort, low-risk translations: worth doing before the
higher-risk Tier 2 work (subagents, hooks), consistent with the tiering
already agreed for this pillar.

## Proposed change

**`slash-commands.md`**: one Claude Code command per `workflow/` phase,
each command body pointing into that phase's actual guideline files by
reference (not inlining content) — preserves this workspace's existing
single-source-of-truth discipline for prompt files rather than creating a
second copy that can drift.

**`skills-wrapper.md`**: one Skill per `best-practices/<category>/<file>.md`,
built mechanically from that file's existing `index.md` row (keywords →
`description`, content → Skill body unchanged). Explicitly notes this
transform is scriptable (read `index.md`, emit one `SKILL.md` per row)
rather than manual per-file authoring, given the row count already
exceeds a dozen entries.

Both files state explicitly that generated artifacts (actual
`.claude/commands/`, `.claude/skills/`) belong in a target repo, not in
this workspace — these two files are the reusable pattern, not an
instance of it.

## Rationale

Both translations are mechanical enough that getting them wrong has no
meaningful blast radius — a broken command just doesn't run; a
non-triggering skill just falls back to today's manual `index.md`
lookup. This matches the Tier 1 designation and is why these are proposed
before the Tier 2 mechanisms (subagents, hooks), which do carry real
blast radius if written wrong.

Neither file references a specific target repo, project, or domain —
both describe the reusable translation pattern only, consistent with
`harness-optimization/README.md`'s project-agnostic-by-construction rule.