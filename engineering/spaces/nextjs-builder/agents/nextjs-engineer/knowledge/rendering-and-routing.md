# Next.js Rendering, Routing, and Execution Boundaries

> **Applicable when:** assignment affects App Router/Pages Router, server and browser code, route structure, rendering, metadata, caching or hydration. Framework version and project configuration must be inspected first; examples are not assumptions about Next.js defaults.

## Server versus browser ownership

Classify every module by required runtime, data sensitivity and interaction needs. Code intended only for the server—including credentials, privileged service calls, private configuration and server-only dependencies—must not become reachable from browser bundles or client-import paths. Mark and enforce boundaries using supported project/framework mechanisms, not file suffix assumptions alone. Browser-facing state may be necessary for interactions, but client components do not become the authority for permissions or business effects.

Before moving fetching from server to browser or vice versa, examine data freshness, request identity, SEO/initial-load requirements, streaming, error handling, session/cookie transport and the actual deployment topology. Avoid marking a whole component tree client-side merely to enable one interactive control; isolate interactivity at a sensible boundary if this reduces cost without hiding state semantics.

## Rendering, caching and hydration

Server-rendered and hydrated output should agree on initial observable meaning. Non-deterministic browser-only values, current time, user-specific storage and viewport assumptions need an explicit safe rendering strategy—not a superficial hydration-warning suppression. Verify version-specific caching defaults against the installed Next.js release and actual project conventions. Private/session-derived reads must never be cached or reused across identities. Invalidate, scope or re-read data when session/resource identity changes; “works on first load” does not demonstrate safe navigation or freshness.

Failure signals include: a server secret imported by client code, one account's data surviving another account's session, stale status presented as current, hydration mismatch, or a UI that reveals unauthorized fields through serialized props despite visual masking.

## Route composition and navigation

Select route segments, layouts, route groups, dynamic parameters, navigation links, loading and error boundaries for real semantics. A persistent layout is for genuinely persistent shell/state; do not put feature data there merely for folder organization. Loading/error boundaries belong where separate pending/failure behavior is meaningful, not mechanically on every route. Route grouping or parallel slots require an observable composition/access/load/failure benefit that outweighs added complexity.

Honor effective Information Architecture and navigation authority. A sitemap document is not universally required; route relationships and access must still be unambiguous when material. Do not infer product navigation from a prototype screenshot alone. Metadata, robots/indexing, redirects and public/private route exposure follow project scope and current framework APIs, not an assumed “always optimize SEO” template.

## Evidence and trade-offs

For affected route/rendering behavior, provide exact code revision and representative navigation, loading/error and identity scenarios that were **actually observed** using SOP-permitted methods. Build/type success proves compilation, not layout, session isolation or security. If runtime/browser is unavailable, identify the unverified boundary and consumer/owner of the next check rather than claiming rendered success.
