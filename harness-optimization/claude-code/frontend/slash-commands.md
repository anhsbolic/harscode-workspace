# slash-commands.md (Claude Code, frontend track)

**Tier:** 1 — low risk. A slash command that's wrong simply doesn't run
correctly; there's no blast radius beyond the current turn.

## What this translates

`workflow/`'s phase-kickoff prompt files (e.g. an exploration-kickoff
prompt, a techplan-synthesis prompt) already exist as standalone
Markdown, written to be handed to an agent verbatim at the start of a
phase. This is close to a 1:1 fit for Claude Code's custom slash commands
(`.claude/commands/*.md`) — the translation is closer to a file-format
change than new content.

## Pattern

```md
<!-- .claude/commands/explore.md -->
---
description: Kick off the exploration phase for a new piece of work
---

Follow the exploration guidelines and process defined in this workspace's
`workflow/1-exploration/` directory (see `guidelines.md` for the 3-stage
process and `sniffing-checklist.md` for the five lenses to apply at
Stage 2). Do not skip or merge the stages.

Area(s) to explore: $ARGUMENTS
```

Each phase gets one command. The command body stays a *pointer* into
`workflow/`'s actual guideline files (via reference, not inlined content)
— consistent with this workspace's existing single-source-of-truth
discipline for prompt files. `$ARGUMENTS` carries whatever the invoker
passes after the command name (e.g. `/explore campaign-detail page`).

## Checklist

- [ ] One command per workflow phase, named to match the phase
      (`/explore`, `/techplan`, `/build`, `/code-review`, `/test`) —
      not per-project or per-feature
- [ ] Command body references `workflow/<phase>/` files by path, never
      copies their content inline — if the guideline changes, the
      command doesn't need a separate edit
- [ ] `$ARGUMENTS` is used for the one thing that genuinely varies per
      invocation (what's being explored/built/tested), not for anything
      that should already be fixed by the guideline itself
- [ ] Commands are added to the project repo's own `.claude/commands/`,
      not to this workspace — this file is the reusable pattern, not an
      instance of it (see `harness-optimization/README.md`)