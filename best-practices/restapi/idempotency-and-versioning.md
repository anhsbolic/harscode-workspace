# REST API Idempotency, Retry and Compatibility

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** State-changing HTTP endpoints, retries, and contract evolution.
> **Triggers:** POST, create, retry, duplicate, idempotency key, timeout, versioning, API compatibility.

## 01 — Applicability

Apply when network retries, duplicate user actions, proxy replay, concurrent submissions or API contract changes can create an observable effect. Read-only endpoints and explicitly safe methods have different obligations from create/mutate operations.

## 02 — Principle / Rule

- Identify the requested operation's **observable effect** and whether repeat submissions may execute it more than once.
- Do not assume an ordinary `POST` is idempotent. For operations where duplicates matter, design and verify an applicable deduplication, uniqueness, idempotency-key or recovery strategy.
- Treat timeout/network failure after dispatch as **outcome unknown**, not automatically failed or safe to repeat.
- If using an idempotency key, scope it to the correct principal/operation, bind it to request meaning, define retention and concurrency behavior, and replay a compatible result; do not let the same key authorize a different payload.
- Keep clients/server aligned with the actual accepted OpenAPI contract. Distinguish additive from breaking changes, and plan compatible rollout or versioning when needed.

## 03 — Rationale & Risk

Retry-after-timeout can create duplicate resources/grants, while blindly suppressing replays can strand valid requests. Contract drift can make a client interpret an incomplete/failed operation as success.

## 04 — Application Guidance

1. State whether multiple identical create requests should return one resource, a conflict, or multiple independent resources; derive this from owning requirements.
2. Choose DB uniqueness/transaction guarantees for domain invariants; layer idempotency keys if API semantics and retry behavior call for them. They solve different problems.
3. For a stored key, enforce atomic claim/result recording or equivalent concurrency-safe semantics; define response for concurrent in-flight duplicates and payload mismatch.
4. On uncertain client outcome, prefer a safe status lookup or properly scoped retry mechanism rather than a blind second create.
5. Keep method, status, error and response-body semantics synchronized with the contract, including conflict and retry conditions.

## 05 — Verification

Test same-key/same-payload replay, same-key/different-payload denial, simultaneous requests, timeout after commit, error before commit, expiry/retention rules and multiple principals **only where that mechanism is selected**. Assert actual durable effects; check OpenAPI/client response compatibility.

## 06 — Boundaries & Trade-offs

A generic best practice cannot demand idempotency keys on every endpoint. Domain uniqueness does not equal user-intent replay deduplication. Retention and request identity carry storage/privacy costs. No automatic version bump is required for every additive API change.

## References

- https://www.rfc-editor.org/rfc/rfc9110.html
- https://www.rfc-editor.org/rfc/rfc9457.html
