# Next.js Engineer — Knowledge Index

> This is **self-contained NextJS Builder Agent knowledge**, not a pointer to external technical handbooks and not a project-wide policy. Use only the relevant topics for the actual assignment. Effective project-owned standards, SOP, accepted contracts, framework version and Human instructions take precedence; no fixed testing framework, API architecture, CSS system or library is selected here.

## Trigger-based reading map

| Actual concern | Read | Why |
| --- | --- | --- |
| Next.js routes, layouts, Server/Client components, caching, rendering, metadata | [Rendering & Routing](knowledge/rendering-and-routing.md) | Runtime/trust boundaries, routing and UI states |
| Data fetching, query cache, URL/form/local state, identity changes, optimistic views | [State & Data Ownership](knowledge/state-and-data.md) | Prevent duplicate truth and stale/cross-account state |
| HTTP/typed APIs, `MOCK_DEVELOPMENT`, `REAL_API_INTEGRATION`, mutations, forms, error/unknown outcomes | [API Modes & Forms](knowledge/api-modes-and-forms.md) | Consume actual contract faithfully without mock drift |
| Components, design implementation, accessibility, responsive layout, visual/copy quality | [UI Implementation & Craft](knowledge/ui-implementation-and-craft.md) | Usable, truthful, purposeful production experience |
| Security/privacy, authorized testing, actual evidence and limited tool readiness | [Security & Verification](knowledge/security-and-verification.md) | Contain material risk; avoid unsupported completion claims |

## Application rule

Start with the [Engineer role contract](agent.md) and [Space I/O](../../contracts.md); load just the topic needed. A rule below is a **decision aid**, not license to override a project's established practice or invent feature semantics. When a proposed technique conflicts with a project rule, use the effective project mechanism unless it would violate higher-priority safety/authorization; report the material conflict and hold the affected action. Record important deviations in implementation evidence, not another mandatory standards file.
