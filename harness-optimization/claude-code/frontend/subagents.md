# subagents.md (Claude Code, frontend track)

**Tier:** 2 — context isolation and tool restrictions are load-bearing. Test a
new mapping on low-stakes work before relying on it.

## What this translates

Portable authority lives in `workflow/context-management.md` plus each phase's
canonical root prompt.

A Claude Code subagent is one way to implement a **fresh/isolation boundary**.
It is **not** a rule that every workflow phase must always be a separate
subagent. The workflow decides whether continuation or fresh context is
appropriate; the harness chooses the native mechanism that implements that
choice.

Important consequences:

- Exploration → Techplan is adaptive. If Exploration recommends `CONTINUE` and
  the current session remains healthy, continuing without a new subagent is
  valid. If it recommends `FRESH`, a Techplan subagent is a good translation.
- Techplan → Build is fresh-preferred because Build needs the locked contract +
  live code rather than exploratory reasoning.
- Code Review and Testing benefit from fresh independent context.
- Review/Testing findings that need code changes return to Build authority; do
  not give reviewer/tester subagents write authority merely for convenience.

## Pattern

When a phase is intentionally isolated, frontmatter carries the minimum tool
scope and model selection; the body points to the canonical Harscode prompt
instead of restating it.

```md
<!-- .claude/agents/explorer.md -->
---
name: explorer
description: Runs Exploration as a read-only investigation
tools: Read, Grep, Glob
model: <choice from the active model-routing/execution profile>
---

Follow workflow/1-exploration-kickoff-prompt.md in full. Preserve its Stage-1
and Stage-2/3 human gates, write the durable Exploration artifacts it requires,
and end with its phase handoff/session recommendation.
```

```md
<!-- .claude/agents/techplan-writer.md -->
---
name: techplan-writer
description: Synthesizes an execution-grade Techplan from durable Exploration evidence
tools: Read, Write
model: <choice from the active model-routing/execution profile>
---

Follow workflow/2-1-techplan-synthesis-prompt.md in full. Its required core
Techplan authority is template.md + rules.md + guardrails.md; deeper guidance,
examples, retro, diagram guidance, and report guidance remain conditional per
that prompt. You may write the task Techplan artifact, but you may not directly
edit protected Harscode Techplan guidance.
```

Use the same pattern for Build, Code Review, and Testing only when a fresh
subagent boundary is warranted. Tool scope follows the actual phase authority:
Build can edit/run; Code Review and Testing should not gain production-code
write authority merely because they discover a defect.

## Context handoff between subagents

A fresh subagent must reconstruct correctness from durable state, not from a
parent conversation summary.

Pass the smallest sufficient durable inputs named by the canonical prompt and
`workflow/context-management.md`, including the previous phase handoff/context
pointers when relevant. Typical examples:

- Techplan: task root + durable Exploration artifacts + applicable target-repo
  authority.
- Build: Approved Techplan spine + current task slice when decomposed + live
  code/spec anchors.
- Code Review: current diff + Approved Techplan/current task + target-repo
  conventions.
- Testing: current Techplan + latest build evidence + real verification entry
  points + exact Test Focus evidence anchors.

Do not pass the entire previous transcript merely because a subagent boundary
exists.

## Checklist

- [ ] A subagent boundary implements an actual fresh/isolation need; it is not
      created automatically just because a new phase name exists.
- [ ] Tools are the minimum the canonical phase requires.
- [ ] The body references the canonical root `*-prompt.md` (phase folder only
      when no root prompt exists) and does not maintain a copied workflow.
- [ ] Required durable inputs/phase handoff are explicit at invocation.
- [ ] Exploration → Techplan respects the Exploration `CONTINUE`/`FRESH`
      recommendation instead of hardcoding one behavior.
- [ ] Review/Testing do not fix production code; patch work returns to Build.
- [ ] New mappings are dogfooded before being trusted for high-risk work.
