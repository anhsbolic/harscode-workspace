# Go Error Handling and Result Contracts

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** Go service/repository/HTTP error contracts and partial operations.
> **Triggers:** error, partial result, transaction, rollback, io.Reader, HTTP status, sentinel, error wrapping.

## 01 — Applicability

Apply when an operation can partially complete, returns `(value, error)`, crosses boundaries or exposes failure to clients. The correct handling depends on the **documented function contract**, not a universal rule that any value accompanying an error is invalid.

## 02 — Principle / Rule

- Define explicitly whether values accompanying a non-nil error are meaningful. Default to treating them as unusable **unless the API contract specifies otherwise**.
- Partial result plus error can be legitimate, e.g. `io.Reader.Read` can return bytes together with a non-nil error; preserve valid partial data when its contract requires it.
- Do not claim a failed operation succeeded because some preliminary work or response data exists. Distinguish committed, rolled back, partially completed and uncertain outcomes.
- Wrap errors with `%w` when callers need classification; use `errors.Is/As` for stable handling. Do not expose raw internal errors to external clients.
- Prefer explicit named constants for materially meaningful error codes/state labels rather than scattered magic strings.

## 03 — Rationale & Risk

Blanket discarding of every partial value breaks APIs where the data is useful; blanket use of returned values after errors invents success. Accidental error swallowing, public leakage and incorrect retry decisions can violate product-state truth.

## 04 — Application Guidance

1. Write per-boundary contracts for success, validation failure, authorization denial, conflict, retryable failure, and uncertain completion as applicable.
2. For repository and transaction functions, if atomic failure is promised, return no success payload and ensure rollback/commit outcome is correctly represented.
3. For streaming/chunk APIs, process any contractually valid bytes before handling `err` (including `io.EOF` semantics).
4. Map internal errors to safe client-facing codes; log only permitted bounded diagnostic fields.
5. Separate transient from permanent failures only where justified; retries of state-changing requests require idempotency or reconciliation as appropriate.

## 05 — Verification

Test error paths with and without partial values, committed versus rolled-back state, client-safe error responses and retry classification. For any function exposing an uncertain outcome, verify consumers do not blindly present success or duplicate effects.

## 06 — Boundaries & Trade-offs

Avoid forcing a single monolithic error taxonomy. Some APIs legitimately return partial data; other business commands must remain strictly atomic. Go language conventions do not decide project product-success semantics.

## References

- https://pkg.go.dev/io#Reader
- https://pkg.go.dev/errors
- https://pkg.go.dev/net/http#Client.Do
