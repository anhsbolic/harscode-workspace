> **Location:** `best-practices/index.md`

# Best Practices Index

Scan this table first. Match `Trigger keywords` against the area being explored/planned,
then open only the matching file(s) — don't read every file in `best-practices/`.

For anything security-relevant, check the **Security Concern Map** below first — it
groups security-critical files by concern across folders, so you don't have to scan
every category's row to find what's relevant to auth, secrets, PII, etc.

| Category | File | Trigger keywords | Security-critical | Summary |
|---|---|---|---|---|
| go | [go/error-handling.md](go/error-handling.md) | error, return, result, wrapping, constant, literal | no | Result/error contract correctness (`return a, b` staleness); named constants for load-bearing literals |
| go | [go/abstraction-boundaries.md](go/abstraction-boundaries.md) | SRP, signature, extraction, pure function, side effect, mock | no | Function signature must not leak extra responsibility; separate pure predicate from side-effecting action; avoid single-caller abstraction layers |
| go | [go/feature-lifecycle.md](go/feature-lifecycle.md) | flag, toggle, TODO, not-yet-active, comment out | no | Disable an incomplete/blocked feature with a flag, not commented-out code |
| go | [go/naming-and-scope.md](go/naming-and-scope.md) | naming, variable, test scope, mock, duplicate test | no | Variable naming should reveal source/purpose, not just shape; test at the lowest level that exposes the behavior |
| go | [go/goroutine-lifecycle.md](go/goroutine-lifecycle.md) | goroutine, leak, concurrency, WaitGroup, errgroup, unbounded | no | Goroutines with no exit path leak; unbounded per-item goroutine spawning under load; use ctx-aware primary calls not outside timeouts |
| go | [go/context-propagation.md](go/context-propagation.md) | context, ctx, cancellation, deadline, Background, TODO | no | context.Background() mid-chain breaks cancellation propagation; don't store ctx in a struct field; long-running work must poll ctx.Done() |
| go | [go/nil-and-zero-values.md](go/nil-and-zero-values.md) | nil, nil map, nil slice, nil pointer, zero value, JSON null | no | Nil map write panics (read doesn't); nil vs empty slice serializes differently (null vs []); nil pointer method calls depend on receiver dereference |
| go | [go/error-wrapping.md](go/error-wrapping.md) | error wrapping, errors.Is, errors.As, %w, %v, sentinel error | no | Don't string-match err.Error(); %w preserves the error chain for errors.Is/As, %v silently breaks it |
| go | [go/defer-pitfalls.md](go/defer-pitfalls.md) | defer, LIFO, resource leak, file descriptor, named return | no | defer in a loop accumulates until function return, not per-iteration; deferred args evaluated immediately, not at execution time; LIFO cleanup order |
| go | [go/interface-and-slice-semantics.md](go/interface-and-slice-semantics.md) | interface nil, typed nil, error interface, slice aliasing, sub-slice | no | Typed nil pointer stored in an interface is not a nil interface; sub-slices share underlying array, mutation/append can silently affect the caller's data |
| go | [go/struct-copying-and-time.md](go/struct-copying-and-time.md) | mutex, copylocks, sync.Mutex, time.Time, monotonic clock, timezone | no | Copying a struct containing sync.Mutex breaks locking; time.Time == comparison fails on monotonic clock differences, use .Equal() |
| go | [go/input-validation-and-injection.md](go/input-validation-and-injection.md) | log injection, command injection, exec.Command, shell, boundary validation | yes | Unsanitized input in log lines enables log forging, prefer structured logging; shelling out with user input risks command injection; validate at the boundary |
| go | [go/secrets-and-sensitive-logging.md](go/secrets-and-sensitive-logging.md) | secrets, PII, sensitive data, logging, redact, %+v | yes | Logging an error verbatim can leak sensitive data it wraps; logging a struct wholesale (%+v, full marshal) leaks any sensitive field it contains |
| go | [go/http-client-and-transport.md](go/http-client-and-transport.md) | http.Client, timeout, DefaultClient, connection pool, transport reuse | no | http.DefaultClient and zero-value http.Client have no timeout; constructing a new client per request exhausts connections instead of reusing the pool |
| go | [go/panic-and-recover.md](go/panic-and-recover.md) | panic, recover, goroutine crash, defer recover | no | Panic in a spawned goroutine crashes the whole process unless that goroutine has its own recover; scattering recover across layers hides bugs instead of fixing them |
| go | [go/decimal-and-money.md](go/decimal-and-money.md) | decimal, rounding, money, float precision, currency | no | Never round-trip money through float64; explicit rounding mode; compare decimals with .Equal() |
| go | [go/jwt-and-token-lifecycle.md](go/jwt-and-token-lifecycle.md) | jwt, token, refresh token, mfa, signing key, token rotation | yes | Separate keys/algorithms per token purpose; refresh rotation + reuse detection |
| go | [go/rate-limiting.md](go/rate-limiting.md) | rate limit, throttle, lockout, token bucket | yes | Per-key limiter with idle-key eviction to avoid a memory leak |
| go | [go/file-upload-handling.md](go/file-upload-handling.md) | file upload, multipart, content-type, magic bytes | yes | Sniff magic bytes, cap size server-side, stream instead of buffering |
| go | [go/testing-concurrency.md](go/testing-concurrency.md) | race condition, goroutine, shared state, -race | no | go test -race + invariant-asserting concurrent tests |
| go | [go/integration-testing-setup.md](go/integration-testing-setup.md) | integration test, build tag, real database, DATABASE_URL, live Postgres, testcontainers | no | Gate DB-dependent tests behind `//go:build integration`; reserve for constraint/transaction/query-validity checks a fake repo can't prove |
| go | [go/authorization-and-idor.md](go/authorization-and-idor.md) | authorization, IDOR, ownership check, resource scope, access control | yes | Resource-level scope check, separate from role check |
| go | [go/role-and-privilege-separation.md](go/role-and-privilege-separation.md) | role separation, privilege escalation, incompatible roles, recuse | yes | Role-exclusivity constraints enforced server-side, not just UI |
| go | [go/webhook-signature-verification.md](go/webhook-signature-verification.md) | webhook, callback signature, hmac verification, replay protection | yes | Signature verification + replay protection on inbound callbacks |
| go | [go/secrets-and-key-management.md](go/secrets-and-key-management.md) | secrets, key management, key rotation, env secrets | yes | One key = one purpose; never reuse a key across concerns |
| go | [go/dependency-and-supply-chain.md](go/dependency-and-supply-chain.md) | dependency scanning, govulncheck, supply chain, package pinning | yes | Manual vulnerability scanning discipline without CI automation |
| postgresql | [postgresql/indexing-and-query-plans.md](postgresql/indexing-and-query-plans.md) | index, query plan, EXPLAIN, seq scan, LIKE, composite index, covering index | no | Function-wrapped predicates defeat indexes; composite index column order; SELECT * defeats covering indexes; LIKE '%x%' needs pg_trgm |
| postgresql | [postgresql/transactions-and-locking.md](postgresql/transactions-and-locking.md) | transaction, lock, deadlock, isolation, FOR UPDATE, outbox | no | Don't call external systems inside a DB transaction; consistent lock ordering to avoid deadlocks; Read Committed non-repeatable read pitfalls |
| postgresql | [postgresql/encryption-at-rest.md](postgresql/encryption-at-rest.md) | encryption at rest, ciphertext, hmac lookup, pii column | yes | Ciphertext for storage, separate HMAC column for lookup |
| postgresql | [postgresql/audit-log-design.md](postgresql/audit-log-design.md) | audit log, redaction, revoke update delete | yes | DB-level immutability + explicit redaction of what's logged |
| postgresql | [postgresql/financial-invariant-enforcement.md](postgresql/financial-invariant-enforcement.md) | balance update, double spend, for update, financial invariant | yes | Row locking / constraint-level enforcement for concurrent balance updates |
| postgresql | [postgresql/migrations-safety.md](postgresql/migrations-safety.md) | migration, backfill, additive migration, reversible migration | no | Additive-first migrations, tested reversibility |
| graphql | [graphql/resolver-n-plus-one.md](graphql/resolver-n-plus-one.md) | N+1, dataloader, resolver, batch, per-item query | no | Per-item resolvers cause N+1 at list scale; dataloaders must be request-scoped, not global; batching alone doesn't fix over-fetching |
| graphql | [graphql/schema-and-error-design.md](graphql/schema-and-error-design.md) | nullable, non-null, schema, breaking change, error union, mutation error | no | Deliberate non-null usage vs null-propagation risk; business errors vs system errors in response shape; what counts as a breaking schema change |
| restapi | [restapi/idempotency-and-versioning.md](restapi/idempotency-and-versioning.md) | idempotent, idempotency key, retry, POST, versioning, breaking change, deprecation | no | Non-idempotent POST double-executes on retry; classify endpoint changes as additive vs breaking before shipping |
| restapi | [restapi/pagination-and-status-codes.md](restapi/pagination-and-status-codes.md) | pagination, offset, cursor, keyset, status code, 4xx, 5xx | no | Offset pagination degrades and drifts under concurrent writes, prefer cursor; status codes must reflect actual failure category |
| restapi | [restapi/anti-enumeration.md](restapi/anti-enumeration.md) | enumeration, timing attack, constant time compare | yes | Generic responses + constant-time comparison to prevent enumeration |
| restapi | [restapi/csrf-and-cookie-security.md](restapi/csrf-and-cookie-security.md) | csrf, samesite, cookie security, refresh endpoint | yes | Cookie-based token flows need explicit CSRF mitigation |
| restapi | [restapi/cors-configuration.md](restapi/cors-configuration.md) | cors, allowed origin, credentials wildcard | yes | Explicit origin whitelist, never wildcard + credentials |
| restapi | [restapi/openapi-spec-first-drift.md](restapi/openapi-spec-first-drift.md) | openapi drift, spec first, codegen, error shape | no | Keep generated code and error-response shape in sync with the spec |
| kafka | [kafka/consumer-and-offset-management.md](kafka/consumer-and-offset-management.md) | offset, commit, consumer group, rebalance, at-least-once, auto-commit | no | Commit offsets only after processing completes; at-least-once requires idempotent handlers; rebalances pause the group |
| kafka | [kafka/producer-and-partitioning.md](kafka/producer-and-partitioning.md) | acks, idempotent producer, partition key, ordering, hot partition | no | Default acks=1 risks message loss, use acks=all + idempotent producer; partition key choice controls both ordering and load distribution |
| pubsub | [pubsub/ack-and-ordering.md](pubsub/ack-and-ordering.md) | ack, nack, ack deadline, ordering key, redelivery | no | Ack only after processing completes; ack deadline shorter than handler time causes duplicates even without failures; ordering needs explicit ordering keys |
| pubsub | [pubsub/retry-and-dead-letter.md](pubsub/retry-and-dead-letter.md) | dead letter, DLQ, retry policy, backoff, poison message | no | No DLQ means a permanently-failing message retries forever silently; retry without backoff amplifies outages |
| redis | [redis/caching-strategy.md](redis/caching-strategy.md) | cache stampede, thundering herd, singleflight, cache invalidation, TTL jitter | no | Concurrent cache misses hammer the DB without stampede protection; multi-key invalidation on write is easy to leave incomplete |
| redis | [redis/key-design-and-safe-commands.md](redis/key-design-and-safe-commands.md) | KEYS, SCAN, TTL, expiry, maxmemory, cluster, CROSSSLOT, hash tag | no | KEYS blocks the event loop under load, use SCAN; every key needs a deliberate TTL decision; multi-key ops need hash tags in cluster mode |
| infra | [infra/security-headers-and-tls.md](infra/security-headers-and-tls.md) | security headers, csp, hsts, reverse proxy | yes | Minimum security-header set enforced at the reverse-proxy layer |
| react | [react/accessibility-fundamentals.md](react/accessibility-fundamentals.md) | accessibility, a11y, aria, focus management, semantic html, keyboard navigation, contrast | no | Semantic HTML over div-soup; accessible names on icon-only controls; explicit focus management on modal/route/async transitions; never color-only signaling |
| react | [react/server-client-component-boundary.md](react/server-client-component-boundary.md) | server component, client component, use client, RSC, env var, secrets bundling | yes | Server-only code/secrets must never be importable from a 'use client' file; explicit no-store caching for per-user server fetches |
| react | [react/form-validation-boundary.md](react/form-validation-boundary.md) | form validation, zod, client validation, 422, validation drift | no | Client schema is UX-only, never source of truth; field-level 422 errors handled distinctly from request-level failures; drift-check on OpenAPI schema changes |
| react | [react/data-fetching-conventions.md](react/data-fetching-conventions.md) | tanstack query, react query, query key, cache invalidation, waterfall, optimistic update | no | Centralized query-key factory; mutation invalidation discipline; avoid sequential-fetch waterfalls; optimistic updates need rollback |
| react | [react/component-test-mocking-discipline.md](react/component-test-mocking-discipline.md) | msw, mock service worker, vitest, react testing library, component test, over-mocking | no | Mock at the network layer not the hook; assert by role/text not implementation detail; loading/error states need dedicated test cases |
| pwa | [pwa/token-storage-and-refresh.md](pwa/token-storage-and-refresh.md) | token storage, silent refresh, in-memory token, broadcastchannel | yes | In-memory access token + HttpOnly refresh cookie, multi-tab sync |
| pwa | [pwa/xss-and-content-sanitization.md](pwa/xss-and-content-sanitization.md) | xss, sanitize, dangerouslysetinnerhtml, user-generated content | yes | Sanitize any bypass of framework auto-escaping |
| pwa | [pwa/service-worker-caching.md](pwa/service-worker-caching.md) | service worker, cache strategy, stale-while-revalidate | no | Cache strategy per resource type; never cache auth-sensitive responses |
| pwa | [pwa/state-management-boundaries.md](pwa/state-management-boundaries.md) | state store, global store, cache invalidation, logout cleanup | no | Per-domain state split + explicit invalidation on session-identity change |
| pwa | [pwa/offline-and-sync.md](pwa/offline-and-sync.md) | offline draft, sync on reconnect, indexeddb | no | Explicit whitelist for offline-safe fields; conflict-aware sync |

---

## Security Concern Map (cross-cutting, security-critical files only)

Scoped only to rows marked `security-critical: yes` above. Files that are pure
correctness/reliability patterns (e.g. defer pitfalls, N+1 resolvers, offset
pagination) don't need a cross-cutting concern tag — they're fully covered by
the flat table and their own category.

| Concern | Files |
|---|---|
| authn | go/jwt-and-token-lifecycle.md, restapi/csrf-and-cookie-security.md, pwa/token-storage-and-refresh.md |
| authz | go/authorization-and-idor.md, go/role-and-privilege-separation.md |
| secrets-and-keys | go/secrets-and-key-management.md, go/secrets-and-sensitive-logging.md, go/jwt-and-token-lifecycle.md, go/webhook-signature-verification.md |
| input-validation-and-injection | go/input-validation-and-injection.md |
| pii-and-encryption | postgresql/encryption-at-rest.md, postgresql/audit-log-design.md |
| external-integration | go/webhook-signature-verification.md |
| rate-limiting-and-abuse | go/rate-limiting.md, restapi/anti-enumeration.md |
| file-handling | go/file-upload-handling.md |
| dependency-supply-chain | go/dependency-and-supply-chain.md |
| money-and-precision | postgresql/financial-invariant-enforcement.md |
| network-boundary | restapi/csrf-and-cookie-security.md, restapi/cors-configuration.md, infra/security-headers-and-tls.md |
| client-security | pwa/xss-and-content-sanitization.md, pwa/token-storage-and-refresh.md, react/server-client-component-boundary.md |
| enumeration-and-timing | restapi/anti-enumeration.md |

**Instruction for agents:** for any story touching authentication, authorization,
money/PII, external callbacks, or client-facing security surfaces, check this map
first — before falling back to scanning the full table by keyword.

---

**Coverage complete for initial pass** across go/, postgresql/, graphql/, restapi/, kafka/, pubsub/, redis/, infra/, pwa/, react/. `react/` added 2026-08-23 — new frontend-general category, sibling to `pwa/` (which stays scoped to offline/service-worker/installability): `accessibility-fundamentals.md`, `server-client-component-boundary.md`, `form-validation-boundary.md`, `data-fetching-conventions.md`, `component-test-mocking-discipline.md`. Written from general React/Next.js knowledge, not yet grounded in a real kencleng frontend story — enrich with real examples as the first frontend tasks land, same pattern as every other category here.

**Maintenance:** every new file added to any `best-practices/<category>/` folder gets
one row here — category, path, trigger keywords, security-critical (yes/no), one-line
summary. If security-critical is `yes`, also add it to the Security Concern Map under
every concern tag it applies to — a security-critical file with no map entry is
effectively invisible to the primary security-scan path. Keep summaries scannable
(one line); don't restate the file's content here.

## Governance

This file and every file it indexes — including every per-category
`examples.md` — are protected. The agent cannot edit any of them
directly, not even to append a real-world reference or fix a typo.

Proposed additions or changes go through the root-level `proposals/`
directory (see `../proposals/README.md`) for human review and manual
merge. Note this differs from `workflow/techplan/`, where
`examples.md`/`retro.md` are agent-appendable directly without a
proposal — that exception is specific to `techplan/` and does not carry
over here.

**Threshold for proposing:** looser than `techplan/proposals/` (which
needs 2+ stories or a genuinely structural gap). `best-practices/` is
knowledge content refined over time, not a contract — a single
well-evidenced gap is enough to propose.

### examples.md convention

Each category folder that has real-world reference material gets its
own `<category>/examples.md` (e.g. `go/examples.md`), holding concrete
implementation-level detail kept separate from the principle files. This
is what keeps the principle files themselves project-agnostic — a
concrete case is valuable to keep, but it belongs in `examples.md`, not
folded into the Principle/Bad/Good of the file it illustrates.

### Genericity discipline

Every file here must be usable in a project that isn't any one specific
codebase — generic to the folder's technology (e.g. `go/` implies Go,
not a specific framework within it), not to any particular project's
domain or tooling choices. If a proposed Bad/Good example leans on a
specific library, tool, or business domain that isn't essential to the
principle, that's a signal to generalize further before proposing, not
after.

See `AGENTS.md` in this folder for the short, agent-facing version of
these rules.