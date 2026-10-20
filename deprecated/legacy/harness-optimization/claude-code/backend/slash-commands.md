# slash-commands.md (Claude Code, backend track)

**Tier:** 1 — low risk. A slash command that's wrong simply doesn't run
correctly; there's no blast radius beyond the current turn.

## What this translates

Same translation as `../frontend/slash-commands.md` — `workflow/`'s
canonical phase prompts are standalone Markdown meant to be handed to an
agent at phase start. The command is therefore a thin invocation adapter,
not a second copy of workflow policy.

The backend track exists only for genuine translation differences, not
because the core `/explore`, `/techplan`, `/build`, `/code-review`, and
`/test` lifecycle differs.

## Pattern

```md
<!-- .claude/commands/explore.md -->
---
description: Kick off the exploration phase for a new feature/task
---

Read and follow {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration-kickoff-prompt.md
in full — it is the canonical entry prompt for this phase. Resolve its
project-level inputs from this project's settings and use the arguments
below as the task requirement/source unless the caller mapped them more
explicitly.

Task/source to explore: $ARGUMENTS
```

Same shape for the other core phase commands: each body points to that
phase's canonical root `*-prompt.md`, never past it directly to a phase
folder. `$ARGUMENTS` carries per-invocation input; it is not a substitute
for project-level variables or a valid `{TASK_PATH}`.

The command does not decide whether the next phase shares the same session.
Honor the canonical prompt's phase handoff and `CONTINUE`/`FRESH`
recommendation.

## Optional domain sequencing wrapper

If the target project groups work by domain and
`workflow/0-domain-sequencing-prompt.md` applies, a command may expose it:

```md
<!-- .claude/commands/domain-sequence.md -->
---
description: Run the optional domain-level sequencing pre-flight
---

Follow {HARSCODE_WORKSPACE_ROOT}/workflow/0-domain-sequencing-prompt.md in
full. Resolve its required inputs explicitly; do not infer the entire domain
scope from the argument alone.

Domain/spec input: $ARGUMENTS
```

This wrapper is optional because the **project planning shape** is optional;
it is not inherently a backend-only lifecycle concept. A frontend or mixed
project can expose the same wrapper when its domain planning uses the generic
prompt.

## Checklist

- [ ] Core command bodies reference canonical root prompts and do not copy
      their workflow content.
- [ ] `$ARGUMENTS` supplies the per-invocation value the command owns; required
      project/task inputs remain explicit.
- [ ] `/explore` treats its primary argument as task/source, not Area-only.
- [ ] Phase handoff/session choice remains owned by workflow context rules.
- [ ] `/domain-sequence` exists only when domain-grouped planning applies.
- [ ] Command instances live in the target repo's `.claude/commands/`, not in
      Harscode itself.
