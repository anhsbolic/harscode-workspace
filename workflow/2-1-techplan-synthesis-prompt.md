# Synthesis Prompt

Ready-to-use prompt for instructing an AI Agent (Claude Code, OpenCode
CLI, etc.) to synthesize a techplan.md from raw story docs, using this
guidance folder. Fill in the two placeholders, paste as-is.

```
Read the guidance folder at workflow/techplan in this order:
README.md, template.md, rules.md, guardrails.md, guidelines.md,
examples.md, retro.md. This defines how you should classify content
and what the output must look like.

Then read every file in {EXPLORATION_LOGS_PATH} — treat all of them as raw
material. Don't assume a fixed number or fixed names; classify each
piece of content by the function it serves (rules.md § 1), not by
which file it came from.

Before filling in the Interface Contract section, read this repo's own
convention file (AGENTS.md / README / CONTRIBUTING — whatever exists
here) to know what's mandatory to cover — don't assume the conventions
from the guidance folder apply here.

If two or more raw docs cover the same ground with conflicting or
overlapping detail, follow rules.md § 2 (Dedup & Reconciliation) —
prefer the most specific and most recent version, and call out
anything that's a genuine conflict rather than picking silently.

If any sub-component has its own independent operational lifecycle
(one-time script, cron, separate rollback/cleanup) — evaluate per
rules.md § 3 whether it belongs as a section here or as a separate
linked document.

Follow every guardrail in guardrails.md — in particular: don't invent
technical facts (mark anything uncertain as `TBD — verify`), don't
overwrite an existing Approved/Implemented techplan's contract sections
silently, and STOP and ask me if you find a breaking change or data
risk that isn't already explicit in the raw docs.

Stack-specific risk lens: before finalizing sniffing (risk, edge cases, miscontext,
misleading signals, inconsistency), read best-practices/index.md.
Match the trigger keywords in the index table against the area(s)/technology(ies)
touched by this ticket (Go, PostgreSQL, GraphQL, REST API, Kafka, Pub/Sub, Redis).
Open ONLY the matching file(s) — do not scan the entire best-practices/ folder.
Apply the checklist from each matching file as part of the risk lens.

When populating section 12 (Testing Checklist), also populate the Test
Focus Pointer table (rules.md § 9) by cross-referencing the raw
exploration docs' Sniffing Checklist Risk findings for this story. Only
carry forward areas genuinely about shared state, concurrency, an
expensive primitive under load, or a security-sensitive boundary — and
don't silently drop one that survived synthesis (guardrails.md § 12);
mark it N/A with a one-line reason instead.

Write the result to {EXPLORATION_LOGS_PATH}/techplan.md, following template.md's
structure exactly. At the end, list out any open items or unresolved
questions you carried forward instead of silently deciding — I'll
review those manually before this goes anywhere further.
```

## Placeholders

- `{EXPLORATION_LOGS_PATH}` — path to the story's raw docs in the target repo
  (e.g. `docs/story/GMRT-50941`). Used as a placeholder because the
  story docs live in the target repo, not in this workspace.

## Notes

- This assumes the agent has file read access to both paths. If your
  guidance folder lives outside the repo the agent is working in, make
  sure it's reachable (mounted, symlinked, or copied somewhere the
  agent's tool access covers) — see `README.md` in the repo root for
  how this workspace is set up.
- The output is a draft for your manual review — the copy step into
  `{service}/.agents/docs/specs/{feature-name}/` is a deliberate
  checkpoint, not something to automate away.
- The stack-specific risk lens step assumes `best-practices/` sits as a
  sibling to `workflow/` at the workspace root (i.e. `best-practices/`
  next to `workflow/`). If your layout differs, update the path in the
  risk lens step above accordingly.