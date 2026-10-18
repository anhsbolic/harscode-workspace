# Station 5 C1 — Best Practices Revision Tracker

> **Status:** Research-branch revisions prepared for bounded Station 5 C1 knowledge evaluation; **not** operational Harscode policy, completed technical runtime validation, or approval for Space formation/invocation.
> **Date:** 2026-10-18 (Asia/Jakarta)
> **Owning branch:** `research/harscode-purpose-llm-fit`, based on `f05c22d7f4959321ccf1505756592d9c17f2a8ed`.
> **Explicit Human authorization:** Anhar requested the needed C1 Best Practices revisions and this tracker on the research branch only. Existing `main` proposal-gated update authority is **not** bypassed or modified.
> **Kencleng pilot:** `pilot/station5-c1-space-only`; its already-approved product inputs remain the owning C1 authority. No Kencleng writes are part of this knowledge change.

## 1. Goal and constraints

Provide **targeted, portable, risk-appropriate technical guidance** likely useful over the *full C1 engineering horizon*, without presupposing historical C1 solution architecture or declaring all 75 Best Practices in need of rewrite. The initial formation/invocation still selects only the documents triggered by its actual outcome, assignment and technical choices.

C1 requires attributable initial Owner relationship, truthful internal-vs-external authority, coherent success of Organization + Owner, inspectable durable state, accurate incomplete/conflict behavior, and separate upstream product truth. These are **Kencleng-owned scoped product semantics**; the reusable guidance below does not define product rules or authorize a new identity provider, token scheme, database design, API operation or UI flow.

Research quality format: Best Practice Authoring Standard v1 (identity, applicability, rule, rationale/risk, application, verification, boundaries/trade-offs). **Research branch content** is not a silent promotion to `main`. A previous Station 3 assessment approved research drafts (16 P1 + 5 P2 plus three pilots); their exact full text was not available as canonical Git file replacements. These revisions are new *research-branch iterations based on current `main` and targeted technical verification*, not a claim that old in-chat drafts were copied verbatim or fully validated.

## 2. Revised now — ten primary guidance files

All paths below are under `best-practices/`. **Disposition = REVISED — RESEARCH CANDIDATE**; existing index paths still route to these files without index modification.

| File | C1 trigger and targeted correction |
| --- | --- |
| `go/authorization-and-idor.md` | Role **plus resource relationship**, internal-vs-external authority distinction, wrong-resource checks; avoid inventing role taxonomy |
| `postgresql/transactions-and-locking.md` | Multi-write observable invariant, isolation/locking/race choice, retry/error and external-effect boundary |
| `postgresql/migrations-safety.md` | Correct false universal claim about `ADD COLUMN ... NOT NULL DEFAULT <constant>`; contextualize locks/backfills/rollout |
| `go/integration-testing-setup.md` | Replace misplaced historical `go/examples.md` with portable real-dependency integration guidance, command/evidence and build-tag caveat |
| `go/testing-concurrency.md` | Replace misplaced historical `go/examples.md`; distinguish Go data races from DB logical concurrency and test overlap |
| `go/secrets-and-sensitive-logging.md` | Explicit safe-field logging; avoid using `MarshalJSON` redaction that changes API/persistence serialization |
| `go/error-handling.md` | Fix overbroad result-plus-error prohibition; distinguish contractually valid partial result from business-command success |
| `restapi/idempotency-and-versioning.md` | Duplicate submission, uncertain commit, keys bound to request/principal, compatibility; no universal idempotency-key mandate |
| `react/state-ownership-and-derivation.md` | Derived state, server-authoritative success, independent form state and reload/uncertainty handling |
| `react/api-client-centralization.md` | Remove assumed Kencleng-specific bearer+cookie+CSRF configuration; demand contract-bound auth, real refresh retry and mutation replay safety |

Scope is **10 targeted documents**, not a wholesale replacement of all remaining 54 Station 3 rewrite candidates. Each source retains its concern route and includes applicability, verification and external technical references.

## 3. Reviewed or conditionally relevant — not rewritten by default

| Guidance | Disposition / reason |
| --- | --- |
| `go/role-and-privilege-separation.md` | RETAIN; applicable only when project authority actually establishes incompatible roles, delegation or recusal. Do not invent Owner/Staff exclusivity from a generic example |
| `go/input-validation-and-injection.md` | RETAIN; relevant to boundary validation, no specific material correction established in this assessment |
| `react/form-validation-boundary.md` | RETAIN; client validation is UX, backend controls accepted validity |
| `react/server-client-component-boundary.md` | RETAIN; server/client trust boundary relevant when RSC path used |
| `react/accessibility-fundamentals.md` and `react/visual-verification.md` | RETAIN; applicable to a material UI, no broad rewrite shown necessary before first Space |
| `restapi/openapi-spec-first-drift.md` | RETAIN; relevant once a contract is produced |
| `go/jwt-and-token-lifecycle.md` | CONDITIONAL / **RECHECK** if JWT/refresh token mechanism selected; avoid treating universal refresh-rotation text as preselected product architecture |
| `restapi/csrf-and-cookie-security.md` | CONDITIONAL / **RECHECK** if cookie-based authenticated mutations selected; evaluate current OWASP defenses |
| `restapi/anti-enumeration.md` | CONDITIONAL; when an endpoint leaks account/resource existence and policy calls for non-disclosure |
| `postgresql/encryption-at-rest.md` and `postgresql/audit-log-design.md` | CONDITIONAL; based on actual PII classification and logging/audit obligations; no preselected encryption/search/audit schema |
| `react/app-router-routing-conventions.md` | CONDITIONAL / DRAFT in `main`; revisit if novel App Router route structure is needed |
| `postgresql/indexing-and-query-plans.md` | CONDITIONAL; query pattern and scale must justify index tuning |
| `go/goqu-query-builder.md` | UNINDEXED DRAFT; do not treat as stable authoritative guidance merely because project stack may use goqu |

Do not present these **retained** or **conditional** files as completed rewrites. If actual Space design/execution exposes a material defect, revise narrowly through applicable branch ownership.

## 4. Verification evidence and epistemic limits

- Repository-verified starting point: operational `main@c762a27aee622c247c2a408d932e762076e3588c`; research `f05c22d7f4959321ccf1505756592d9c17f2a8ed`. At this point, `best-practices/` trees were identical between branches. Current research branch adds revisions; **`main` is intentionally untouched**.
- Read current source guidance and C1 Stage 6 accepted requirements; checked published PostgreSQL, Go, React, HTTP and OWASP references. Technical references appear within revised files. This is **source-based review, not independent runtime reproduction** of every example.
- Intentional docs-only revision. No Go code compiled, PostgreSQL migration run, HTTP/client integration exercised, browser scenario verified or security red-team suite run. Do not report technical test PASS.
- No verification that new guidance improves Agent performance, prevents actual C1 defects, or amortizes Space formation investment. These belong to Station 5 real piloting.
- Known caveat: old in-chat research rewrite bodies are not reliably stored as full replacement artifacts in repository. This is a new research candidate revision set, not proof of byte-for-byte continuity with those approvals.

## 5. Space knowledge binding and next gate

**Before Space formation:** determine first *coherent bounded production outcome* and capability; do not form one Space per historical workflow stage or per Best Practices document.

**At formation/readiness:** route only the guidance applicable to actual assignment, project authority and threat surface. Bind it explicitly as **Station 5 experimental guidance** from this pinned research revision, not `main` policy. For security-sensitive operations, verify critical assumptions against live project/code/official sources and preserve Human approval/independent assurance requirements.

**Before invocation:** review input/output contract, historical-engineering-exclusion boundary, allowed tools, protected write permissions, minimal Space working state and test evidence expectations. Separately authorize execution. This tracker is **not** a Space/Agent assignment, Techplan, runtime claim, or Space ready-to-run certificate.

## 6. Follow-up conditions

Reopen only for material evidence: incorrect guidance, demonstrably missing C1-triggered safety requirement, new technical choice (e.g. token/cookie model), actual validation failure, or source/authority conflict. Do not reflexively rewrite every other Best Practice, create a new audit framework, or promote research policy to `main` as part of Station 5.

**Owning research authority:** `research/checkpoints/station4-closeout-space-only-2026-10-18.md`.
**Owning C1 pilot entry:** Kencleng `docs/project/station5-c1-space-only-pilot-entry.md` on `pilot/station5-c1-space-only`.
