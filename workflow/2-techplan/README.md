# Techplan Guidance

This folder contains the guidance an AI Agent uses to read exploration
documents in `{TASK_PATH}/1-exploration/logs/` and produce a single
`techplan.md` in `{TASK_PATH}/2-techplan/`.

This folder is a **purely local workspace** — not merged into any
project repo, and portable across projects with different standards.

## File Map

| File | Answers the question | Nature |
|---|---|---|
| `template.md` | What does the final techplan look like? | Stable |
| `rules.md` | What's mandatory, and how do we map content to sections? | Stable |
| `guardrails.md` | When should the agent stop instead of assuming? | Stable |
| `guidelines.md` | What's the read-synthesize-write process, step by step? | Stable |
| `diagram-guidelines.md` | How do I write a valid, correctly-scoped Mermaid diagram for the digest? | Stable |
| `examples.md` | Concrete examples calibrated for tone & level of detail? | Growing (append new examples) |
| `retro.md` | Mistakes that happened during synthesis, and their mitigations? | Growing (living log) |
| `techplan-example.md` | Real example of techplan result? | Stable|
| `proposals/` | Proposed changes to the four files above | Growing (append new proposals) |

## Fundamental Rules

1. **The agent must not edit `template.md`, `rules.md`, `guardrails.md`,
   `guidelines.md`, or `diagram-guidelines.md` directly.** If the agent
   finds a gap or friction during synthesis, it writes a new proposal in
   `proposals/` (see `proposals/_proposal-template.md` for the format). A
   human reviews and merges it into the target document.
2. `examples.md` and `retro.md` may be appended to directly by the
   agent without going through the proposal process — the risk is low
   since these are additive (adding an example/note), not a change to
   an existing rule.
3. Proposals that have been **Merged** are not deleted. Since this
   folder isn't git-tracked as its own repo, the proposal history is
   the only changelog that exists for "why rules.md looks like this now".
4. Threshold for writing a proposal: **recurring friction (2+ stories)
   or genuinely structural** — not every time a session finds something
   that could be slightly better. See `guidelines.md` § Proposal Threshold.

## Workflow at a Glance

```
{TASK_PATH}/1-exploration/logs/*.md  (raw, dynamic, count & content not fixed)
              │
              ▼  agent reads everything + reads this guidance folder
   classify content by FUNCTION (not by file name)
              │
              ▼
{TASK_PATH}/2-techplan/techplan.md   (canonical, ready for lead/team review)
```