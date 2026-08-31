# Synthesis Prompt

Ready-to-use prompt for instructing an AI Agent (Claude Code, OpenCode
CLI, etc.) to synthesize a techplan.md from raw exploration output,
using this guidance folder. Fill in the placeholders, paste as-is.

```
Read the guidance folder at {WORKSPACE_ROOT}/workflow/2-techplan in
this order: README.md, template.md, rules.md, guardrails.md,
guidelines.md, examples.md, retro.md. All bare file references below
(rules.md, guardrails.md, template.md) resolve relative to this same
folder. This defines how you should classify content and what the
output must look like.

Response style: full detail, execution-grade, no compression — this
techplan becomes the contract other agents and humans execute against
later ({WORKSPACE_ROOT}/workflow/README.md § Response Style By Phase).

Then read every file in {TASK_PATH}/1-exploration/logs/ — treat all of
them as raw material. Don't assume a fixed number or fixed names;
classify each piece of content by the function it serves (rules.md
§ 1), not by which file it came from.

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
misleading signals, inconsistency), read {WORKSPACE_ROOT}/best-practices/index.md.
Match the trigger keywords in the index table against the area(s)/technology(ies)
touched by this ticket (Go, PostgreSQL, GraphQL, REST API, Kafka, Pub/Sub, Redis).
Open ONLY the matching file(s) — do not scan the entire best-practices/ folder.
Apply the checklist from each matching file as part of the risk lens.

When populating the Testing Checklist section (currently §12 — verify
the actual number against this template.md, don't assume), also
populate its Test Focus Pointer table (see rules.md's Test Focus
Pointer rule) by cross-referencing the raw exploration docs' Sniffing
Checklist Risk findings for this task. Only carry forward areas
genuinely about shared state, concurrency, an expensive primitive
under load, or a security-sensitive boundary — and don't silently drop
one that survived synthesis (see guardrails.md's rule on flagged risk
areas); mark it N/A with a one-line reason instead.

Write the result to {TASK_PATH}/2-techplan/techplan.md, following
template.md's structure exactly. At the end, list out any open items
or unresolved questions you carried forward instead of silently
deciding — I'll review those manually before this goes anywhere
further.
```

## Placeholders

- `{WORKSPACE_ROOT}` — path to this harscode-workspace's content
  relative to (or as an absolute path from) your project. Set once per
  project; see `workflow/README.md` § Path Variables Convention.
- `{TASK_PATH}` — root working directory for this specific task in the
  target repo (e.g. `.local-agents/works/account/06-mfa-totp/`), NOT
  just the exploration output folder. Every phase writes into its own
  numbered subfolder under this same root — see root `README.md` §
  Task Working Directory Structure. This prompt specifically reads
  from `{TASK_PATH}/1-exploration/logs/` and writes to
  `{TASK_PATH}/2-techplan/techplan.md`.

## Notes

- `{WORKSPACE_ROOT}` replaces the old "make sure it's reachable" manual
  step — resolve it once for this project and every reference above
  follows automatically.
- The output is a draft for your manual review — writing it to
  `{TASK_PATH}/2-techplan/techplan.md` is a deliberate checkpoint, not
  something to automate past. Review before it goes anywhere further
  (a PR, a decomposition pass, etc.).
- The stack-specific risk lens step assumes `best-practices/` sits as a
  sibling to `workflow/` under `{WORKSPACE_ROOT}`. If your layout
  differs, that's exactly what `{WORKSPACE_ROOT}` is for — point it at
  wherever the common parent actually is.