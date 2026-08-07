# Techplan Guidance

This folder contains the guidance an AI Agent uses to read exploration
documents in `docs/story/<story-code>/` and produce a single
`techplan.md` in that same story folder.

This folder is a **purely local workspace** — not merged into any
project repo, and portable across projects with different standards.

## File Map

| File | Answers the question | Nature |
|---|---|---|
| `template.md` | What does the final techplan look like? | Stable |
| `rules.md` | What's mandatory, and how do we map content to sections? | Stable |
| `guardrails.md` | When should the agent stop instead of assuming? | Stable |
| `guidelines.md` | What's the read-synthesize-write process, step by step? | Stable |
| `examples.md` | Concrete examples calibrated for tone & level of detail? | Growing (append new examples) |
| `retro.md` | Mistakes that happened during synthesis, and their mitigations? | Growing (living log) |
| `proposals/` | Proposed changes to the four files above | Growing (append new proposals) |

## Fundamental Rules

1. **The agent must not edit `template.md`, `rules.md`, `guardrails.md`,
   or `guidelines.md` directly.** If the agent finds a gap or friction
   during synthesis, it writes a new proposal in `proposals/` (see
   `proposals/_proposal-template.md` for the format). A human reviews
   and merges it into the target document.
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
docs/story/<story-code>/*.md  (raw, dynamic, count & content not fixed)
              │
              ▼  agent reads everything + reads this guidance folder
   classify content by FUNCTION (not by file name)
              │
              ▼
docs/story/<story-code>/techplan.md   (canonical, ready for lead/team review)
```