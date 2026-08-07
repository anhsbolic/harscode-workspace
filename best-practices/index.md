> **Location:** `best-practices/index.md`

# Best Practices Index

Scan this table first. Match `Trigger keywords` against the area being explored/planned,
then open only the matching file(s) — don't read every file in `best-practices/`.

| Category | File | Trigger keywords | Summary |
|---|---|---|---|
| go | [go/error-handling.md](go/error-handling.md) | error, return, result, wrapping, constant, literal | Result/error contract correctness (`return a, b` staleness); named constants for load-bearing literals |
| go | [go/abstraction-boundaries.md](go/abstraction-boundaries.md) | SRP, signature, extraction, pure function, side effect, mock | Function signature must not leak extra responsibility; separate pure predicate from side-effecting action; avoid single-caller abstraction layers |
| go | [go/feature-lifecycle.md](go/feature-lifecycle.md) | flag, toggle, TODO, not-yet-active, comment out | Disable an incomplete/blocked feature with a flag, not commented-out code |
| go | [go/naming-and-scope.md](go/naming-and-scope.md) | naming, variable, test scope, mock, duplicate test | Variable naming should reveal source/purpose, not just shape; test at the lowest level that exposes the behavior |
| go | [go/goroutine-lifecycle.md](go/goroutine-lifecycle.md) | goroutine, leak, concurrency, WaitGroup, errgroup, unbounded | Goroutines with no exit path leak; unbounded per-item goroutine spawning under load; use ctx-aware primary calls not outside timeouts |
| go | [go/context-propagation.md](go/context-propagation.md) | context, ctx, cancellation, deadline, Background, TODO | context.Background() mid-chain breaks cancellation propagation; don't store ctx in a struct field; long-running work must poll ctx.Done() |
| go | [go/nil-and-zero-values.md](go/nil-and-zero-values.md) | nil, nil map, nil slice, nil pointer, zero value, JSON null | Nil map write panics (read doesn't); nil vs empty slice serializes differently (null vs []); nil pointer method calls depend on receiver dereference |
| go | [go/error-wrapping.md](go/error-wrapping.md) | error wrapping, errors.Is, errors.As, %w, %v, sentinel error | Don't string-match err.Error(); %w preserves the error chain for errors.Is/As, %v silently breaks it |
| go | [go/defer-pitfalls.md](go/defer-pitfalls.md) | defer, LIFO, resource leak, file descriptor, named return | defer in a loop accumulates until function return, not per-iteration; deferred args evaluated immediately, not at execution time; LIFO cleanup order |
| go | [go/interface-and-slice-semantics.md](go/interface-and-slice-semantics.md) | interface nil, typed nil, error interface, slice aliasing, sub-slice | Typed nil pointer stored in an interface is not a nil interface; sub-slices share underlying array, mutation/append can silently affect the caller's data |
| go | [go/struct-copying-and-time.md](go/struct-copying-and-time.md) | mutex, copylocks, sync.Mutex, time.Time, monotonic clock, timezone | Copying a struct containing sync.Mutex breaks locking; time.Time == comparison fails on monotonic clock differences, use .Equal() |
| go | [go/input-validation-and-injection.md](go/input-validation-and-injection.md) | log injection, command injection, exec.Command, shell, boundary validation | Unsanitized input in log lines enables log forging, prefer structured logging; shelling out with user input risks command injection; validate at the boundary |
| go | [go/secrets-and-sensitive-logging.md](go/secrets-and-sensitive-logging.md) | secrets, PII, sensitive data, logging, redact, %+v | Logging an error verbatim can leak sensitive data it wraps; logging a struct wholesale (%+v, full marshal) leaks any sensitive field it contains |
| go | [go/http-client-and-transport.md](go/http-client-and-transport.md) | http.Client, timeout, DefaultClient, connection pool, transport reuse | http.DefaultClient and zero-value http.Client have no timeout; constructing a new client per request exhausts connections instead of reusing the pool |
| go | [go/panic-and-recover.md](go/panic-and-recover.md) | panic, recover, goroutine crash, defer recover | Panic in a spawned goroutine crashes the whole process unless that goroutine has its own recover; scattering recover across layers hides bugs instead of fixing them |
| postgresql | [postgresql/indexing-and-query-plans.md](postgresql/indexing-and-query-plans.md) | index, query plan, EXPLAIN, seq scan, LIKE, composite index, covering index | Function-wrapped predicates defeat indexes; composite index column order; SELECT * defeats covering indexes; LIKE '%x%' needs pg_trgm |
| postgresql | [postgresql/transactions-and-locking.md](postgresql/transactions-and-locking.md) | transaction, lock, deadlock, isolation, FOR UPDATE, outbox | Don't call external systems inside a DB transaction; consistent lock ordering to avoid deadlocks; Read Committed non-repeatable read pitfalls |
| graphql | [graphql/resolver-n-plus-one.md](graphql/resolver-n-plus-one.md) | N+1, dataloader, resolver, batch, per-item query | Per-item resolvers cause N+1 at list scale; dataloaders must be request-scoped, not global; batching alone doesn't fix over-fetching |
| graphql | [graphql/schema-and-error-design.md](graphql/schema-and-error-design.md) | nullable, non-null, schema, breaking change, error union, mutation error | Deliberate non-null usage vs null-propagation risk; business errors vs system errors in response shape; what counts as a breaking schema change |
| restapi | [restapi/idempotency-and-versioning.md](restapi/idempotency-and-versioning.md) | idempotent, idempotency key, retry, POST, versioning, breaking change, deprecation | Non-idempotent POST double-executes on retry; classify endpoint changes as additive vs breaking before shipping |
| restapi | [restapi/pagination-and-status-codes.md](restapi/pagination-and-status-codes.md) | pagination, offset, cursor, keyset, status code, 4xx, 5xx | Offset pagination degrades and drifts under concurrent writes, prefer cursor; status codes must reflect actual failure category |
| kafka | [kafka/consumer-and-offset-management.md](kafka/consumer-and-offset-management.md) | offset, commit, consumer group, rebalance, at-least-once, auto-commit | Commit offsets only after processing completes; at-least-once requires idempotent handlers; rebalances pause the group |
| kafka | [kafka/producer-and-partitioning.md](kafka/producer-and-partitioning.md) | acks, idempotent producer, partition key, ordering, hot partition | Default acks=1 risks message loss, use acks=all + idempotent producer; partition key choice controls both ordering and load distribution |
| pubsub | [pubsub/ack-and-ordering.md](pubsub/ack-and-ordering.md) | ack, nack, ack deadline, ordering key, redelivery | Ack only after processing completes; ack deadline shorter than handler time causes duplicates even without failures; ordering needs explicit ordering keys |
| pubsub | [pubsub/retry-and-dead-letter.md](pubsub/retry-and-dead-letter.md) | dead letter, DLQ, retry policy, backoff, poison message | No DLQ means a permanently-failing message retries forever silently; retry without backoff amplifies outages |
| redis | [redis/caching-strategy.md](redis/caching-strategy.md) | cache stampede, thundering herd, singleflight, cache invalidation, TTL jitter | Concurrent cache misses hammer the DB without stampede protection; multi-key invalidation on write is easy to leave incomplete |
| redis | [redis/key-design-and-safe-commands.md](redis/key-design-and-safe-commands.md) | KEYS, SCAN, TTL, expiry, maxmemory, cluster, CROSSSLOT, hash tag | KEYS blocks the event loop under load, use SCAN; every key needs a deliberate TTL decision; multi-key ops need hash tags in cluster mode |

---

**Coverage complete for initial pass** across go/, postgresql/, graphql/, restapi/, kafka/, pubsub/, redis/. Add rows above as new files land, or as new categories are introduced.

**Maintenance:** every new file added to any `best-practices/<category>/` folder gets one row here — category, path, trigger keywords, one-line summary. Keep summaries scannable (one line); don't restate the file's content here.