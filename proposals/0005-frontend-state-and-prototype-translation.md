# 0002 — Frontend state-handling conventions + AI-prototype-to-production translation discipline

**Status:** Proposed
**Date:** 2026-08-23
**Triggered by:** Reviewing kencleng's `docs/ui-ux/` and `docs/design-reference/` directories during frontend workflow discussion — found two genuinely generic patterns embedded inside otherwise correctly project-specific documents
**Target area:** best-practices
**Target file(s):**
- New: `best-practices/react/loading-empty-error-state-conventions.md`
- New: `best-practices/react/ai-prototype-to-production-translation.md`
- `best-practices/index.md` — 2 new rows (no Security Concern Map entry needed — neither file is marked security-critical, though the error-message-leak checklist item in the first file is adjacent to it)

Filed separately from proposal 0001 (same target area, same day) so each can
be reviewed/accepted/rejected independently rather than as one bundle.

## Gap found

**1. Loading/empty/error/success state handling** — kencleng's own
`docs/ui-ux/patterns.md` already documents this per page-pattern, in detail
(skeleton shape, generic error + retry, per-card partial-failure isolation
on Dashboard pages, empty-state CTA gated by role). That content is
correctly project-specific (kencleng copy, kencleng route names) and stays
where it is. But the underlying principle is generic and not yet present
anywhere in `best-practices/`: agent-generated frontend code defaults to
building the happy path and treating the other three states as an
afterthought, and the error state specifically carries a real risk —
surfacing a raw backend error/exception string is an information-leak
failure, the frontend-side equivalent of the "improper error messages"
concern already checked for on the backend
(`kencleng-agentic-workflow.md` §8.1) but with no corresponding
`best-practices/` file on the frontend side.

**2. AI-design-tool-prototype-to-production translation** —
`docs/ui-ux/design-reference-usage.md` is a genuinely thorough
"how to consume design-reference/" guide, but it's necessarily tied to
Claude Design's specific export format (the `<script type="__bundler/
template">` bundling, the extraction script) and kencleng's specific stack
(Tailwind config, `components/ui/` structure). The pattern underneath it —
which parts of an AI-generated prototype transfer directly (composition,
states, copy, a11y) versus which parts must be translated and never copied
verbatim (inline token-referencing styles, hardcoded spacing, the tool's
own scratch component primitives, mock data, local state) — is a reusable
discipline for any project using this now-common workflow (AI design tool
→ visual/structural precedent → real implementation), not something tied
to kencleng or to Claude Design specifically.

## Proposed change

Two new files under `best-practices/react/`, following the existing
Location → Principle → Bad → Good → Checklist format. Full content is
drafted in place at the paths listed above — see those files directly for
the actual proposed text (each includes worked Bad/Good code examples,
consistent with every other file in this category).

Corresponding `index.md` updates: 2 new table rows with keywords and
one-line summaries. Neither file is proposed as `security-critical: yes`
— the state-conventions file touches an info-leak-adjacent concern (raw
error text exposure) but isn't primarily a security file the way
`pwa/xss-and-content-sanitization.md` is; reviewer's call whether that
should change the Security Concern Map classification on merge.

## Rationale

Both are genuinely generic — no kencleng-specific route names, copy, or
token values appear in either file; the AI-prototype file is written
tool-agnostically (references "AI design tools (Claude Design, v0, and
equivalents)" rather than assuming Claude Design specifically).

Same "generic knowledge first, real-case enrichment later" pattern as
0001 and the rest of `best-practices/` — no real kencleng frontend story
has run through this workspace's phases yet, so neither file has a
worked example grounded in an actual kencleng bug; expected to follow
as the `account` domain's frontend track runs.

One thing deliberately **not** proposed here: genericizing `patterns.md`'s
six page-pattern taxonomy (List/Detail/Form/Dashboard/Curation/Status)
itself into `best-practices/`. That's closer to a UX-methodology/spec
document than a best-practices file in this workspace's existing sense
(all current files are code-level Bad/Good patterns, not page-shape
taxonomies) — a different kind of content that doesn't fit the existing
format without stretching it, and isn't proposed here.