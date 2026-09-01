# AGENTS.md — workflow/

Read `README.md` first — full phase-by-phase detail and rationale live
there. This file is just the short version.

## Hard rules

- `2-techplan/` protected files (`template.md`, `rules.md`,
  `guardrails.md`, `guidelines.md`, `diagram-guidelines.md`,
  `report-template.md`): never edit directly. Propose via the root
  `../proposals/`, with `Protection Tier: techplan-protected` — there is
  no separate `2-techplan/proposals/` folder anymore.
- `2-techplan/examples.md` and `2-techplan/retro.md`: the one exception —
  append directly, no proposal needed.
- `1-exploration/`, `3-build/`, `4-code-review/`, `5-testing/`,
  `6-pull-request/`: no protected files today, corrected in the moment.
  Don't invent guardrails or a proposal requirement here on your own
  judgment.