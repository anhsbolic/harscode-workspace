# New category: hybrid-monolith/

**Status:** Proposed
**Date:** 2026-09-07
**Protection Tier:** general
**Triggered by:** locking the frontend data-fetching approach for a new Inertia.js-based project, surfacing a rendering-mechanism decision that doesn't fit any existing category
**Target area:** best-practices
**Target file(s):**
- `best-practices/hybrid-monolith/server-vs-client-driven-rendering.md` — new file
- `best-practices/index.md` — new `hybrid-monolith` category row

## Gap found

`restapi/` covers pure REST API contract concerns (pagination, idempotency, CORS) and `react/` covers React/Next.js-specific frontend concerns — neither is the right home for architectures where a server-rendered bridge (Inertia.js, Turbo/Hotwire, HTMX, and similar) delivers most page data via the initial server-driven render, while some interactions still need client-side fetching (search/autocomplete, polling, anything that shouldn't trigger a full page visit). The concrete failure mode: when the same underlying data is refreshed by two different mechanisms for the same page — a server-driven page reload/revisit and a client-side cache invalidation — the two can race and disagree about the current state, and it's easy to lose track of which mechanism is supposed to own which piece of data as a codebase grows.

## Proposed change

Add a new `best-practices/hybrid-monolith/` folder with one file (full content below), plus a new row in `best-practices/index.md`.

### `index.md` addition

New row in the main trigger-keyword table:

| Category | File | Trigger keywords | Security-critical | Summary |
|---|---|---|---|---|
| hybrid-monolith | [hybrid-monolith/server-vs-client-driven-rendering.md](hybrid-monolith/server-vs-client-driven-rendering.md) | inertia, turbo, htmx, server-driven render, client-driven fetch, page props, partial reload | no | Choose server-driven (initial page render) vs client-driven (separate fetch) per data need explicitly; never let both mechanisms refresh the same data for the same page, which causes races and stale state |

No Security Concern Map entry — this is an architectural/consistency concern, not itself a security concern.

### New file

See attached file content (`server-vs-client-driven-rendering.md`) — full text ready to paste into `best-practices/hybrid-monolith/`.

## Rationale

The principle applies to any server-rendered-bridge architecture (Inertia.js, Turbo/Hotwire, HTMX, similar patterns), not to Inertia specifically — the example uses Inertia because it's the most common current instance, but the underlying decision (server-driven vs client-driven per data need, and never mixing both for the same data) is the same regardless of which specific bridge library is used. This is a distinct category from `react/` because the decision point here is about *which mechanism delivers the data in the first place* (page props vs a separate fetch) — a question that doesn't exist in a pure SPA or a pure Next.js app, both of which `react/`'s existing files already assume one delivery mechanism (client-side fetching) for. It doesn't belong in a project's own `AGENTS.md` because the race-condition failure mode and the decision criteria are the same on any hybrid-monolith stack, independent of project domain.

---

*After human review: update the Status above. If Accepted, merge into
the target document and leave this proposal in place (don't delete
it) — it serves as this folder's changelog. See `proposals/README.md`
for the Protection Tier distinction and numbering convention.*
