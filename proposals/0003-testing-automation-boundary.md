# 0003 — Automation-vs-manual boundary for frontend testing (`react/testing-automation-boundary.md`)

**Status:** Proposed
**Date:** 2026-08-23
**Triggered by:** Discussion of whether kencleng frontend testing can/should be enforced by automation vs manual review — surfaced that the earlier checklist items across 0001/0002's files (ban raw `fetch`, ban unsanitized `dangerouslySetInnerHTML`, ban raw `error.message` in JSX) were stated as prose checklist items with no corresponding enforcement mechanism
**Target area:** best-practices
**Target file(s):**
- New: `best-practices/react/testing-automation-boundary.md`
- `best-practices/index.md` — 1 new row

## Gap found

This workspace already learned, and formalized via `workflow/2-techplan/`
proposals 0002/0003, that a rule restated as prose inside a checklist gets
skipped regardless of model or person — the fix that held was converting it
into an explicit mechanical self-check. The `react/` files added in 0001
and 0002 contain several checklist items that are themselves mechanically
pattern-matchable (banned function calls, banned props, banned identifier
usage) but were left as prose-only checklist bullets, with no lint-rule
equivalent shown. Without a concrete example of *how* to convert "no raw
fetch outside lib/api/" into an enforced rule, it stays exactly the kind of
prose reminder this workspace's own retro already showed doesn't survive.

Separately, there wasn't previously a stated decision boundary for *which*
kinds of frontend checks are worth automating at all versus which
genuinely require human judgment (test intent, UX/visual correctness,
whether a gate is being gamed) — leaving that implicit risks either
under-automating (checklist bloat nobody actually enforces) or
over-automating (chasing lint coverage for things that need a human,
like judging whether a mock is at the right layer).

## Proposed change

One new file, `react/testing-automation-boundary.md`, that:
1. States the automate-vs-manual decision rule (AST/text-pattern-matchable
   → lint; requires understanding intent → manual, at the existing
   human-checkpoint/Finalize stage — no new stage introduced)
2. Gives concrete ESLint config examples for the three bans already implied
   by earlier files in this category (raw `fetch`, unsanitized
   `dangerouslySetInnerHTML`, raw `error.message` in JSX)
3. Notes automated a11y tooling (`jest-axe`/`@axe-core/react`) is a floor,
   not a substitute for a manual accessibility pass — industry tooling
   catches roughly a third to half of real a11y issues

Corresponding `index.md` update: 1 new row, not security-critical, not
added to the Security Concern Map (it's a cross-cutting testing-process
file referencing security-relevant bans defined elsewhere, not itself a
security pattern file).

## Rationale

Genuinely generic — the decision table and the three example rules apply
to any React/TypeScript codebase using ESLint, not kencleng specifically.
It's also directly derivative of a pattern this workspace has already
validated once (techplan's self-check-list conversion, `workflow/
2-techplan/retro.md`) — applying a proven lesson to a new area rather than
inventing a new one, which is a stronger justification than most
first-time proposals get to make.

This file cross-references checklist items in `api-client-centralization.md`
(0001), `xss-and-content-sanitization.md` (pre-existing `pwa/`), and
`loading-empty-error-state-conventions.md` (0002) — if any of those are
rejected or revised on review, this file's example rules should be
revisited to match, since they're illustrating enforcement of those
specific checklist items.