# slash-commands.md (Claude Code, backend track)

**Tier:** 1 — low risk. This track reuses the frontend command translation
except where a backend-specific command genuinely exists.

## Shared phase commands

Use `../frontend/slash-commands.md` for `/explore`, `/techplan`, `/build`,
`/code-review`, and `/test`. The same canonical Harscode prompts and input
contracts apply to frontend and backend.

In particular, `/explore` passes the task requirement/source as its primary
per-invocation argument; it does not reinterpret `$ARGUMENTS` as an Area-only
value. Session continuity remains owned by the canonical phase handoff.

## Optional domain sequencing command

When the target project actually groups work by domain and the generic
`workflow/0-domain-sequencing-prompt.md` applies, a command may route to it:

```md
<!-- .claude/commands/domain-sequence.md -->
---
description: Run the optional domain-level sequencing pre-flight
---

Follow {HARSCODE_WORKSPACE_ROOT}/workflow/0-domain-sequencing-prompt.md in full.
Resolve its required inputs explicitly; do not invent domain scope from the
argument alone.

Domain/spec input: $ARGUMENTS
```

This is an optional wrapper around an existing generic workflow prompt, not a
backend lifecycle rule. A frontend/domain project could expose the same wrapper
if the project planning structure requires it.

## Checklist

- [ ] Shared phase commands inherit the canonical mapping/input semantics from
      `../frontend/slash-commands.md`.
- [ ] `/domain-sequence` exists only where the project uses domain-grouped
      planning; otherwise omit it.
- [ ] Command wrappers do not copy or redefine workflow policy.
- [ ] Command instances live in the target project, not Harscode.
