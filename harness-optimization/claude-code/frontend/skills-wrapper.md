# skills-wrapper.md (Claude Code, frontend track)

**Tier:** 1 — low risk. A skill that never triggers simply falls back to
current behavior (manual `index.md` lookup); no blast radius.

## What this translates

`best-practices/index.md` is a manually-scanned keyword table: an agent
matches the area it's working on to a row, then opens that file. Claude
Code Skills auto-discover based on a `description` field evaluated against
the current task, at ~100 tokens of overhead per skill regardless of
whether it fires — this replaces manual table-scanning with automatic,
progressive-disclosure loading (full file content only loads once the
skill actually triggers).

## Pattern

Each `best-practices/<category>/<file>.md` becomes one Skill. The
`index.md` row this workspace already maintains supplies everything
needed — this is a mechanical transform, not new authoring:

```md
<!-- .claude/skills/<file-slug>/SKILL.md -->
---
name: <file-slug>
description: >
  Use when working with <the exact keyword list from index.md's
  "Trigger keywords" column for this file>.
---

<the full content of best-practices/<category>/<file>.md, unchanged>
```

`index.md`'s existing columns map directly:
- Trigger keywords → the `description` field's task-matching text
- File content → the Skill body, verbatim, no rewriting
- Security Concern Map entries → worth a short prefix line in the
  security-critical skills' description (e.g. "security-critical:") so
  the match signal is stronger for that subset

## Checklist

- [ ] Skill `description` is built from `index.md`'s keyword column, not
      re-invented — keeps the two in sync by construction rather than by
      discipline
- [ ] Skill body is the best-practices file's content unchanged — this is
      a wrapping transform, not a rewrite; if the underlying file changes
      via its own proposal process, the skill just needs its body
      re-copied, not re-authored
- [ ] One skill per file, not one skill per category — a category-level
      skill would load everything in the category regardless of which
      specific concern actually matched, defeating the point of
      progressive disclosure
- [ ] This wrapping can be scripted (read `index.md`, emit one
      `SKILL.md` per row) rather than done by hand per file — worth
      automating given the row count already exceeds a dozen
- [ ] Skills are generated into the target repo's own `.claude/skills/`,
      not committed to this workspace — same instancing rule as
      `slash-commands.md`