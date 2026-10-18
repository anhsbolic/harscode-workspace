# React API Client Boundaries

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** Browser/frontend HTTP request handling, credential modes, CSRF, retries and error contracts.
> **Triggers:** fetch, API client, session, cookie, bearer, CSRF, 401, retry, OpenAPI, credentials.

## 01 — Applicability

Use when several frontend calls need common transport/error behavior. Authentication transport, cookie policy, token refresh and CSRF defenses depend on **the chosen backend/session design**. Do not import a previous project's security contract by copying its client wrapper.

## 02 — Principle / Rule

- Centralize genuine shared mechanics (base URL, safe error parsing, consistent response typing, correlation/tracing, applicable credentials) **where it reduces drift**. Do not force a single global wrapper for unrelated APIs.
- Attach authentication and CSRF headers/cookies **only according to the active backend contract and threat model**. Neither in-memory bearer token, `credentials: "include"`, nor `X-Requested-With` is universally required or sufficient to defeat CSRF.
- Never put raw secrets in URLs/logs; do not expose untrusted server error text directly in the UI.
- An auth-refresh flow must **actually retry** the original permitted request after successful refresh if the contract promises it; cap refresh/retry attempts and guard against loops.
- A failed or unknown-response state-changing request cannot be blindly replayed; establish idempotency/replay safety first.
- Treat client role visibility as UX only; protected decisions remain backend-authorized.

## 03 — Rationale & Risk

A hardcoded template can silently choose a cookie+bearer architecture, leak token headers across origins, retry a non-idempotent create, or hide a broken 401-refresh path. Blind reuse of header conventions may create security theater rather than a real defense.

## 04 — Application Guidance

1. Bind the client to the selected API origin and OpenAPI operations, accepted status/error shape, and actual browser/server boundary.
2. Choose credentials mode based on same-origin/cross-origin deployment and session policy; enforce allowed origins server-side. If cookies are sent automatically for state changes, adopt an actual CSRF defense (e.g. origin checks and suitable token/header scheme), not just a decorative header.
3. On 401, refresh only where the chosen protocol permits it, deduplicate concurrent refresh attempts when needed, and replay **at most once** only when request body and effect semantics are safely repeatable.
4. Treat network uncertainty and application errors separately. Map failures to truthful UI states rather than always assuming creation failed.
5. Keep generated API types consistent with the source contract; avoid handwritten competing success/error meanings.

## 05 — Verification

Exercise actual 2xx, expected 4xx, 401 refresh success/failure, forbidden origin/CSRF, concurrent refresh, replay prevention for mutation, timeout/unknown result and token-free logging. Confirm request method/body/headers on a real retry when enabled. Omit auth-refresh tests if no refresh protocol is selected; record non-applicability.

## 06 — Boundaries & Trade-offs

A simple server-rendered application may not need an elaborate API client. Cookie sessions and bearer tokens require different defenses. This guidance does not choose an identity provider, authentication architecture, token lifecycle or refresh strategy.

## References

- https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
- https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html
- https://www.rfc-editor.org/rfc/rfc9110.html
