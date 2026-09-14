# slash-commands.md (Claude Code, backend track)

**Tier:** 1 — low risk. A slash command that's wrong simply doesn't run
correctly; there's no blast radius beyond the current turn.

## What this translates

Same translation as `../frontend/slash-commands.md` (0009) — `workflow/`'s
phase-kickoff prompt files are already standalone Markdown meant to be
handed to an agent verbatim, which is close to a file-format change, not
new content, to become Claude Code slash commands. This file exists
separately from the frontend one only because `harness-optimization/
README.md`'s track-split rule is about the *harness translation*, and
backend adds one command frontend doesn't need (`/domain-sequence`,
Proposal 0026) — not because the core five commands differ in shape.

## Pattern

```md
<!-- .claude/commands/explore.md -->
---
description: Kick off the exploration phase for a new feature
---

Read and follow {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration-kickoff-prompt.md
in full — it is the canonical entry prompt for this phase. Fill its
inputs from this project's settings and the arguments below. Do not
skip or merge its stages.

Area(s) to explore: $ARGUMENTS
```

Same shape for the other four phase commands (`/techplan`, `/build`,
`/code-review`, `/test`) — each body a pointer to that phase's canonical
root `*-prompt.md`, using the same command → prompt mapping as
`../frontend/slash-commands.md`, never to `workflow/<phase>/` directly
(`workflow/README.md` § Canonical Phase Prompts). `$ARGUMENTS` carries
whatever varies per invocation (area to explore, techplan file path,
etc.).

```md
<!-- .claude/commands/domain-sequence.md -->
---
description: Run the domain-level sequencing pre-flight before starting the first feature in a new domain
---

Follow `workflow/0-domain-sequencing-prompt.md` in full — read it first,
it defines what this pass must and must not do (coarse, domain-wide
fencing/dependency check only, not per-feature implementation detail;
explicit lower-confidence caveat required in the output).

Domain to sequence: $ARGUMENTS
```

This sixth command is the one genuine backend-track addition beyond the
five-command pattern `../frontend/slash-commands.md` already
established — it exists because Proposal 0026 added a domain-level
pre-flight step that frontend's translation predates and doesn't (yet)
have an equivalent need for.

## Checklist

- [ ] One command per workflow phase (`/explore`, `/techplan`, `/build`,
      `/code-review`, `/test`), plus `/domain-sequence` for the
      pre-flight step — not per-project or per-feature
- [ ] Command body references the phase's canonical root `*-prompt.md`
      by path (the phase folder only when no root prompt exists), never
      copies its content inline — if the prompt or guideline changes,
      the command doesn't need a separate edit
- [ ] `$ARGUMENTS` is used for the one thing that genuinely varies per
      invocation, not for anything that should already be fixed by the
      guideline itself
- [ ] Commands are added to the project repo's own `.claude/commands/`,
      not to this workspace — this file is the reusable pattern, not an
      instance of it (see `harness-optimization/README.md`)
