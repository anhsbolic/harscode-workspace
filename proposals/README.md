# proposals/

Single, continuously-numbered log of every proposal to change protected
guidance in this workspace — regardless of which area it targets.

This folder used to be two separate mechanisms: a root `proposals/`
(for `best-practices/` and, if ever needed, lightweight `workflow/`
phases) and a separate `workflow/2-techplan/proposals/` (for
`2-techplan/`'s own protected files, with its own numbering). They were
kept apart deliberately for a while — see the history note at the
bottom — but two independent sequences that occasionally need to
cross-reference each other (e.g. a best-practices fix and a techplan
fix landing from the same real incident) produced colliding numbers
with no way to tell them apart. This folder is the fix: one sequence,
one place, with the tier distinction preserved as **metadata on each
proposal** instead of by folder location.

## Protection Tier field

Every proposal states its tier right after Status/Date:

- **`techplan-protected`** — targets one or more of
  `workflow/2-techplan/{template.md, rules.md, guardrails.md,
  guidelines.md, diagram-guidelines.md, report-template.md}`. Higher
  threshold: write one only if the same friction shows up across 2+
  tasks, or the gap is genuinely structural — a techplan is a contract
  a lead signs off on, so its guidance changes slowly and deliberately.
- **`general`** — targets `best-practices/` (all of it, including
  `index.md`) or a lightweight `workflow/` phase
  (`1-exploration/`, `3-build/`, `4-code-review/`, `5-testing/`,
  `6-pull-request/`) if one of those ever needs formal protection.
  Lower threshold: a real bug/incident, or a recurring pattern, is
  enough on its own.

Use `_proposal-template-general.md` or
`_proposal-template-techplan-tier.md` as the starting shape — the
techplan-tier template additionally expects a `Friction Found` section
grounded in raw task docs, matching that tier's higher bar for
justification.

## After human review

Update the `Status` field (Proposed → Accepted / Rejected /
Superseded). If Accepted, merge the change into the actual target
file(s) and leave the proposal in place — don't delete it. This folder
is the only changelog for guidance changes, since it isn't its own
git-tracked history separate from the rest of the workspace.

## Numbering

Strictly sequential, one shared counter across both tiers — check the
highest existing number before adding a new one, don't restart per
tier. If you're unsure what the next number is, list the folder sorted
— don't trust memory of "the last one I wrote."

## History note

Proposals 0001-0003 predate this consolidation — they were originally
in `workflow/2-techplan/proposals/` under their own numbering (which
happened to match 1-3 here too, so no renumbering was needed for them
specifically). Proposals 0004 onward were renumbered from two
independent sequences when this folder was consolidated — if you find
an old reference elsewhere citing a proposal by a number that doesn't
match what's in this folder, it's pointing at the pre-consolidation
number; check this folder's actual filenames, not the cited number, to
find the right file.