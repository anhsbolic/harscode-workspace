# Exploration Kickoff Prompt

Canonical entrypoint for understanding a task before solution/Techplan synthesis. Exploration produces durable evidence; it does not implement or prematurely lock the solution.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}` — path to this Harscode workspace, relative to or absolute from the target project. Project-level; normally set once.
- `{TASK_PATH}` — root working directory for this specific task in the target repo. Exploration writes durable output under `{TASK_PATH}/1-exploration/logs/`; later phases reuse the same task root.
- `{CODEBASE_CONTEXT}` — one-line project/stack orientation only (for example, `Kencleng — Go backend + Next.js frontend`). Project-level; not a substitute for reading target-repo authority.
- `{TASK}` — the requirement to explore, either pasted text or a path/link to its authoritative task/spec source. Per-task.
- **Ticket / Area** — optional identifiers or scope hints. If unknown, leave them unknown; Stage 1 determines relevant areas instead of guessing.

## Prompt

```text
You are exploring this task in {CODEBASE_CONTEXT}. This phase has three
stages; do not merge solutioning into gap analysis.

Task: {TASK}
Ticket: {ticket/link if any}
Area: {known area or "not sure yet"}
Working directory: {TASK_PATH}

If {TASK} points to a task-specific requirement/spec document, read that
source before Stage 1. If it points to a large multi-topic source, read the
authoritative section(s) governing this task plus referenced dependencies;
do not infer requirements from a title, filename, or stale summary.

Guidance for Exploration:
- {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration/guidelines.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration/sniffing-checklist.md

Do not load Exploration examples unless you need calibration for an ambiguous
output shape.

Response style: Stage 1 is concise because it is only a routing/checkpoint
step. Stages 2 and 3 preserve concrete evidence and material rationale because
Techplan synthesis must be able to reconstruct the work from durable artifacts.

STAGE 1 — PLAN ANNOUNCEMENT (hard stop)
- Read the target repo's applicable AGENTS/README/convention authority only
  far enough to identify the relevant areas and any non-negotiable boundaries.
- State your 1–2 sentence understanding of the task so a requirement misread
  can be corrected early.
- Identify the areas you intend to explore, their order, and why that order.
- Do not inspect implementation deeply and do not propose solutions yet.
- STOP for human confirmation before Stage 2.

STAGE 2 — GAP ANALYSIS (after confirmation)
For each area, finish that area before moving on:
- Current state — concrete live behavior, relevant files/symbols/contracts.
- Requirement — the exact relevant expectation; cite the governing source
  section/anchor when the task came from a document.
- Gap — the specific difference between current state and requirement.
- Sniffing — run the five lenses in sniffing-checklist.md for this area.
- Code anchors — record path + symbol/section + why it matters for later
  verification/Build; copied implementation text is not a new authority.

When Stage 2 surfaces a concrete stack/security concern that matches portable
best-practice guidance, use
{HARSCODE_WORKSPACE_ROOT}/best-practices/AGENTS.md as the routing rule: search
or scan only the relevant clue/index entries and open only matching authority
files. Do not browse the whole best-practices tree for completeness theater.

Do not develop solutions or compare alternatives in Stage 2. A one-line
observation may be parked without turning it into a decision.

Write durable Stage-2 evidence under {TASK_PATH}/1-exploration/logs/. Report
progress after each area so the human can redirect, but do not require a new
approval between every area unless asked.

STAGE 3 — SOLUTIONING (only after human confirms Stage 2)
Compare viable options/trade-offs and record the chosen direction. Preserve
material rejected alternatives and the rationale/consequence that prevents a
later agent from reopening a settled choice accidentally.

Keep source evidence and decisions durable in
{TASK_PATH}/1-exploration/logs/; do not rely on chat memory alone. The raw-doc
shape should follow the evidence rather than a forced per-file template.

For every durable Exploration artifact written in this phase, include a compact
provenance header with the values actually known: Phase/Stage, Author, Created
(and Updated when materially revised), plus Model, Reasoning, Session, target
revision, and workflow revision when exposed/known and safe to persist. Do not
invent missing metadata or persist account/credential identifiers. Git history
is the default version history.

At Stage-3 completion, output:

## Phase handoff
- Completed: <areas explored + solutioning state>
- Artifacts: <durable Exploration paths>
- Human decision: <decision needed now; "none" if none>
- Open / deferred: <non-blocking unresolved/deferred items or "none">
- Recommended next step: Techplan synthesis
- Session transition: <plain-language continue/fresh action + reason>
- Context pointers: <source/spec paths + code anchors likely needed next>

Recommend a fresh Techplan session when this session was compacted/reset,
accumulated substantial dead ends/unrelated investigation, had major human
redirection, or cannot name the current durable authorities cleanly. Otherwise
say explicitly that Techplan synthesis can continue in this session because
continuation fitness remains healthy. Do not expose only a CONTINUE/FRESH enum
or use a fuzzy task-size label as the deciding rule.
```

## Notes

- Exploration is detailed evidence, not an early Techplan. Techplan later synthesizes this evidence into the execution contract.
- `{CODEBASE_CONTEXT}` stays intentionally small; target-repo authority owns the real project description.
- Code anchors transfer coordinates, not cached implementation truth. Later phases reopen live code/spec before treating implementation facts as current.
- Stage 1 is a deliberate human checkpoint. Stage 2 is not blocking between areas; Stage 3 waits for confirmation that the gap analysis is sound.
- Stage 1 does not need its own durable artifact merely because it is a checkpoint; preserve durable evidence when Stage 2/3 creates information later phases must reconstruct.
