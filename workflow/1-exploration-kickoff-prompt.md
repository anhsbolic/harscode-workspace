# Exploration Kickoff Prompt

Canonical entrypoint for understanding a task before solution/Techplan synthesis.

## Inputs required before running

- `{HARSCODE_WORKSPACE_ROOT}`
- `{TASK_PATH}`
- `{CODEBASE_CONTEXT}` — one-line orientation only
- `{TASK}` — requirement text or source path
- optional Ticket / Area

## Prompt

```text
You are exploring this task in {CODEBASE_CONTEXT}.

Task: {TASK}
Ticket: {ticket/link if any}
Area: {known area or "not sure yet"}
Working directory: {TASK_PATH}

Read the target repo's applicable instructions/authority only as needed to
identify and investigate the relevant areas. Guidance for Exploration lives at:
- {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration/guidelines.md
- {HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration/sniffing-checklist.md

Do not load Exploration examples unless you need calibration for an ambiguous
output shape.

STAGE 1 — PLAN ANNOUNCEMENT (hard stop)
- State your 1–2 sentence understanding of the task.
- Identify the areas you intend to explore, order, and why.
- Do not inspect implementation deeply or propose solutions yet.
- STOP for human confirmation.

STAGE 2 — GAP ANALYSIS (after confirmation)
For each area, complete it before moving on:
- Current state — concrete live behavior, files/symbols/contracts.
- Requirement — exact relevant source expectation.
- Gap — specific difference.
- Sniffing — risk, edge cases, miscontext, misleading signals,
  inconsistency per sniffing-checklist.md.
- Code anchors — record path + symbol/section + why it matters for later
  verification/Build; do not turn copied implementation into a new authority.

No developed solutioning here. A one-line observation may be parked without
turning it into a decision.

Write durable Stage-2 evidence under {TASK_PATH}/1-exploration/logs/.
Report progress after each area so the human can redirect, but do not require a
new approval between every area unless asked.

STAGE 3 — SOLUTIONING (only after human confirms Stage 2)
Compare options/trade-offs and record the chosen direction plus material
rejected alternatives/rationale. Keep source evidence and decisions durable in
{TASK_PATH}/1-exploration/logs/; do not rely on chat memory alone.

At Stage-3 completion, output:

## Phase handoff
- Completed: <areas explored + solutioning state>
- Artifacts: <durable Exploration paths>
- Open / blocked: <material unresolved items or none>
- Recommended next step: Techplan synthesis
- Session recommendation: CONTINUE | FRESH — based on continuation fitness
- Context pointers: <source/spec paths + code anchors likely needed next>

Recommend FRESH when the session was compacted/reset, accumulated substantial
dead ends/unrelated investigation, had major human redirection, or cannot name
the current durable authorities cleanly. Otherwise CONTINUE is valid; do not
use a fuzzy task-size label as the deciding rule.
```

## Notes

Exploration is detailed evidence, not an early Techplan. The Techplan later synthesizes it into a durable execution contract. Code anchors transfer coordinates; later phases still reopen live code/spec before treating implementation details as current fact.
