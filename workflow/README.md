# Workflow

This is a personal AI development workflow — guidance only. Everything
in here tells an AI Agent *how* to produce something at a given stage
of a feature's lifecycle. It does not store any generated content.

Generated artifacts (task exploration docs, techplan.md, PR
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
  exploration/     Kickoff + clarifying questions → produces raw docs in {TASK_PATH}/1-exploration/logs/
  techplan/        Turns those raw docs into one techplan.md
  build/           Thin test-scope boundary for the tight edit → run → fix loop
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
| `2-techplan/` (`template.md`, `rules.md`, `guardrails.md`, `guidelines.md`, `diagram-guidelines.md`, `report-template.md`) | Yes | `../proposals/` (root), Protection Tier: `techplan-protected` — threshold: 2+ tasks or genuinely structural |
| `2-techplan/examples.md`, `2-techplan/retro.md` | No — agent-appendable directly | N/A |
| `1-exploration/`, `3-build/`, `4-code-review/`, `5-testing/`, `6-pull-request/` | No, today | None — corrected in the moment. If a real recurring gap ever justifies formal protection here, use `../proposals/` with Protection Tier `general`, not a new mechanism |

There's one proposal mechanism for the whole workspace: the root-level
`proposals/`, one shared numbering sequence. `2-techplan/`'s protected
files keep a higher bar (2+ tasks or a genuinely structural gap) —
appropriate given a techplan is a contract a lead signs off on — but
that's now expressed as a `Protection Tier: techplan-protected` field
on the proposal itself, not a separate folder. This used to be a
second, narrower `2-techplan/proposals/` folder; it was folded into
the root `proposals/` because two independent numbering sequences that
occasionally needed to cross-reference each other (a `best-practices/`
fix and a techplan fix from the same real incident) produced colliding
numbers. See `../proposals/README.md` for the tier field and numbering
rule. The lightweight stages above use the same root `proposals/` with
Protection Tier `general` if one of them ever outgrows "corrected in
the moment." Don't reach for it pre-emptively — that would contradict
the whole point of keeping these stages lightweight.

`2-techplan/examples.md` and `2-techplan/retro.md` are the one
exception to "protected files need a proposal" anywhere in this
workspace — append directly, no proposal needed. This does not
generalize to `best-practices/examples.md` files, which are
proposal-gated (see `best-practices/index.md`).

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

## Path Variables Convention

Every prompt file under `workflow/` (the root-level `*-prompt.md`
files) references this workspace's own guidance files — `template.md`,
`rules.md`, `best-practices/index.md`, and so on. Where this
workspace's content actually lives relative to a given project varies
by person and by project (copied into project root, kept as a
subfolder, symlinked from a shared location elsewhere) — nothing here
assumes one fixed layout.

Two tiers of fill-in variables show up across these prompts — knowing
which tier a variable belongs to tells you how often you actually need
to touch it:

- **Project-level (set once, reused across every task on this
  project):** `{HARSCODE_WORKSPACE_ROOT}` — where this workspace's content
  lives relative to the project. `{CODEBASE_CONTEXT}` — a one-line
  label for the project/repo (e.g. "Kencleng — Go backend + Next.js
  frontend"), used only for quick orientation before an agent reads the
  repo's own README/AGENTS.md in full. It is deliberately NOT a
  restated description of the codebase — that would duplicate the
  target repo's own README as a second, independently-drifting source
  of truth, the exact failure mode this workspace's own single-source-
  of-truth principle exists to avoid elsewhere. Deep repo understanding
  always comes from the agent actually reading the repo's own
  convention file, which every relevant prompt already instructs it to
  do — this label just orients faster before that read happens.
- **Per-run (set fresh for each task/invocation):** `{TASK_PATH}`,
  `{TASK}` (pasted content or a document path, either works), and
  similar — these change every time because they describe this
  specific piece of work, not the project as a whole.

Set every project-level variable once per project — e.g. if this
workspace is symlinked at `./guidance` in a given project, every
prompt used against that project resolves `{HARSCODE_WORKSPACE_ROOT}` to
`./guidance` for every future invocation, not once per prompt.

`[TARGET REPO CONVENTION FILE PATH]` (used in a couple of prompts) is
a third, hybrid case — technically project-level since the path itself
doesn't change, but written as a per-invocation bracket placeholder
today since the prompts that use it are invoked less frequently than
per-task ones. Treat it as project-level in practice.

## Response Style By Phase

Two independent things vary by phase — don't conflate them into one
"verbose vs terse" dial:

- **Process verbosity** — how much narration/reasoning an agent
  produces while doing the work itself, before any final report or
  artifact exists. Planning-type phases (techplan synthesis, review,
  decomposition) warrant full, explicit reasoning at every step,
  because ambiguity here becomes an execution contract other people
  and agents rely on later. Execution-loop phases (`build/`, and
  `testing/`'s coverage/sweep work) warrant minimal narration — do the
  work efficiently, don't narrate each step — because this is fast,
  iterative work, not the final artifact.
- **Deliverable completeness** — how much detail the phase's actual
  output (techplan.md, a review findings report, a build/testing
  report) contains. This stays high in every phase regardless of how
  terse the process getting there was. A terse build loop must still
  produce a complete, unambiguous report — what changed, what was
  tested, what's flagged — the same way a real testing report already
  demonstrates this is possible without a slow, over-narrated process
  (see `best-practices/go/examples/testing-concurrency.md` for a
  worked real-world example).

Each prompt states its own setting for both axes near the top of its
`## Prompt` block — a one-line pointer back here plus whatever's
specific to that phase, not a restatement of the whole rationale every
time.

## Prompt File Shape

Every `*-prompt.md` file follows the same skeleton, so a new phase's
prompt doesn't drift from whichever sibling its author happened to
copy last:

1. **Title + one-line intro** — what this prompt is for. A dedicated
   `## Purpose` heading is optional, not mandatory — only add one when
   the prompt introduces something genuinely non-obvious that needs
   justifying (e.g. `2-2-techplan-review-prompt.md` explains *why* an
   independent second-pass review exists, citing the real incident
   that motivated it). Don't add `## Purpose` just for uniformity —
   restating an obvious phase name in prose is filler, not
   documentation.
2. **`## Inputs required before running`** — every placeholder
   (`{HARSCODE_WORKSPACE_ROOT}`, `{TASK_PATH}`, etc.) and every precondition
   material (a locked techplan, prior-phase output already on disk,
   etc.) needed before this prompt makes sense to run. Always this
   exact heading, always before the `## Prompt` block — a reader
   deciding whether they're ready to run this shouldn't have to read
   the whole prompt text first to find out.
3. **`## Prompt`** — the literal, paste-ready fenced block. Mandatory,
   always this exact heading. This is the one thing every prompt file
   exists to provide; if a phase turns out to need conditional logic
   before its prompt applies (see `2-3-techplan-decomposition-prompt.md`'s
   gate question), that logic goes inside this block, not as a
   replacement for it.
4. **Phase-specific output sections** (optional, varies per phase) —
   e.g. `4-code-review-prompt.md`'s Safety/Quality/Consistency
   breakdown, `3-build-prompt.md`'s What changed/Tests run. These
   genuinely differ per phase; don't force a common shape here.
5. **`## Notes`** — always last, always this exact heading. Answers
   "what do I do with the output" and "what's the immediate next
   manual step" — not a dumping ground for anything that didn't fit
   elsewhere. If you're tempted to add a "How To Use" heading, put that
   content here instead: a second heading for the same kind of content
   invites exactly the two-sources-of-truth drift this workspace
   already learned to avoid the hard way (`techplan/decisions-log.md`'s
   Summary-desync history).

When adding a new phase prompt, copy this shape, not the nearest
existing file verbatim — the existing files themselves have drifted
from each other before (`2-3-techplan-decomposition-prompt.md` was
missing both its `## Prompt` block and its `## Notes` section until a
routine review caught it).