# 0004 — New `react/` best-practices category (frontend-general, sibling to `pwa/`)

**Status:** Proposed
**Date:** 2026-08-23
**Triggered by:** Frontend workflow discussion for kencleng, ahead of the `account` domain's frontend track starting (backend track for `account` is underway/near done; frontend is still scaffold-only — no real story/task to ground examples in yet, see Rationale)
**Target area:** best-practices
**Target file(s):**
- New folder: `best-practices/react/` — 6 new files:
  - `react/accessibility-fundamentals.md`
  - `react/server-client-component-boundary.md`
  - `react/form-validation-boundary.md`
  - `react/data-fetching-conventions.md`
  - `react/component-test-mocking-discipline.md`
  - `react/api-client-centralization.md`
- `best-practices/index.md` — 6 new rows, 1 Security Concern Map entry (`client-security`), updated coverage note

Full file contents are drafted in place under `best-practices/react/` and in the
updated `best-practices/index.md` — this proposal doesn't restate them inline
(they're substantial, e.g. worked code examples per file); see those files
directly for the actual proposed content. This doc records the gap and
rationale per the proposal process.

## Gap found

`best-practices/pwa/` (5 files: token storage, XSS sanitization, service
worker caching, state boundaries, offline/sync) is the only frontend-facing
category, and every file in it is security-critical by design — correct as
far as it goes, but it leaves zero coverage for correctness/quality concerns
that are just as likely to show up in agent-generated frontend code:

1. **Accessibility** — kencleng's own `docs/kencleng-agentic-workflow.md` §14
   names an "a11y check" gate explicitly, but no document (in kencleng or
   this workspace) defines what that check verifies. An agent running that
   gate today would have to improvise criteria each time.
2. **Server/Client Component boundary** (RSC frameworks, e.g. Next.js App
   Router) — a real trust-boundary risk (server secrets bundled into client
   JS, per-user server-fetched data cached and served cross-user), not
   covered anywhere.
3. **Form validation boundary** — kencleng's own `frontend/AGENTS.md`
   declares "no business logic in the frontend, client validation is UX
   only" as a hard rule, but nothing documents *how* to keep the client
   schema from silently drifting from the backend's actual rules.
4. **Data-fetching (TanStack Query) conventions** — `pwa/state-management-
   boundaries.md` covers Zustand/session-identity invalidation but not
   server-state query-key hygiene or mutation-invalidation discipline.
5. **Component test mocking discipline** — MSW is the chosen mocking
   strategy (`kencleng-frontend-tech-stack.md`), but nothing documents the
   over-mocking failure mode (mocking the hook instead of the network layer)
   that defeats the point of choosing MSW in the first place.
6. **API client centralization** — `restapi/csrf-and-cookie-security.md` and
   `pwa/token-storage-and-refresh.md` each assume their guarantees (CSRF
   header, token attachment) are applied consistently, but neither says
   *how* that consistency is actually achieved across every call site.

Secondary, non-blocking observation: `pwa/` as a folder name is a partial
mismatch for its own current contents — only 2 of its 5 files
(`service-worker-caching.md`, `offline-and-sync.md`) are PWA-specific;
the other 3 are general SPA/React security concerns that happened to be
filed there. Not part of this proposal (no file moves proposed here,
to keep this change additive-only) — flagged for a separate future
proposal if it's ever worth the churn.

## Proposed change

Add `best-practices/react/` as a new category, sibling to `pwa/`, scoped to
general React/Next.js concerns (correctness, accessibility, testing,
data-fetching) — while `pwa/` stays scoped to offline/service-worker/
installability specifically. Six files as listed above, each following the
existing file format (Location → Principle → Bad → Good → Checklist,
matching e.g. `pwa/xss-and-content-sanitization.md`).

Corresponding `index.md` updates:
- 6 new table rows under a `react` category, keywords and one-line summaries
  per file
- `server-client-component-boundary.md` added to the Security Concern Map
  under `client-security` (marked `security-critical: yes` — leaking
  server-only secrets/env into client bundles, or serving one user's
  server-fetched data to another via a caching default, are both real
  security failures, not just correctness ones)
- Coverage note updated to include `react/` and note these files are
  written from general React/Next.js knowledge, not yet grounded in a real
  kencleng frontend story/task

## Rationale

Genuinely generic — nothing in any of the 6 files references kencleng
specifically; all six patterns (a11y baseline, RSC trust boundary, client/
server validation drift, query-key hygiene, test-mocking discipline,
centralized API client) apply to any React/Next.js + TanStack Query +
MSW-tested frontend, not just this project.

This follows the same "generic knowledge first, real-case enrichment later"
pattern already used for every other category in `best-practices/`
(including `pwa/` itself, whose files predate any real kencleng frontend
code) — distinct from `workflow/`, where structure is meant to be earned
through observed friction rather than seeded upfront. No real frontend
story/task has run through this workspace's phases yet, so none of these six
files have a worked example grounded in an actual kencleng bug yet; that's
expected to follow as the `account` domain's frontend track runs, per the
same enrichment pattern as everywhere else.

One item **not** included here, flagged as a candidate for a future,
separately-evidenced proposal rather than bundled into this one: promoting
kencleng's own frontend gate order (`kencleng-agentic-workflow.md` §14 step
3 — lint → component test → contract check → a11y check) into
`workflow/5-testing/`. That's a `workflow/` change, not `best-practices/`,
and per this workspace's "structure earned, not preemptive" principle for
`workflow/`, it should wait until it's actually been run against a real
frontend task and any friction is observed — not proposed speculatively
alongside this content-only addition.