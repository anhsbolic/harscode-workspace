# subagents.md (Claude Code, backend track)

**Tier:** 2 — tool restrictions and context isolation are load-bearing. Test a
new mapping on low-stakes work before relying on it.

## What this translates

The shared session/context rule is `workflow/context-management.md`; read
`../frontend/subagents.md` for the common Claude Code translation.

Backend does **not** redefine the shared boundary rule: Exploration → Techplan
remains adaptive, Build is fresh-preferred from planning, Review/Testing are
fresh for independence, and patches return to Build authority. Use a subagent
when that fresh/isolation boundary is actually chosen; do not infer "one
subagent per phase" as generic workflow policy.

## Where backend genuinely differs

1. **`builder` normally needs `Bash` as well as read/write/edit.** Backend
   iteration commonly needs migrations, framework CLI commands, and tests.
   Scope Bash to what the target repo allows; tool availability never overrides
   protected-path or command authority.
2. **Target-repo fenced/protected paths remain authoritative.** A backend
   builder must read the target repo's own protected-path declaration and stop
   rather than work around a required fenced edit. Harscode does not hardcode a
   project path list here.
3. **Model routing remains an execution concern.** Use the active generic
   routing/execution profile and preserve any language-validation caveat in
   that source; this translation does not create a backend-specific model rule.

## Pattern

```md
<!-- .claude/agents/builder.md -->
---
name: builder
description: Runs Build/Patch edit -> verify -> fix work
tools: Read, Write, Edit, Bash
model: <choice from the active model-routing/execution profile>
---

Follow workflow/3-build-prompt.md in full. Re-ground on the Approved Techplan
spine, current task slice when decomposed, specific patch plan on re-entry, and
current live code/spec. Use the target repo's allowed commands. Before editing,
check the target repo's protected/fenced-path rules and stop/report if the work
requires an edit outside this authority.
```

Explorer, Techplan, Code Review, and Testing use the shared translation from
`../frontend/subagents.md` unless a real backend harness-mechanics difference
exists. Do not create a backend copy merely for stack terminology.

## Patch re-entry

When Code Review or Testing requests a patch, invoke/reuse Build with the
specific patch-plan path plus the smallest sufficient durable state. Do not
move the production fix into reviewer/tester authority and do not pass the
entire review/testing transcript as context.

## Checklist

- [ ] Backend `builder` has the target-repo command/tool capability it actually
      needs, including Bash where appropriate.
- [ ] Protected/fenced-path rules come from target-repo authority, not a list
      invented here.
- [ ] Session/subagent boundaries follow `workflow/context-management.md`.
- [ ] Every subagent body routes to the canonical Harscode phase prompt rather
      than a copied workflow.
- [ ] Patch work remains Build authority.
- [ ] New mappings are dogfooded before high-risk use.
