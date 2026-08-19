# Workflow

This is a personal AI development workflow — guidance only. Everything
in here tells an AI Agent *how* to produce something at a given stage
of a feature's lifecycle. It does not store any generated content.

Generated artifacts (story exploration docs, techplan.md, PR
descriptions, etc.) always live in the target project's own repo —
different repo per project, dynamic, not tracked here. This folder is
purely local and portable across projects with different standards.

There is no top-level "guidance" folder here on purpose — everything
under `workflow/` already is guidance, by definition. Naming a folder
"guidance" inside "workflow" would just repeat the point.

## Structure

```
workflow/
  AGENTS.md        First thing an agent reads in this folder — hard rules + routing, no rationale
  exploration/     Kickoff + clarifying questions → produces raw docs in docs/story/<code>/
  techplan/        Turns those raw docs into one techplan.md
  code-review/     Safety / Quality / Consistency review passes on the implementation
  testing/         Testing-driven refinement + final verification
  pull-request/    Turns an approved techplan + final diff into a PR description
```

This is the rough lifecycle order, though in practice it loops — code
review and testing often send you back to adjust the implementation, and
occasionally back to techplan if a contract-level assumption breaks.

## Why Each Stage Has a Different Internal Structure

Not every stage needs the same amount of ceremony. The internal
structure of each folder is proportional to that stage's stakes and
change frequency — this is deliberate, not inconsistent:

- **`techplan/`** is high-stakes (it's the contract a lead approves
  before execution) and changes slowly. It has `rules.md` +
  `guardrails.md` + a formal `proposals/` process — the agent cannot
  edit its core files directly.
- **`pull-request/`** is high-frequency and low-stakes per artifact (one
  PR description, easy to fix in review if it's slightly off). It's
  intentionally lightweight: `template.md` + `guidelines.md` +
  `examples.md`, no guardrails, no proposal process. Add ceremony here
  only if a real recurring problem proves it's needed — don't
  pre-emptively copy the techplan structure.
- **`exploration/`, `code-review/`, `testing/`** are all lightweight,
  same tier as `pull-request/` — guidelines + examples/checklist, no
  guardrails or proposal process. None of these are contracts anyone
  approves; they're working practices that get corrected in the moment
  if they're off, not through formal review.

## Governance

### Protected files, by stage

| Stage | Protected files? | Proposal mechanism |
|---|---|---|
| `techplan/` (`template.md`, `rules.md`, `guardrails.md`, `guidelines.md`, `diagram-guidelines.md`) | Yes | `techplan/proposals/` (own, threshold: 2+ stories or genuinely structural) |
| `techplan/examples.md`, `techplan/retro.md` | No — agent-appendable directly | N/A |
| `exploration/`, `code-review/`, `testing/`, `pull-request/` | No, today | None — corrected in the moment. If a real recurring gap ever justifies formal protection here, use the root-level `../proposals/`, not a new mechanism |

`techplan/proposals/` is the one place in this whole workspace with a
higher bar (2+ stories or a genuinely structural gap) — appropriate
given a techplan is a contract a lead signs off on. The root-level
`proposals/` (which also governs `best-practices/`) is deliberately
lower-ceremony and is available to any of the lightweight stages above
if one of them ever outgrows "corrected in the moment." Don't reach for
it pre-emptively — that would contradict the whole point of keeping
these stages lightweight.

`techplan/examples.md` and `techplan/retro.md` are the one exception to
"protected files need a proposal" anywhere in this workspace — append
directly, no proposal needed. This does not generalize to
`best-practices/examples.md` files, which are proposal-gated (see
`best-practices/index.md`).

### `AGENTS.md` vs this file

This file is the source of truth for `workflow/` — the tiering
rationale above, cross-stage conventions, scope boundaries. `workflow/AGENTS.md`
is a much thinner layer: the first thing an agent reads on entering this
folder, containing only imperative hard rules and a pointer back here
for anything beyond that. If a rule needs justifying, the justification
lives here, not in `AGENTS.md`.

## Cross-Stage Source of Truth

Later stages consume earlier stages' output, but not by copying
wholesale — each stage's guidance specifies which section of the
earlier artifact is authoritative and which parts must be re-verified
against current reality (e.g. `pull-request/guidelines.md` explains why
"Changes" and "Demo" must come from the actual diff, not from
techplan's Implementation Details).

## What's Explicitly Out of Scope Here

- Project-specific codebase conventions (naming, error handling
  patterns, etc.) — those belong in the target repo's own `AGENTS.md`,
  not here. This folder stays generic and portable on purpose.