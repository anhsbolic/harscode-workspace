# App Router Routing Conventions

> Status: DRAFT — not yet grounded in real Kencleng examples. Enrich with real route
> structure/PR references once the first App Router stories land, same pattern as every
> other file in this folder.
>
> Scope note: this file covers route-segment file conventions (loading/error/layout),
> route composition (groups/parallel routes), and metadata. It deliberately does NOT
> cover Server/Client Component boundary or secrets-bundling risk — that's
> `server-client-component-boundary.md`'s scope. If a topic could go either place,
> it belongs there if it's about *what can safely execute where*, and here if it's
> about *how routes are structured and composed*.

## Layout / loading / error placement

- `loading.tsx` per route segment only where the data fetch is nontrivial enough to
  need a visible loading state — don't add it reflexively to every segment; an
  instant/cached fetch with a flashing skeleton is worse UX than no loading state.
- `error.tsx` per route segment that can meaningfully fail independently of its parent.
  Don't rely solely on a root-level error boundary if a nested segment's failure
  shouldn't take down the whole page — e.g. a sidebar widget failing shouldn't blank
  the main content.
- Shared layout state (nav, sidebar, persistent chrome) belongs in `layout.tsx`, not
  re-fetched or re-rendered per page — that's the point of a layout persisting across
  navigations within its segment. A layout re-fetching on every child navigation is a
  sign the layout boundary was drawn at the wrong level.

## Route groups

`(groupName)` organizes routes without affecting the URL. Use for separating route
trees that share a concern but not a URL prefix — most commonly an authenticated vs
public route tree living under one layout structure, or grouping by team/feature area
in a large app without polluting the URL.

Don't use route groups purely for file-tree tidiness if the routes don't actually share
a meaningfully different layout or access-control boundary — that's organizing files,
not routes, and a plain folder without the parens does the same job with less
indirection.

## Parallel routes

`@slot` conventions are for genuinely independent, simultaneously-visible sections that
need independent loading/error states — e.g. a dashboard with widgets that load and
fail independently of each other. This is real complexity (extra files, `default.tsx`
per slot, careful handling of unmatched routes) — justified only by that specific need,
not reached for as default page composition. If the sections aren't actually
independent (one depends on another's data, or they always succeed/fail together), a
single component with internal state is simpler and correct.

## Metadata & SEO

Use `generateMetadata` (async, for dynamic per-route metadata like a product title
pulled from fetched data) or the static `metadata` export (for routes with fixed
metadata) — not manual `<head>` tag management. `generateMetadata` blocks rendering
until it resolves, so keep the data it depends on lean; don't fetch the full page
payload just to read a title field if a lighter query can supply it.

## Self-check before merging a PR touching routes/layouts

- [ ] `loading.tsx`/`error.tsx` added deliberately per segment — present where a
      nontrivial fetch or independent-failure risk exists, not copy-pasted everywhere
      or missing where it's actually needed
- [ ] Layout only holds state/UI that's genuinely persistent across the segment's
      child routes — not re-fetching per navigation
- [ ] Route group used for a real shared-layout/access-boundary reason, not just
      file-tree organization
- [ ] Parallel routes used only where sections are genuinely independent in loading/
      failure — not the default way to compose a page
- [ ] `generateMetadata`/`metadata` used instead of manual `<head>` tags; async
      metadata doesn't over-fetch just to populate a title