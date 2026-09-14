# Proposal: Add a "Domain Closure Review" Checklist to `harscode-workspace/workflow`

**Status:** Proposed
**Date:** 2026-09-12
**Origin:** Domain `akun` (D01) closure audit
(`.agents-local/backend/domain-reports/D01-domain-akun-closure-audit.md`) — Anhar asked, before that
audit began, for a standard review process to make sure a domain can be reliably declared "done,"
the same way the audit had just been performed manually. He explicitly asked for this proposal to
come **last**, after the audit's own findings were actually resolved, so it would be grounded in
what really happened rather than upfront guesswork.
**Proposed scope:** a new reusable workflow document/phase — this is process guidance applicable
across projects, not a `koperasiqu-web-app`-specific decision, matching the precedent already set by
proposal 0002 (`.agents-local/backend/proposals/0002-trim-code-comment-verbosity-guideline.md`),
which targets the same external workspace for the same reason.
**Target area:** `harscode-workspace/workflow/` — recommended as a new `domain-closure/` document
alongside the existing per-feature phases (`1-exploration/` through `6-pull-request/`), though the
exact final placement/split is left to whoever applies this (see the staged draft's own closing
note).

## Context

`harscode-workspace/workflow/` already defines a reusable, per-feature pipeline — explore, techplan,
build, code-review, test, pull-request — used across (at least) this project's domain-`akun` work.
Nothing in that pipeline operates at the *domain* level: each feature verifies itself against its
own techplan, but nothing checks the domain as a whole once every feature inside it has gone
through that pipeline individually.

That gap was concrete, not theoretical, in this project's own domain `akun`: by the time all 9
features (D01-01 through D01-09) had individually reached a "testing" commit, the domain still had
a fully-unbuilt feature hiding behind that appearance — D01-09 (Admin Pusat authentication) had
been decomposed into 5 tasks during its own techplan phase, and only the first (a foundation/data
layer) had ever been built. Every one of that feature's own reports was honest about this (the
testing report literally said "this Pass isn't mistaken for 'the feature is done'"), but nothing in
the existing per-feature pipeline forces a *domain-level* rollup that would have caught it before
someone declared the whole domain finished.

The manual audit that followed (linked above) found five more issues nothing in the existing
pipeline was positioned to catch, precisely because each one only becomes visible at the
whole-domain level: a stale permission name in "already revised" API contract text, a hardcoded
value where a sibling implementation right next to it was already config-driven, a live Golden Rule
violation from pre-domain boilerplate nobody had gotten around to retiring, a domain-wide task
(a global rate limiter) that didn't map to any single feature's task list and so was never built by
anyone, and a manual-testing collection that had quietly fallen behind as later features shipped.

## Recommendation

Add a "Domain Closure Review" checklist/guideline document to `harscode-workspace/workflow/`,
staged in full at `.agents-local/backend/proposals/domain-closure-review-checklist-draft.md`
(alongside this proposal, same pattern as proposal 0005's staged replacement YAML) — ready to paste
in, not a summary to rewrite from scratch. It defines: when this review runs (once, after every
feature in a domain finishes its own per-feature pipeline, before the domain is declared done); an
8-point checklist covering spec-delivery completeness, API-contract cross-checking, cross-artifact
consistency, cross-session change-log review, testing-docs completeness, a general Golden-Rule/
boilerplate sweep, a regression-testing protocol specifically for domain-wide changes, and a
tie-breaker rule for contract-vs-"mirrors X" conflicts within one techplan; and an explicit
instruction to keep a running Progress Log during execution as raw material for revising the
checklist itself later, rather than treating it as frozen after this first version.

## Impact / Scope of Applying This

Process-only. Adds a new document to `harscode-workspace/workflow/`; changes nothing about any
already-shipped code in `koperasiqu-web-app` or any other project. Future domains (D02 onward, in
this project or others using the same workspace) would run this review once their features'
individual pipelines finish, before being declared closed — a new checkpoint, not a change to the
existing per-feature phases.

## What This Proposal Does NOT Do

- Does not write into `harscode-workspace/` directly — that's a separate repo outside this
  session's primary working directory, same constraint that governs every `docs/`-repo proposal in
  this same folder (`.agents-local/backend/proposals/`), applied here to a different external repo
  for the same structural reason.
- Does not retroactively re-run this checklist against any domain other than `akun` (D01) — the
  linked audit is the one, already-completed worked example this checklist is drawn from, not a
  claim that every other already-"closed" domain needs re-auditing as a consequence of this
  proposal existing.
- Does not decide the exact file/folder split within `harscode-workspace/workflow/` (one document
  vs. `guidelines.md`/`checklist.md`/`examples.md` matching the existing per-phase convention) — the
  staged draft flags this explicitly as left to whoever applies it, since that's a judgment call
  about that workspace's own conventions best made from inside it.
- Does not make this checklist mandatory-by-tooling in any way — like every other phase in
  `harscode-workspace/workflow/`, it's a guideline followed by convention, not enforced by a script
  or gate.
