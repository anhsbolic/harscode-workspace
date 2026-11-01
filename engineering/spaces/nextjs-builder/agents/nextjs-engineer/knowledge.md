# Next.js Engineer — Applied Capability Knowledge

> **Non-binding Agent-owned reference**, not framework documentation, project architecture, mandated stack or active Harscode `main` policy. Project-owned current Engineering/Design/security/testing SOP and actual Next.js version prevail. Source material was selectively reviewed from the operational `main` legacy `best-practices/react/*` lineage; Foundation archive is `deprecated/legacy/`. **Do not treat legacy examples as authority.**

## Technical decision order

1. Read effective target-project work/requirements/Design, frontend architecture, security and testing SOP. Inspect actual Next.js version, Router mode and existing code. Verify uncertain or version-sensitive mechanisms against current relevant framework sources before changing them.
2. Identify authoritative state, action/result meaning, API/provider standing and trust boundary; derive deterministic values rather than store synchronized copies.
3. Choose the smallest correct implementation: route-local composition for local concerns, shared components only when genuine stable semantics benefit; no speculative state stores, generic SDKs, adapters or event engines.
4. Distinguish server-only code/secrets from browser code; check cache and identity scoping for per-user data, including SSR/hydration and client query cache invalidation. Routing, layouts, loading/error boundaries and metadata follow actual project and framework version.
5. For API work, derive request/response/result types from effective canonical/accepted contracts where available; use appropriate project client/data fetching pattern and separate network/transport failure from typed server denial, application success and genuinely unknown effect. Preserve auth/CSRF/session/replay/idempotency/PII meaning. No frontend role checkbox as backend permission.
6. Keep client validation helpful, not source of backend validity. Design correct error/empty/loading/denied/unknown and long-content states; preserve keyboard/focus and responsive information. Client state, form state and query state have distinct appropriate owners.
7. Build against project assets, tokens, icon family and copy rules. Translate prototype composition/intent into real project styling/components/state/API; never copy untrusted scratch mocks/inline style infrastructure blindly.
8. Follow project testing SOP: no universal Playwright, Vitest, coverage floor or silent automation; run only permitted applicable checks. Compiler/lint or mocked test does not establish rendered, real-backend or release success. Record observed evidence and unresolved limitations.

## Targeted legacy provenance and cautions

Candidate portable principles were source-reviewed at `anhsbolic/harscode-workspace@8604bc39dfdb5692b9f3363fdca99fd510936c32` under:
- `best-practices/react/server-client-component-boundary.md`
- `best-practices/react/state-ownership-and-derivation.md`
- `best-practices/react/component-composition-and-abstraction.md`
- `best-practices/react/data-fetching-conventions.md`
- `best-practices/react/form-validation-boundary.md`
- `best-practices/react/app-router-routing-conventions.md`
- `best-practices/react/api-client-centralization.md`
- `best-practices/react/ai-prototype-to-production-translation.md`
- `best-practices/react/loading-empty-error-state-conventions.md`

**Known legacy defects:** examples of bearer-in-memory tokens, automatic `401` refresh retries, cookie/CSRF headers, universal API client wrapping or skeleton-over-spinner are **not universal mechanisms**. Current project auth, deployment and behavior control actual choices. App Router routing legacy guide was DRAFT; re-evaluate version-sensitive details. Mock-first defaults are assignment mode rules, not license to fabricate missing interface semantics.

Security applies only where concern is present and never substitutes for backend-owner protection. Refer independently to applicable project-owned standards for auth, authorization, privacy, API, dependency and logging obligations; request expert assessment when beyond competence.
