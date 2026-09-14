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

Read and follow {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration-kickoff-prompt.md
in full — it is the canonical entry prompt for this phase and routes to
the phase's guideline files itself. Fill its inputs from this project's
settings and the arguments below. Do not skip or merge its stages.

Area(s) to explore: $ARGUMENTS
```

`{HARSCODE_WORKSPACE_ROOT}` is resolved to this project's actual path
once, when the command is instanced into the target repo (see
`workflow/README.md` § Path Variables Convention).

Each phase gets one command, routed to that phase's canonical root
prompt:

| Command | Canonical prompt |
|---|---|
| `/explore` | `workflow/1-exploration-kickoff-prompt.md` |
| `/techplan` | `workflow/2-1-techplan-synthesis-prompt.md` — then `2-2-techplan-review-prompt.md` and `2-3-techplan-decomposition-prompt.md` only when their own gate questions apply |
| `/build` | `workflow/3-build-prompt.md` |
| `/code-review` | `workflow/4-code-review-prompt.md` |
| `/test` | `workflow/5-testing-prompt.md` |

The command body stays a *pointer* to the canonical prompt (via
reference, not inlined content), per `workflow/README.md` § Canonical
Phase Prompts. Don't point past the prompt at `workflow/<phase>/`
directly — the prompt is what carries the phase's inputs, response-style
setting, and output format, and a command that skips it silently drops
all three. A phase with no root prompt (`6-pull-request/` today) is the
one case where the command points at the phase folder. `$ARGUMENTS`
carries whatever the invoker passes after the command name (e.g.
`/explore campaign-detail page`).

## Checklist

- [ ] One command per workflow phase, named to match the phase
      (`/explore`, `/techplan`, `/build`, `/code-review`, `/test`) —
      not per-project or per-feature
- [ ] Command body references the phase's canonical root `*-prompt.md`
      by path (the phase folder only when no root prompt exists, e.g.
      `6-pull-request/`), never copies its content inline — if the
      prompt or guideline changes, the command doesn't need a separate
      edit
- [ ] `$ARGUMENTS` is used for the one thing that genuinely varies per
      invocation (what's being explored/built/tested), not for anything
      that should already be fixed by the guideline itself
- [ ] Commands are added to the project repo's own `.claude/commands/`,
      not to this workspace — this file is the reusable pattern, not an
      instance of it (see `harness-optimization/README.md`)