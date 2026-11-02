# API Execution Modes, Contract Consumption, and Forms

> **Applicable when:** frontend consumes backend interfaces, mutations, validation, authentication transport or backend-independent mocked development. The selected API mode comes from the Coordinator's Human-authorized assignment—not current server availability.

## Contract and API consumer

Identify the **effective** interface representation, revision/standing and normative behaviors. Prefer project-standard derived types when supported; do not create a parallel handwritten DTO that competes with canonical schema. Strong TypeScript types do not guarantee runtime payload conformance. Resolve method/path, requiredness/nullability, identifiers, headers, auth/CSRF, success, field validation, denial, system failure, timeout/unknown outcome, pagination and resource-state meanings as *applicable*.

Keep transport/result normalization at a maintainable boundary when actual complexity warrants it; do not write a generalized SDK, monolithic adapter or special error parser for a one-request feature. UI copy is an experience decision tied to approved meanings, not necessarily literal backend error text; never expose internal stack traces or sensitive detail.

## `MOCK_DEVELOPMENT` — explicit default for API-dependent work

Use accepted, sufficiently deterministic contract inputs to build network-boundary mocks when suitable and permitted. Exercise meaningful variants, not happy-path-only sample JSON: success, validation, denied, empty, transport error and ambiguous/unknown result when supported. Keep test/dev mocks visibly isolated from real production behavior and trace them to exact contract revisions. A mock does **not** prove backend operation availability, persistence, transaction consistency or live auth.

When the contract is missing a material domain/interface rule, stop that *dependent* implementation rather than manufacture endpoints or enum statuses. Work on genuinely independent authorized UI surfaces only. If backend becomes available during mock mode, do not switch modes; report readiness to Coordinator for a future Human decision.

## `REAL_API_INTEGRATION` — explicit Human assignment

Confirm exact effective API and frontend/backend revisions, reachable authorized environment, safe test data, credentials/identity arrangements, applicable SOP and operation-level compatibility. Validate actual request and response/status behavior using permitted methods. Reconcile prior mocked/proposed shape against the canonical provider contract; don't silently paper over inconsistent semantics via frontend adapters.

If the real provider is down, unavailable, fails a required operation, or materially contradicts accepted contract, perform **bounded diagnosis** to determine frontend/backend/environment/shared-authority ownership. Fix frontend-owned issues within scope. Otherwise hand off exact observed error and **stop affected integration assignment**; do not revert to mock mode, substitute test doubles as live proof or expand into backend code. An isolated test double may still be used for expressly permitted component checks, never as real-integration evidence.

## Forms, effects and recoverability

Client validation is immediate UX feedback, not authoritative business validation. If backend returns field-specific validation, preserve its intended location and safe explanation; differentiate it from request-level/auth/network errors. Do not block valid values with stale stricter client rules. Accessible labels and errors must remain associated with fields.

For consequential mutations, apply contract-defined idempotency/replay/duplicate safeguards. Do not assume all POSTs need an idempotency key, or that a retry with a new key is harmless. A lost response is **unknown**, not proof of failure; do not automatically repeat a side-effecting command without accepted recovery rules. Keep “submitted”, “accepted”, “completed”, “rejected”, “unknown” distinct as the contract requires. Don't equate hiding an action with server permission.

## Evidence boundary

Record mode, contract version, whether provider was mocked or live, observed status and outcome and applicable SOP restrictions. Static schema validation, generated types and component mocks are not live integration. Backend owner remains accountable for server implementation; overall FE–BE acceptance belongs to the named project owner, not this frontend consumer by default.
