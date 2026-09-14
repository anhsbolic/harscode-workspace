# subagents.md (Claude Code, backend track)

**Tier:** 2 — higher risk than Tier 1. A subagent's tool restrictions and
context isolation are load-bearing: get the tool list wrong and either an
agent can do something it shouldn't (under-fenced), or a phase silently
loses information it needed because it wasn't explicitly passed in
(over-isolated). Test each mapping in a low-stakes run before trusting it.

## What this translates

Same underlying mechanics as `../frontend/subagents.md`: Claude Code
subagents provide a genuinely separate context window plus scoped tools.
The portable boundary policy itself now lives in
`workflow/context-management.md`.

That means **do not infer one subagent per workflow phase as a mandatory
policy**. Use a subagent when the workflow calls for or recommends a fresh /
isolated context. In particular:

- Exploration → Techplan remains adaptive (`CONTINUE` or `FRESH` from the
  Exploration handoff).
- Techplan → Build is fresh-preferred.
- Code Review and Testing benefit from fresh independent context.
- Review/Testing patch requests return to Build authority.

The remainder of this file only states where the backend Claude Code
translation genuinely differs from the shared/frontend mapping, per
`harness-optimization/README.md`'s track-split rule.

## Where backend genuinely differs from frontend

1. **`builder` needs `Bash`, not just `Read`/`Write`.** Running
   migrations, the framework's CLI tooling, and the test suite as part
   of the tight build→run→fix loop (`workflow/3-build/`) is normal
   backend build activity. Don't copy a narrower tool list verbatim if
   the backend target actually needs those commands.
2. **Every subagent's system prompt must reference the target repo's
   own File-Path-Fencing-Tier-0-class declaration**, wherever that
   repo's `AGENTS.md` (or equivalent) states it. Harscode does not name
   or hardcode those target-project paths. A builder must stop and
   report rather than work around a required fenced edit.
3. **Model routing carries whatever caveats the active routing source
   declares.** Do not silently treat a language-validated routing row as
   language-neutral. Model/client choice is execution configuration;
   this file does not create a new lifecycle rule.

## Pattern

```md
<!-- .claude/agents/explorer.md -->
---
name: explorer
description: Runs the exploration phase (read-only investigation)
tools: Read, Grep, Glob
model: <choice from the active routing/execution profile>
---

Follow workflow/1-exploration-kickoff-prompt.md — the canonical entry
prompt for this phase. Do not skip its human gates. Read-only — do not
write or edit production files during this phase. End with the prompt's
phase handoff and session recommendation.
```

```md
<!-- .claude/agents/builder.md -->
---
name: builder
description: Runs the build phase (tight edit -> run -> fix loop) and executes patches requested by code-review or testing
tools: Read, Write, Edit, Bash
model: <choice from the active routing/execution profile>
---

Follow workflow/3-build-prompt.md — the canonical entry prompt for this
phase. Re-ground on the Approved Techplan spine, current task slice when
decomposed, relevant live code/spec, and the specific patch plan on
re-entry. Use Bash only for commands the target repo authorizes.

Before touching any file, check it against [TARGET REPO CONVENTION FILE
PATH]'s protected/fenced-path declaration (if any). If the task appears
to require touching a fenced path, stop and report it — do not work around
it via an indirect edit.
```

When a fresh Techplan/Code Review/Testing subagent is warranted, use the
shared pattern from `../frontend/subagents.md`: route to the canonical root
prompt, give it the smallest sufficient durable inputs, and preserve that
phase's tool/write authority.

## Context handoff between subagents

Information needed by a fresh subagent must be explicit and durable, not
assumed to carry over from a parent conversation. Use the phase handoff and
`workflow/context-management.md` to pass only what the next phase needs.

One backend-specific example: a `builder` invoked for a patch requested by
Code Review or Testing needs that specific patch-plan path (it lives under
`4-code-review/` or `5-testing/`) plus the Approved Techplan/current task and
relevant live code. It does **not** need the whole reviewer/tester transcript.

## Checklist

- [ ] A subagent boundary implements an actual fresh/isolation need; it is
      not created automatically just because a new phase name exists.
- [ ] `builder` includes the command capability (e.g. Bash) the target repo
      actually requires, no broader.
- [ ] Protected/fenced-path instructions come from target-repo authority,
      never a Harscode-hardcoded project path list.
- [ ] Every subagent body references the canonical root `*-prompt.md`
      (phase folder only when no root prompt exists), never an inlined copy.
- [ ] Durable handoff inputs are explicit; chat history is not authority.
- [ ] Review/Testing do not execute production patches; fixes return to Build.
- [ ] New mappings are tried on a low-stakes task first — Tier 2 for a reason.
