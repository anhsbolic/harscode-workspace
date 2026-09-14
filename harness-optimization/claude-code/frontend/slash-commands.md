# slash-commands.md (Claude Code, frontend track)

**Tier:** 1 — low risk. A command is a thin invocation adapter to canonical
Harscode prompts, not a second workflow.

## What this translates

Harscode's root `workflow/*-prompt.md` files are already runnable phase entry
surfaces. Claude Code custom commands should point to them and resolve their
inputs, not copy their instructions.

## Pattern

```md
<!-- .claude/commands/explore.md -->
---
description: Kick off Exploration for a task or authoritative task source
---

Read and follow {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration-kickoff-prompt.md
in full. Resolve its project-level inputs from this project's configuration and
use the invocation arguments as the task requirement/source unless the caller
provided a more explicit mapping.

Task/source to explore: $ARGUMENTS
```

`$ARGUMENTS` is per-invocation input, not a substitute for project-level
`{HARSCODE_WORKSPACE_ROOT}`, `{CODEBASE_CONTEXT}`, target-repo authority, or a
proper `{TASK_PATH}`. The command instance must be able to resolve the canonical
prompt's required inputs instead of silently guessing them.

| Command | Canonical prompt |
|---|---|
| `/explore` | `workflow/1-exploration-kickoff-prompt.md` |
| `/techplan` | `workflow/2-1-techplan-synthesis-prompt.md`; independent review/decomposition only when their own gates apply |
| `/build` | `workflow/3-build-prompt.md` |
| `/code-review` | `workflow/4-code-review-prompt.md` |
| `/test` | `workflow/5-testing-prompt.md` |

A phase with no root prompt (`6-pull-request/` today) may point to its folder
guidance instead.

The command does not decide session continuity. After a phase completes, honor
the canonical prompt's phase handoff and `CONTINUE`/`FRESH` recommendation;
do not hardcode Exploration + Techplan into one command/session merely because
both are planning work.

## Checklist

- [ ] Command body references the canonical root prompt; no copied lifecycle
      instructions.
- [ ] Required project/task inputs can be resolved explicitly; `$ARGUMENTS`
      carries only the per-invocation value(s) the command actually owns.
- [ ] `/explore` treats arguments as task/source by default, not merely an Area
      hint; Area remains optional inside the canonical prompt.
- [ ] Phase gates and phase handoff/session recommendation remain owned by the
      canonical prompt/workflow.
- [ ] Command instances live in the target repo's `.claude/commands/`, not in
      Harscode itself.
