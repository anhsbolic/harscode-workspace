# NextJS Builder — External Input / Output Contract

> **Standing:** Research formation candidate, NOT FORMATION APPROVED. Owned by reusable `nextjs-builder` capability; target-project authoritative sources and explicit invocation bind actual values. [Entrypoint](README.md).

## 1. One logical Input Contract — not five required files

| ID | Class | Required meaning and authority | Acquisition / sufficiency |
| --- | --- | --- | --- |
| **I1** | **Bounded Implementation Objective** | Project/work identity, authorized target behavior, defect or outcome, relevant scope/exclusions, observable acceptance, intended consumer and effective revision/standing. Owned by Human / target project. | Human identifier plus scoped original-source discovery. A Product Outcome, PRD, Rancang handoff or fixed format is **not universal**. A terse identifier permits discovery, not unbounded code changes. |
| **I2** | **Effective Project Authority / SOP** | Applicable current Product, Design/UX, visual/brand/asset/content, Engineering, security/privacy, verification/manual-QA and protected-path standards; explicit prohibitions and owners. | Read target-project originals and effective revisions. Missing formal docs is not invalidity when delegated ordinary choices suffice; unresolved consequential meaning returns to its owner. |
| **I3** | **Implementation-Consumable Contracts** | Applicable technical/interface/experience obligations, state ownership, authorization/result/error/unknown/retry semantics, proposed vs canonical standing, consumer requirements, verification obligations and integration dependencies. | **Conditional by actual need**; accepted Rancang, canonical API, authorized design or other sufficient authoritative sources may supply them. No mandatory Rancang/OpenAPI. When material contract meaning is absent, hold only dependent production rather than invent APIs. |
| **I4** | **Current Technical Baseline** | Target repository/branch/exact revision and actual changes, Next.js/React/runtime versions, code/config, relevant integrations, tooling/environment/readiness and access limits. | Inspect live source and available environment; repository facts do not become Product/Design authority. In real-API mode, resolve actual provider implementation/runtime and permitted test environment. |
| **I5** | **Human Execution Authorization** | Exact bounded assignment, selected API execution mode, allowed actions/tools/writes, protected paths, external side effects, SOP exceptions, result/state destinations, intended consumers, supervision and consequential gates. | Human-direct authorization. Read-only discovery is not write/test/service authorization; available tool access is not permission. |

**Input decision:** locate effective sources, judge actual work sufficiency, separate delegated Engineering unknowns from missing Product/Design/API decisions, and identify independently executable authorized edges. Use `READY`, `CONDITIONAL`, `INSUFFICIENT` or `BLOCKED` descriptively; no mandatory process state machine. If authority/source revision changes, recheck only affected obligations and approval edges.

**Project precedence:** effective target-project standards and SOP govern testing, visual style, frameworks, asset usage and mechanism selection. Space knowledge is non-binding. No formal testing SOP means choose proportionate permitted evidence; a project SOP explicitly assigning manual-only verification means **do not create or run forbidden automation**. For material high-risk cases, propose a bounded exception to authorized Human/project owner *before* any prohibited action. If denied, honor SOP, expose residual risk and keep unverifiable assurance claims separate. No project SOP overrides higher-priority legal/security safeguards or permissions; escalate actual material conflicts instead of disobeying silently.

## 2. Explicit API execution mode — bound to each assignment

| Concern | `MOCK_DEVELOPMENT` (default when API-dependent) | `REAL_API_INTEGRATION` (Human explicitly selected) |
| --- | --- | --- |
| Purpose | Build frontend independently of live backend while preserving contract behavior. | Integrate frontend with an actual available backend and verify the scoped consumer boundary. |
| Input | Accepted/effective sufficient interface semantics for scope, source and standing; authorized mock use. | Effective canonical/accepted applicable real interface; backend revision, live endpoint/runtime, auth/test-data and environment permissions, known limits. |
| Action | Use contract-faithful network-boundary mocks where suitable; real provider not required. Avoid inventing endpoints or rival editable DTOs. | Perform consumer/provider compatibility check and connect actual frontend client; scoped diagnosis of real failures. |
| Backend status changes | **No automatic switch**, even if provider declares ready. | **No automatic fallback** to mock if provider is down, nonconformant or unavailable. |
| Failure | Hold only contract-dependent work; independent UI work may proceed when authorized. | If backend/environment/contract issue materially blocks actual integration, stop affected **real-integration assignment**, report exact evidence/owner/next condition; do not re-label mock exercise as success or casually switch to other scope. |
| Completion | Mock-based frontend implementation may COMPLETE within that authorized scope; real integration remains NOT VERIFIED. | Only claim observed real integration within actual contract, environment, permitted verification and evidence scope. |
| Test doubles | Normal permitted contract-faithful development/test machinery. | Permitted isolated tests can still use doubles, but these are **not** evidence of real integration nor a change of execution mode. |

**Mode selection:** API-independent work = `NOT APPLICABLE`. For API-dependent work without explicit Human mode, Coordinator uses `MOCK_DEVELOPMENT` and records it. Explicit instruction to integrate with real API selects `REAL_API_INTEGRATION`. A provider's readiness notification alone **does not grant mode switch**; mode changes need new Human invocation or exact authorized scope amendment. Project SOP may prohibit mocks or require another mechanism: resolve the conflict, do not pretend default overrides project authority.

**Mock fidelity:** mocks mirror actual accepted behavior including meaningful errors, denied/unknown paths and versioned response shapes. Mocks are not the product's authority and must not be hidden behind a production feature flag as if they were a live backend. If a required technical contract is missing, produce only authorized implementation that genuinely needs no invented semantics. When real integration is later authorized, compare mocked/proposed against effective canonical interface; migrate type generation and consumption as needed, without rival authoritative schemas.

**Real readiness:** distinguish provider-declared readiness from actual consumer-verified readiness. Verify the exact backend and interface revisions, compatible operation/status/auth/schema/semantics, reachable environment, safely available test identities/data, SOP-permitted execution, allowed side effects and known provider limits. Missing evidence blocks only affected integration. Frontend owner fixes frontend deviations; backend owner owns provider deviations; shared/canonical contract conflicts return to owning authority. No unauthorized backend implementation or invisible compatibility patch that changes authoritative meaning.

**Integration ownership:** Next.js Engineer owns *frontend-side* real API consumption and repair within scope; actual backend owner owns backend implementation and conformance; a **named project integration/acceptance owner** owns the overall FE–BE or outcome-level acceptance. Coordinator records owners and consumer claims. No mandatory separate Integration Space or automatic downstream dispatch.

## 3. One external Output — implementation, not documentation

**External result:** **Revisioned Next.js Frontend Implementation** with discoverable source and a truthful consumer handoff. The following are logical coverage, **not separate file counts, Agent stages or duplicate implementations**.

| ID | Logical output | Accountable owner | Acceptance |
| --- | --- | --- | --- |
| **O1** | **Working Next.js Implementation** | Next.js Engineer | Actual authorized source changes covering applicable routes, interactions, state displays, layout, responsive/accessibility, content, branding and visual/asset craft, and correct framework mechanics; exact revision/snapshot identifiable. |
| **O2** | **Contract & State Conformance** | Next.js Engineer | Applicable interface/state/auth/result/unknown/freshness/retry meaning is implemented correctly. This is **a property of O1 code**, not duplicate API-client files. Identify mock vs real provider; genuinely API-independent work need not manufacture an API output. |
| **O3** | **Verification & Quality Evidence / Disposition** | One accountable producer for each assigned check; Independent Reviewer owns independent findings; Coordinator joins | Project-SOP-conformant performed evidence, method/environment/scope/revision/results, permitted manual-QA ownership, relevant NOT RUN/NOT VERIFIED/PROHIBITED/deferred checks, material defect disposition and residual risks. No universal Vitest, Playwright, percentage, screenshot suite or automatic test machinery. |
| **O4** | **Revisioned Consumer Handoff** | Space Coordinator | Exact assignment/mode, source and output revisions, valid authority/permission, O1/O2 coverage, O3 findings, actual provider integration standing, known intended consumer compatibility, completion limits and next authorized action, navigable without chat recall. |

**Craft quality on O1:** intentional composition and information hierarchy, responsive behavior under realistic content, meaningful loading/empty/error/uncertain states, accessibility, appropriate typography/iconography/assets/logo, truthful copy and absence of unjustified filler. The Experience & Craft Specialist challenges and reports; the Engineer remains accountable for implementation. Missing image tools lead to approved reuse, purposeful no-image design, or actionable asset brief/candidate with clear dependency; do not fake brand approval, identity evidence or asset licensing. Do not block harmless independent UI work on a nonessential asset.

**Security on O1/O2/O3:** Engineer and Reviewer use applicable project security rules on Server/Client boundary, secrets, private cache, XSS/content, session/CSRF, resource grants, PII exposure (including markup/URL/telemetry) and consequential mutations. Browser controls are not backend authorization. For beyond-competence/high-risk findings, ask Human for specialized assessment; no implicit fifth Agent or blanket security certification.

## 4. Verification: policy, method and truth are different concerns

1. **Policy first:** discover who owns tests/manual QA, what is required/forbidden, what may run and whose acceptance is binding. Neither absence of a testing rule nor a strict manual-only SOP becomes an excuse to invent a new project policy.
2. **Method is scoped:** relevant check may be source review, static/build, behavioral automated test, actual rendered/browser inspection, manual Human QA or authorized independent review. Do not infer that available Playwright/Vitest implies authorization, or that material rendered quality was proven by lint/build/jsdom.
3. **Exception is explicit:** when a material high-risk behavior seems inadequately verified under the effective SOP, give the Human/owning authority concrete failure mode, smallest recommended additional method, cost/side effects, alternative, and residual risk. Do not execute a forbidden test before scoped exception approval.
4. **Report exact claims:** `IMPLEMENTED`, `MOCK-VERIFIED`, `REAL-API-INTEGRATED`, `RENDER-VERIFIED`, `SECURITY-ASSESSED`, `MANUAL-QA-PASSED`, `HUMAN-ACCEPTED` and `DELIVERED` are **distinct evidence-scoped descriptions**, not automatic status transitions. Never invent a PASS for methods performed by other owners. Manual-QA-owned work may remain pending after an authorized Builder implementation handoff.
5. **Independent findings:** for material risk/accepted assurance requirements, Reviewer must inspect originals, exact implementation and performed evidence through actually independent context. An Agent name is not independence; unproven isolation is marked `INDEPENDENCE UNVERIFIED`. Findings return to the Engineer for correction and targeted re-review.

## 5. Consumer joins and exact revisions

For each *known intended* consumer:
- **Generic check:** if that consumer has an applicable formed reusable Input Contract, verify type, semantics, completeness, standing and exact reviewed revisions. Otherwise `NOT APPLICABLE` with reason; unknown future Spaces are `NOT CHECKED`, not fictitiously certified.
- **Project-bound check (always):** can the actual output revision meet this consumer's current project scope, source authority, security/SOP and acceptance requirements? State actual evidence or `CONDITIONAL` / `BLOCKED` / `UNVERIFIED`.
- Keep a discoverable pointer from the existing project-owned work/assignment identity to effective code, evidence and exact handoff; no global registry or mandatory file names. An uncommitted worktree is not a durable Git revision: capture actual recoverable snapshot/patch if authorized, or report non-reconstructability rather than claiming durable implementation.
- Human approval of a proposed upstream design, Builder implementation completion, manual/independent QA, real FE–BE integration, final project acceptance, canonical API adoption and release are **separate boundaries**.

## 6. Completion and stopping rules

**COMPLETE (scoped Builder assignment)** requires all applicable *Builder-owned* implementation and SOP-permitted verification/disposition and handoff obligations for its **selected mode** to be fulfilled, with no unresolved blocker defeating that scoped claim. A correct documented transfer to separately owned manual QA can be COMPLETE for the Builder implementation scope but **not** `TESTED` or `QA ACCEPTED`; if Human explicitly includes QA acceptance inside Builder's assignment, it remains incomplete until received.

- **PARTIAL:** meaningful source/evidence exists, but an applicable Builder-owned obligation remains incomplete.
- **BLOCKED:** unresolved authority, protected permission, material contract/API/runtime dependency or prohibited needed action defeats the affected work; in `REAL_API_INTEGRATION`, stop the affected integration assignment, no mock fallback.
- **FAILED:** attempted production did not successfully yield required result.
- **UNVERIFIED:** evidence limit/claim qualifier, not an escape hatch to call a mandatory unperformed obligation complete.

Use one truthful status per relevant claim plus actionable blocked edge; do not build a universal state machine. New input or code revisions invalidate only affected checks/findings/approvals. Do not reopen accepted Product/Design/API decisions for taste. Human accepts the exact material implementation/handoff revision separately; acceptance is not automatically release.

## 7. Strict exclusions

No unapproved protected changes; no backend code, migrations or canonical shared interface writes absent separately authorized ownership; no Product/Design policy invention or automatic new project standards; no auto API mode switches; no automatic mock fallback from real mode; no secretly launched external systems/tests; no fabricated rendered, security or integration evidence; no general project orchestration, scheduler or default deployment responsibility. A scoped assignment may separately authorize a specific additional action without expanding the reusable Space's authority.
