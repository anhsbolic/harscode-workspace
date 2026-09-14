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
- Default session split for one feature: (exploration+techplan),
  (build+patch loop), (code-review), (testing) — four sessions, not one
  per phase and not one for the whole feature. See `README.md` §
  Session Boundaries for the rationale and the one blessed exception
  (merging exploration+techplan).
- Before the first feature session in a new domain, run
  `0-domain-sequencing-prompt.md` and produce `{DOMAIN_PATH}/
  _domain-manifest.md` before picking which feature to start. Don't
  default to strict serial order across a domain's features without
  having checked this.
- Start each phase from its root `*-prompt.md` where one exists. Harness
  wrappers and project overlays route to it — never re-author it, never
  fork it per stack. See `README.md` § Canonical Phase Prompts.
- Stop polishing a phase artifact once the next phase won't have to
  invent a material decision; if a later phase hits one anyway, stop and
  report instead of inventing it. See `README.md` § Phase Convergence.