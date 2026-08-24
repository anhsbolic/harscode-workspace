# subagents.md (Claude Code, frontend track)

**Tier:** 2 — higher risk than Tier 1. A subagent's tool restrictions and
context isolation are load-bearing: get the tool list wrong and either an
agent can do something it shouldn't (under-fenced), or a phase silently
loses information it needed because it wasn't explicitly passed in
(over-isolated). Test each mapping in a low-stakes run before trusting it.

## What this translates

`workflow/`'s "amnesiac contractor" framing (agents don't compound; each
session ideally starts from exactly the context it needs, no more, no
less) maps directly onto Claude Code subagents: a genuinely separate
context window per invocation, not just a discipline of "pretend this is
a fresh session." Combined with `best-practices/model-routing.md`'s
tier-based model selection and this workspace's existing fencing concept
(separation of authority between phases), a subagent per phase is a
stronger implementation of an idea this workspace already had, not a new
idea.

## Pattern

One subagent per `workflow/` phase. Frontmatter carries the model tier
and tool restriction; the system prompt body points at the phase's actual
guideline files by reference, same discipline as `slash-commands.md`.

```md
<!-- .claude/agents/explorer.md -->
---
name: explorer
description: Runs the exploration phase (read-only investigation)
tools: Read, Grep, Glob
model: <lowest tier suited to interactive/small material per
        best-practices/model-routing.md's Exploration row>
---

Follow workflow/1-exploration/guidelines.md's 3-stage process and
workflow/1-exploration/sniffing-checklist.md's five lenses. Do not skip
or merge stages. You have read-only access — do not attempt to write or
edit files during this phase.
```

```md
<!-- .claude/agents/techplan-writer.md -->
---
name: techplan-writer
description: Synthesizes a techplan from exploration output
tools: Read, Write
model: <highest tier warranted per model-routing.md's Techplan-synthesis
        row, scaled to the story's assessed complexity tier>
---

Follow workflow/2-techplan/guidelines.md, rules.md, and
guardrails.md. You may write the techplan artifact itself. You do not
have access to edit any file under workflow/2-techplan/ directly (that
tree is agent-protected — see workflow/2-techplan/AGENTS.md); if you
find a gap in the guidance itself, write a proposal instead.
```

Repeat the pattern for build, code-review, and testing subagents, each
scoped to that phase's actual tool needs (a code-review subagent, for
instance, plausibly needs only `Read` — it shouldn't be able to edit the
code it's reviewing).

## Context handoff between subagents

Because each subagent's context is genuinely separate, information that a
later phase needs from an earlier one must be explicitly passed, not
assumed to carry over. The techplan subagent needs the exploration
output's location (a file path) passed into its invocation; the build
subagent needs the techplan's location, and so on. This isn't a new
requirement — it's the same handoff this workspace's phases already do
via written artifacts on disk — but a subagent boundary makes the
handoff mandatory rather than something an agent might reconstruct from a
long shared context by accident.

## Checklist

- [ ] Each subagent's `tools` list is the minimum the phase's guideline
      files actually require — not copied from a broader default. A
      code-review subagent that can `Write` defeats the "separation of
      authority" principle this workspace already holds for that phase
- [ ] Each subagent's `model` is chosen per `best-practices/
      model-routing.md`'s tier logic, not defaulted to whatever the
      main session is using
- [ ] Every subagent's system-prompt body references `workflow/<phase>/`
      files by path — never inlines guideline content, for the same
      single-source-of-truth reason as `slash-commands.md`
- [ ] What information a later-phase subagent needs from an earlier one
      is explicit in how it's invoked (a file path, a story identifier)
      — never assumed to be "still in context" from a prior turn
- [ ] New subagent mappings are tried on a low-stakes task first — this
      is Tier 2 for a reason; an under- or over-fenced subagent is a
      silent failure mode, not a loud one