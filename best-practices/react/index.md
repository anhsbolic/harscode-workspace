# React Best-Practices Index

Use this subindex when the active concern is already known to be React/Next.js UI work. Match the current task/phase to the smallest applicable row and open only those target files.

| Concern | Guidance | Typical triggers |
|---|---|---|
| accessibility | [accessibility-fundamentals.md](accessibility-fundamentals.md) | semantic HTML, keyboard, focus, ARIA, contrast |
| server/client boundary | [server-client-component-boundary.md](server-client-component-boundary.md) | RSC, `use client`, server-only code, secrets |
| App Router | [app-router-routing-conventions.md](app-router-routing-conventions.md) | route segments, loading/error/layout, metadata |
| form validation | [form-validation-boundary.md](form-validation-boundary.md) | client validation, Zod, 422, schema drift |
| state ownership | [state-ownership-and-derivation.md](state-ownership-and-derivation.md) | local/global/URL/server state, duplicated derived state |
| data fetching | [data-fetching-conventions.md](data-fetching-conventions.md) | TanStack Query, query keys, invalidation, waterfalls |
| component boundaries | [component-composition-and-abstraction.md](component-composition-and-abstraction.md) | extraction, reusable/shared components, composition, prop explosion |
| component testing | [component-test-mocking-discipline.md](component-test-mocking-discipline.md) | RTL, Vitest, MSW, over-mocking |
| API client | [api-client-centralization.md](api-client-centralization.md) | auth headers, CSRF, credentials, raw fetch |
| loading/empty/error | [loading-empty-error-state-conventions.md](loading-empty-error-state-conventions.md) | skeletons, empty state, partial failure, error copy |
| responsive layout | [responsive-layout-robustness.md](responsive-layout-robustness.md) | breakpoints, overflow, wrapping, realistic content |
| prototype translation | [ai-prototype-to-production-translation.md](ai-prototype-to-production-translation.md) | design exports, mock data, inline styles, prototype code |
| visual verification | [visual-verification.md](visual-verification.md) | rendered UI, visual QA, responsive/design comparison |
| testing automation boundary | [testing-automation-boundary.md](testing-automation-boundary.md) | lint enforcement, objective runtime/rendered checks |

## Retrieval rule

```text
task + role/specialization + workflow phase
→ matching concern row(s)
→ target guidance
→ STOP
```

Do not read every React file because the task is frontend work. Cross-cutting security concerns may additionally route through `../index.md`'s Security Concern Map when the narrower rows above do not already cover the active risk.
