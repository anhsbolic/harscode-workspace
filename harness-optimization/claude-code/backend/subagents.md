# subagents.md (Claude Code, backend track)

**Tier:** 2 — higher risk than Tier 1. A subagent's tool restrictions and
context isolation are load-bearing: get the tool list wrong and either an
agent can do something it shouldn't (under-fenced), or a phase silently
loses information it needed because it wasn't explicitly passed in
(over-isolated). Test each mapping in a low-stakes run before trusting it.

## What this translates

Same underlying idea as `../frontend/subagents.md` (0010) — `workflow/`'s
"amnesiac contractor" framing maps onto Claude Code subagents as a
genuinely separate context window per phase, one subagent per
`workflow/` phase, `tools` scoped to the minimum, `model` chosen per
`best-practices/model-routing.md`. Read that file first for the shared
reasoning; this file only states where the backend translation actually
differs, per `harness-optimization/README.md`'s rule that a track split
exists only where the translation genuinely differs, not by default.

## Where backend genuinely differs from frontend

1. **`builder` needs `Bash`, not just `Read`/`Write`.** Running
   migrations, the framework's CLI tooling, and the test suite as part
   of the tight build→run→fix loop (`workflow/3-build/`) is normal
   backend build activity in a way that doesn't map the same way onto a
   frontend build subagent (which `../frontend/subagents.md` doesn't
   scope `Bash` for). Don't copy frontend's `builder` tool list verbatim
   — it under-fences a backend build subagent that needs to actually run
   migrations and tests to iterate.
2. **Every subagent's system prompt must reference the target repo's
   own File-Path-Fencing-Tier-0-class declaration**, wherever that
   repo's `AGENTS.md` (or equivalent) states it — e.g. a PII-encryption
   trait, a permission/role seeder, ledger-locking logic for balances.
   This file does not name or hardcode what those paths are for any
   specific project (that would violate this tree's project-agnostic-
   by-construction rule); it states the pattern: **`builder`'s system
   prompt must include an explicit instruction to stop and report,
   rather than work around, any task that appears to require touching a
   Tier-0-class fenced path** — mirroring `../frontend/hooks-protected-
   files.md`'s "translate an existing rule, don't invent a new one"
   discipline, one level up (prose-in-subagent-prompt instead of a
   hook), applied to whatever the target repo itself has already
   declared protected. Frontend has no equivalent because the
   koperasiqu-web-app-style fencing concept, as observed so far, is
   backend-specific (PII/encryption, permission seeding, ledger
   locking) — this may not generalize to every project using this
   workspace, which is exactly why the instruction is phrased as "read
   whatever your target repo declares," not as a fixed list.
3. **Model routing carries an explicit unresolved caveat.**
   `best-practices/model-routing.md`'s "Backend build" row is scoped to
   Go (`Backend build (Go)`) and that same table's own fallback-mapping
   section notes the Go-tuned picks aren't validated for other backend
   languages. For a non-Go backend (e.g. PHP/Laravel), route `builder`
   to the fallback-mapping table's generic Claude Code "Backend build,
   Expert" cell (currently Opus 4.8) rather than the Go-row's specific
   picks, and flag this substitution explicitly rather than presenting
   it as a validated language-specific choice — same posture a real
   decomposition manifest on this workspace already took when it hit
   this exact gap.

## Pattern

```md
<!-- .claude/agents/explorer.md -->
---
name: explorer
description: Runs the exploration phase (read-only investigation)
tools: Read, Grep, Glob
model: <lowest tier suited to interactive/small material per
        best-practices/model-routing.md's Exploration row>
---

Follow workflow/1-exploration/guidelines.md's process. Do not skip or
merge stages. Read-only — do not write or edit files during this phase.
```

```md
<!-- .claude/agents/builder.md -->
---
name: builder
description: Runs the build phase (tight edit -> run -> fix loop) and executes patches requested by code-review or testing
tools: Read, Write, Edit, Bash
model: <Expert/Good/Enough per model-routing.md's "Backend build" row —
        see the Go-scoping caveat above if this repo's backend isn't Go>
---

Follow workflow/3-build/'s process. You have Bash access to run
migrations, framework CLI tooling, and the test suite as part of the
iteration loop. Every patch this feature needs — from your own
iteration, or requested later by code-review/testing — executes and is
reported here, per README.md's Task Working Directory Structure rule.

Before touching any file, check it against [TARGET REPO CONVENTION FILE
PATH]'s File-Path-Fencing declaration (if any). If the task appears to
require touching a fenced path, stop and report it — do not work around
it via an indirect edit.
```

Repeat the phase-subagent pattern for `techplan-writer` and
`code-reviewer`/`tester` following `../frontend/subagents.md`'s existing
examples for those two — nothing backend-specific changes their tool
scope or system-prompt shape, only `builder`'s does, per the three
differences above.

## Context handoff between subagents

Same requirement as `../frontend/subagents.md` — explicit, not assumed.
One backend-specific addition: the `builder` subagent, when invoked to
execute a patch requested by `code-reviewer` or `tester`, needs that
patch-plan's file path passed in explicitly at invocation (it lives in
`4-code-review/` or `5-testing/`, not `3-build/`, per README.md's Task
Working Directory Structure) — a subagent boundary makes this handoff
mandatory in exactly the way a single long session might let it happen
implicitly.

## Checklist

- [ ] `builder`'s tool list includes `Bash` — verify this wasn't copied
      from frontend's `builder` mapping without re-checking
- [ ] Every subagent's system prompt includes the fenced-path stop-and-
      report instruction, sourced from the target repo's own `AGENTS.md`
      (or equivalent) — never a hardcoded path list invented here
- [ ] `builder`'s `model` choice states explicitly whether it's using a
      language-validated cell from `model-routing.md`'s "Backend build"
      row or falling back to the generic Claude Code Expert-tier pick,
      per the caveat above — don't silently treat the Go-scoped picks as
      language-neutral
- [ ] Every subagent's system-prompt body references `workflow/<phase>/`
      files by path — never inlines guideline content
- [ ] New subagent mappings are tried on a low-stakes task first — Tier
      2, same as frontend's version of this file
