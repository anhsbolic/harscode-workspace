# A5 P3 — NextJS Frontend Builder
## Independent I/P/O/O Research Definition V3 — FE–BE Integration Refinement

> **Standing:** WORKING RESEARCH V3 REFINEMENT (2026-11-10), with Anhar-approved **P6 FE–BE responsibility and conditional Mock/Real mode direction**. Exact consolidated V3 text was prepared for persistence following that directional approval; **not independently exact-revision formation approved, not runtime verified, not operational policy**.
> **Decision owner:** Anhar.
> **Repository / branch:** `anhsbolic/harscode-workspace` / `research/cross-stage-mapping`.
> **Direct source:** [Exact previously approved V2](a5-nextjs-frontend-builder-unified-ipoo-research-definition-v2.md) at commit `d1a319bb18a1e8c324072f37ef3385abd4726911` / blob `a00a5a4e5105c2822aef5ab02ca97a1e08186f0a`. V2 remains untouched as provenance. V3 retains four Inputs, five concerns, two Outputs and the same technical Outcome.
> **V1 independent baseline:** [A5 NextJS independent I/P/O/O checkpoint](a5-nextjs-frontend-builder-independent-ipoo-research-checkpoint.md), pinned at commit `bc96a1f6ed3fbe066c37b8e2b925b3e1160b4f95` / blob `837ceb191b916516ca13ea4f0c414d8be526264b`. V1 remains unchanged as provenance.
> **Historical research input:** Existing formed NextJS Builder at exact research approval revision `323d8c4a19eb1ae497066ff47ce092ee19f0ab94` was reviewed as a *source of selected semantic insights only*, **not** as an architecture, Input/Output shape, Agent topology, or execution-mode structure to retain. The four V2 refinements were subsequently approved as working research direction by Anhar; this consolidated definition was separately approved for persistence.
> **A5 standing:** P3 remains `IN_PROGRESS` at research level; A5-wide P1–P8 coverage and A6 cross-foundation closure are not resolved by this file. Track progress only in the [single owning tracker](audit-revision-plan-and-tracker.md).

## 1. Responsibility and Technical Outcome

**NextJS Frontend Builder** is a reusable, project-agnostic, Next.js-specialized Engineering capability responsible for implementing and verifying delegated frontend software behavior.

It is **frontend-only**, not a generic Frontend Builder or full-stack application owner.

**Technical Outcome — V1 retained**

> A NextJS Frontend Builder delivers correctly implemented Next.js frontend capabilities within an authorized scope, conforming to effective project contracts and applicable functional, experience, accessibility, security, and quality requirements.
>
> Its responsibility includes frontend rendering, navigation, interactions, presentation and UI state, and applicable frontend-side data consumption or presentation-oriented server-side support.
>
> Its accountability excludes authoritative backend/domain implementation, ownership of domain persistence and business invariants, overall system integration acceptance, and end-to-end Product/actor outcomes.
>
> Technical achievement and completion claims must be qualified by actual verification evidence.

Next.js server-side capabilities may be used where their behavior legitimately belongs to delegated frontend responsibility. Runtime location does not confer domain or backend authority.

## 2. INPUT — Four Logical Information Groups

**I1 — Assignment & Delegated Authority**

Authorized objective, scope, exclusions, intended consumer, relevant permissions, protected boundaries, technical discretion, explicit limits of UI design discretion, and consequential decision owners.

Changes to materially delegated integration scope, protected operations, or external effects require applicable authorization. Tool availability and discovered code do not confer authority.

For API-dependent assignments, the selected `MOCK_DEVELOPMENT` or `REAL_API_INTEGRATION` scope and any consequential mode change must be explicitly authorized.

**I2 — Effective Frontend Requirements & Contracts**

Applicable effective Product, UX, UI, Design Standards, Engineering, interface, content, accessibility, privacy, security, and quality obligations.

Include, where material:

- Accepted user-facing states and authoritative result meaning.
- Interface behavior for success, failure, denial, partial and uncertain outcomes.
- Data freshness, authentication/session, authorization, and identity-scoping obligations.
- Sufficient accepted visual/interaction direction, or legitimate accepted equivalents.
- Verification and receiving-consumer requirements.
- For API-dependent work, the effective API contract and adoption/approval standing, relevant provider/consumer versions, error/identity/result semantics and permitted API integration mode.

Material decisions must be traceable to effective authority. Missing Hi-Fi does not authorize material UI invention.

**I3 — Current Next.js Technical Baseline**

Actual repository, branch/revision, implementation architecture, relevant Next.js/React versions, existing rendering/routing/state/data patterns, dependencies, codebase conventions and technical constraints.

Existing code is implementation evidence, not automatic Product or Design authority.

**I4 — Execution & Verification Context**

Actual project-side environments, relevant backend/provider availability, integration dependencies, available/permitted tools, testing policies, test data, execution constraints and verification limitations.

Distinguish simulated, real-provider, source-level and rendered evidence capabilities. Availability does not mean authorization.

For real API integration, inspect actual backend revision, adopted interface, endpoint availability, test identities/data and permitted side effects. Mock tools alone are not real-provider readiness.

These four Inputs are semantic information groups, not four mandatory files or upstream producers.

## 3. PROCESS — Five Logical Engineering Concerns

**C1 — Frontend Technical & Responsibility Assessment**

Establish source authority, delegated scope, design sufficiency, frontend/backend ownership, contractual completeness, technical baseline and actual execution feasibility.

Identify consequential gaps and the specific dependent work they affect. Separate ordinary technical uncertainty from missing legitimate decisions.

**C2 — Implementation Approach & Planning**

Choose a fit-for-purpose Next.js implementation approach: rendering, components, routes, state ownership, frontend data flow, integration boundaries, security, compatibility and proportionate verification.

Avoid unnecessary abstraction, speculative infrastructure and unsupported UI decisions.

Planning depth follows risk and complexity; no mandatory planning document.

**C3 — Frontend Implementation & Applicable Integration**

Implement delegated frontend capabilities, including applicable UI behavior, responsive/accessibility requirements, frontend state, data consumption, and authorized presentation-oriented server-side support.

Preserve authoritative state and interface semantics.

In particular:

- Do not treat optimistic presentation as confirmed backend success.
- Do not treat timeout or lost response as proof of transaction failure.
- Handle freshness, identity changes, and sensitive data according to effective contracts.
- Do not create competing frontend authority for backend-owned business state.
- Do not silently change integration scope or substitute simulated behavior for assigned real-provider integration.

**P6 FE–BE integration ownership:** For an authorized Next.js assignment requiring real API consumption, NextJS Frontend Builder owns **frontend-side FE–BE integration**, compatibility diagnosis and actual consumer behavior checks. The backend owner retains server/API/persistence implementation and backend dependency integration. Backend nonconformance returns to its backend owner; consequential proposed shared-contract changes return to legitimate contract authority before adoption. NextJS does not thereby own backend code, independent Engineering E2E testing, overall Product verification or Human acceptance.

**C4 — Frontend Technical Verification**

Perform applicable, authorized and risk-proportionate technical checks.

Assess actual implementation against effective functional, visual, interaction, accessibility, contract, security and quality obligations.

Distinguish:

- Source/build correctness from observed runtime behavior.
- Simulated-provider evidence from real-provider integration.
- Actual rendered inspection from static code review.
- Frontend-owned verification from independent/system-level acceptance.
- Scoped consumer-to-real-backend checks from optional, separately authorized Engineering E2E integration testing.

Testing methods follow effective project policy and permissions. Never claim unperformed verification.

**C5 — Technical Review, Disposition & Handoff**

Reconcile actual implementation, verification evidence, unresolved issues, residual risks and known intended consumer obligations.

Determine:

- What has actually been implemented?
- What has been verified?
- Which requirements or claims remain incomplete or blocked?
- Is the output sufficient for the **actual receiving consumer and delegated scope**?
- What remains owned by external integration, QA, Design, Product or Human authorities?

Provide reconstructable handoff using actual source/output revisions and available evidence.

Builder-scoped completion is not automatically overall application acceptance.

For API-dependent work, report authorized mode, actual provider/consumer revisions, mock-versus-real evidence, contract/backend blockers and any separately applicable E2E Engineering testing obligation.

These are engineering concerns, not five mandatory execution stages or five Agents.

## 4. OUTPUT — Two Logical Categories

**O1 — Implemented Next.js Frontend Capability**

Actual, identifiable implementation revision delivering delegated frontend software capabilities.

O1 includes applicable implementation correctness across:

- Frontend rendering, routes, components and interactions.
- Responsive, accessible and intentional user-facing experience.
- UI copy, visual fidelity and authorized asset usage.
- Presentation, state ownership, freshness and identity-safe data handling.
- Effective interface, authorization/result/error/uncertainty semantics.
- Frontend-owned API consumption and conditional server-side support, including authorized real FE–BE consumer integration.
- Applicable security, compatibility and quality obligations.

Contract conformance, state correctness, intentional craft and legitimate UI design adherence are **properties of O1**, not independent mandatory software outputs.

**O2 — Verification Evidence & Technical Handoff**

Evidence and reconstructable information sufficient to understand actual implementation standing.

O2 identifies:

- Authorized scope and effective source revisions.
- Actual implementation revision or recoverable state.
- Checks performed, methods, environments, observations and limitations.
- Simulated-versus-real integration standing and selected authorized API mode where applicable.
- Relevant visual, behavioral, accessibility, security and contract evidence.
- Unresolved issues, blockers, residual risks and deferred obligations.
- Consumer compatibility and consequential dependencies.
- Scoped completion standing, without conflating it with independent or end-to-end acceptance.

No fixed document format, test framework or file-per-output is universally required.

## 5. Cross-Cutting Safeguards

**Design Sufficiency & Delegated UI Discretion**

Missing Hi-Fi is not design authority.

For material UI decisions, sufficient accepted visual/experience direction or legitimate delegation must exist.

Builder may exercise ordinary implementation judgment within that boundary. Unresolved material decisions return to their owning Product, UX, UI or Project Standards authority.

Authorized visual exploration remains `PROPOSED` until legitimately accepted. A polished interface cannot substitute for design approval.

**Frontend State & Contract Truthfulness**

Frontend must preserve the distinction between requested, pending, confirmed, rejected, uncertain and stale effects where relevant.

State presentation must not invent backend guarantees, business invariants or permissions.

Private/user-specific state must respect legitimate identity and lifecycle boundaries.

**Integration Integrity — Scoped API Execution Modes**

Two distinct modes are available for API-dependent assignments, selected according to actual purpose and authorization:

- **`MOCK_DEVELOPMENT`:** Frontend implementation and consumer checks against sufficiently specified effective API contract semantics, using contract-faithful mocks. This supports parallel FE and BE development without live provider availability. Report performed `MOCK-VERIFIED` scope only, never real API integration.
- **`REAL_API_INTEGRATION`:** Frontend consumption and reconciliation against the actual available, authorized backend, using the effective adopted/accepted API interface and inspected provider revision, environment and test data. Report observed real API integration only within executed scope. Backend defects go to the provider owner and contract changes to legitimate authority.

**Neither mode is universally mandatory.** Mock-first is an option, not a required phase; an assignment may directly authorize real integration. Provider readiness does not grant an automatic mode switch. A blocked real integration must remain blocked/partial for its affected scope and cannot silently fall back to mock or relabel mock evidence.

The modes are **authorization/verification boundaries**, not new mandatory Agents, universal state machine or forced two-stage workflow. Conditional Engineering E2E integration testing by a separate authorized responsibility remains distinct from frontend consumer-side verification and from Product verification.

**Intentional Experience Craft**

Frontend experience quality must be purposeful, accessible, understandable and appropriate to actual accepted Product/UX/UI meaning.

Avoid unjustified filler, misleading copy, arbitrary decorative decisions, unsupported trust indicators and unapproved assets.

Craft quality does not confer Product, UX, brand or UI design authority.

**Consumer-Fit & Scoped Completion**

Completion is evaluated against applicable delegated Builder obligations and the real intended consumer, not arbitrary universal checklists.

Implementation may be complete within a bounded frontend assignment while separately owned system integration, independent QA or Product acceptance remains pending.

Do not expand delegated responsibility merely to make the entire application appear complete.

**Evidence and Authority**

Actual evidence, exact revisions, permissions and legitimate decision owners bound every meaningful claim.

Blocked or unverified work is reported truthfully; safe independent authorized work may continue where appropriate.

## 6. Conceptual Sufficiency

The V3 model accommodates:

- UI-only changes without inventing API dependencies.
- Frontend API consumer changes with sufficient contract meaning.
- Conditional presentation-oriented server-side responsibilities.
- New/material UI with accepted design coverage.
- Small UI changes using sufficient accepted design equivalents.
- Missing consequential UI authority with dependent work held.
- Mock-based development without false real-integration claims.
- Real-provider integration without silent fallback.
- Parallel frontend mock development and backend implementation against effective interface semantics when authorized.
- Direct authorized real API integration without a required preceding mock assignment.
- Scoped implementation completion with separate receiving-consumer obligations.

These are conceptual coverage tests, not execution evidence.

## 7. Explicit Non-Goals

This definition does not prescribe:

- Existing historical NextJS Builder Agent topology.
- Any required number of Agents or independent runtime contexts.
- A mandatory mock-first sequence, automatic mode switch or universal workflow state machine.
- Mandatory sequential stages, approval per Process or fixed artifact chain.
- A universal frontend testing framework or coverage threshold.
- Automatic full-stack ownership.
- Overall FE–BE integration acceptance.
- A new UI Design responsibility inside Engineering.
- Harscode operational promotion or runtime readiness.

Agent composition, actual execution mechanisms and runtime validation remain separate later decisions.

## 8. Research Standing

**V3 refinement intent:** preserve all V2 responsibility semantics and safeguards while making NextJS P6 FE–BE consumer integration explicit and introducing scoped Mock/Real API assignment modes without a mandatory sequence.

The independently derived `4 Input / 5 Process / 2 Output / 1 Outcome` structure is retained because no additional logical category has demonstrated sufficient independent accountability.

The historical NextJS Builder is a bounded research reference, not an architecture to inherit or preserve.

**Current status:** Anhar approved the P6 ownership and Mock/Real API execution-mode refinement *direction* and authorized V3 persistence. This consolidated V3 text is a working research artifact **pending independent exact-revision Human definition/formation review**; no formation, production invocation, or runtime readiness is implied.

A5 P3 remains research in progress. Runtime verification has not been performed.
