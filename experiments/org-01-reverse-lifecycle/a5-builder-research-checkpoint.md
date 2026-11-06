# A5 — Engineering Builder Research Checkpoint

> **Standing:** WORKING RESEARCH CHECKPOINT / DISCUSSION CONTINUITY — **NOT A5.1 APPROVAL**, not a formed Space, not canonical Harscode policy, not runtime evidence.
> **Decision owner:** Anhar. **Recorded:** 2026-11-06.
> **Repository / branch / starting checkpoint:** `anhsbolic/harscode-workspace` / `research/cross-stage-mapping` / `35351b0015a54e2bd58c17cd91eacbec74dcc445`.
> **Scope:** Preserve the current A5 reasoning and unresolved boundaries before further Engineering Builder I/P/O/O discussion. This document does **not** revise the original experiment, settled A1–A4 research decisions, current Space definitions or target-project authorities.

## 1. Authority and source standing

- **Immutable original Builder evidence:** [`engineering-builder.md` at `947d9b361bd4cdf07d3aeebffb4a27eaf18da49a`](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/engineering-builder.md), blob `22f88376a1b9912ee54c3a6b462245a7c0f2003f`. Its status is **WORKING EXPERIMENT SNAPSHOT**, not approved generalized Harscode Builder guidance.
- **Original source-provenance hypothesis:** [`input-source-mapping.md` at the same immutable commit](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/input-source-mapping.md), blob `262e009c49a7b9ac2c6be88de0f3c5abfdbd7a84`. Its source edges are candidate mappings, not verified project-level consumer fit.
- **Research standing / exact approval provenance:** [`audit-revision-plan-and-tracker.md`](audit-revision-plan-and-tracker.md), starting-checkpoint blob `1c1d4d5c439cfdce404732820114fb33d3fd3b71`. A1–A3 are settled for research; A4 Rancang has exact **FORMATION APPROVED / RESEARCH-ONLY** standing at `5a2964703bfddc3dc06a78091ef0b7f0220a57f0`; Engineering Project Standards are separately **ACCEPTED FOR RESEARCH**; A5 and A6 have not received comparable final approval.
- **Current Engineering reference, not a substitute for the experiment:** `engineering/production-and-verification.md`, `engineering/space-formation.md`, `engineering/spaces/rancang/contracts.md`, and `engineering/spaces/nextjs-builder/contracts.md` on the research branch.
- **A5.1 initial audit / Target Model v2:** conversational working analytical proposals, **not Human-approved**, not written into authoritative Engineering definitions. Their detail is not silently promoted by this checkpoint.

## 2. Original Builder experiment — unchanged

The illustrative ORG-01 reverse-lifecycle Builder model has **10 Inputs → 8 Processes → 5 Outputs + 6 actor Outcomes**:

| Type | Exact original items |
| --- | --- |
| **Inputs (10)** | (1) Product Contract; (2) UX Flow / Interaction Specification; (3) Hi-Fi UI Design; (4) Engineering Solution Design; (5) API Contract; (6) Data Model / Database Schema; (7) Existing Codebase & Technical Standards; (8) Test & Acceptance Scenarios; (9) Design System; (10) Web Assets. |
| **Processes (8)** | (1) Input Review; (2) Implementation Planning; (3) Frontend Development; (4) Backend Development; (5) Database Implementation; (6) Integration; (7) Testing & Verification; (8) Review & Handoff. |
| **Outputs (5)** | (1) Functional Web UI; (2) Working Backend API; (3) Operational Database Structure; (4) Integrated Application; (5) Test & Verification Results. |
| **Actor Outcomes (6)** | (1) Start organization formation; (2) understand information/consequences before creation; (3) authenticate as needed and explicitly submit; (4) form organization together with a valid initial internal Owner; (5) inspect durable organization/Owner relationship; (6) receive truthful failure/uncertain-result information. |

**Original-case qualification:** Inputs 1–8 were required for that illustrative end-to-end case; Design System and Web Assets become required when accepted design/project constraints make them necessary. An input is needed **information**, not necessarily a dedicated file. The eight processes are logical activities, not eight agents, Spaces or obligatory waterfall steps. The six outcomes are case-specific actor outcomes, **not universal Engineering outcomes**.

The original **direct Product Contract input** is a fact about the broad Builder experiment. The more specialized Builder responsibility boundary below is a **proposed working refinement**, not a retroactive edit to that experiment.

## 3. Working agreements — direction, not approval of final model

### 3.1 Engineering specialization and formation posture

- Build Engineering capabilities from **real project demand**, with a scope broad enough to cover established industry practices relevant to that technology/discipline. Do not prematurely build a complete hypothetical Engineering catalog.
- **Reusable Engineering definitions must be project-agnostic**, while particular executions are bound to the target project's actual sources, constraints and permissions. Technology-specific specialization is valid; project-specific business semantics or fixed library decisions must not become reusable policy.
- Relevant, still-useful deprecated legacy practices can be assessed for adoption; legacy source is not authoritative by inertia.
- Organize around **coherent external production results and accountable responsibility**, not one Space per process, original output, skill or Agent. Combining related capabilities is justified only where it improves coherence and accountability rather than hiding important boundaries.
- Internal specialists/Agents, if eventually justified, may contribute selectively and iteratively; **no fixed linear sequence and no obligation to invoke every Agent**. Independent assurance must remain meaningfully independent when material.
- **No Space formation or Agent composition decision is made by this checkpoint.** Candidate Space language is an analytical lens only.

### 3.2 Engineering-wide reasoning standard

Apply **fit for purpose, value for resources, technical feasibility and proportionate scalability** across relevant specializations:

- Judge trade-offs using actual project stage, constraints, risk, people/tools/resources and reasonably foreseeable growth.
- Select the simplest **sufficient and robust** mechanism for real requirements; avoid speculative abstractions, infrastructure, process and premature optimization.
- Preserve correctness, security, integrity, recovery and legitimate Human/owner gates where materially required; simplicity/cost do not excuse missing safeguards.
- Feasibility reasoning is part of Engineering skill and implementation judgment, not merely a final architectural checkbox.

### 3.3 Authority boundary: Product → Rancang → specialized Builder

- **Rancang is part of Engineering**, owning **Product-to-Engineering technical translation**: turning accepted Product meaning and relevant Design/UX requirements into implementation-consumable technical obligations and handoff.
- **Specialized Builder owns implementation correctness against sufficiently authoritative, accepted/effective technical inputs**, plus relevant technical feasibility, actual project standards and technical conformance. It **does not own Product analysis, Product interpretation or Product-to-Engineering translation**.
- Do **not** make direct full-Product-Contract discovery/analysis a default task or skill prerequisite for specialized Builder. Instead, discover **which concrete Product-derived technical information Builder actually needs**, then test in later cross-stage audit whether Rancang supplies it sufficiently. This is a **working desired boundary**, not a claim current Rancang contracts or all target projects already satisfy it.
- Builder evaluates **technical input sufficiency**: missing interface detail, incoherent engineering constraints, incompatible schemas, feasibility, applicable standards, etc. Missing or conflicting Product-derived semantics return to Rancang/the legitimate input owner; Builder does not fill them by authoring Product decisions.
- If code fails an adequate effective technical contract, implementation responsibility belongs to Builder. If code faithfully implements a faulty Product-to-Engineering translation and therefore the Product outcome fails, investigate **upstream translation/contract responsibility**, rather than automatically declaring Builder at fault. Attribution must follow actual evidence; it is not a blanket immunity for incorrect implementation or ignored technical hazards.
- **Engineering Project Standards** and actual code/environment remain direct relevant Engineering sources that Builder must evaluate and apply within its scope. Their applicability and adequacy are Engineering concerns, unlike ownership of Product semantics.
- Preserve the separate authority between **proposed Engineering API/schema contracts**, **legitimately adopted effective project contracts**, **authorized implementation**, and **executed tests**. A Rancang proposal does not itself grant project-canonical adoption or code/write permission.

**Product-derived technical obligations to examine later (not yet a final I/O contract):** implementable behavior/effects, enforceable invariants, identity/authorization, data/state meaning, failure/unknown/recovery semantics, and falsifiable acceptance scenarios. Source-level coverage and consumer sufficiency remain open for verification; Builder should not independently reconstruct their Product meaning.

### 3.4 Evidence and outcomes

- Distinguish **component implemented**, **component verified**, **actual integration verified**, **Human accepted**, and **delivered actor outcome**. Each claim needs its own subject/scope/revision/evidence; delegation of a verification task is **not** a verification PASS.
- A bounded Builder assignment can finish a valid component implementation without claiming full actor outcome or overall integration. The end-to-end output/outcome chain still needs distinct accountable integration and verification.
- Mock/front-end contract simulation, provider-side tests, real FE–BE integration and actual delivered behavior are distinct evidence scopes.
- No new universal state machine, central evidence registry or mandatory document template is implied.

## 4. Candidate responsibility groupings — not formed

| Candidate specialization | Coherent scope under discussion | Original output contribution | Boundary |
| --- | --- | --- | --- |
| **NextJS Frontend Builder** | Next.js frontend implementation and frontend-side API consumption/integration when separately authorized and needed | Functional Web UI; contributes to Integrated Application and scoped verification | Does not own Product/UX design, backend implementation, or overall FE–BE–DB acceptance. The existing NextJS Builder is formation-approved for research at exact commit `323d8c4a19eb1ae497066ff47ce092ee19f0ab94`; that formation is **not** an A5 architecture constraint or proof of runtime readiness. |
| **Go Backend Builder** | Go API/domain implementation together with relational PostgreSQL persistence, when they form one accountable, coherent result | Working Backend API + applicable Operational Database Structure; contributes to Integrated Application and scoped verification | Candidate only, **not formed**. Does not decide Product meaning, silently change effective canonical contracts, implement frontend, claim overall integration, or execute protected/destructive database changes without separate authorization. |

**Grouping hypothesis:** Backend API + persistence is a promising cohesive implementation capability because transactions, authorization, business invariants, schema and failure semantics frequently interact. Not every assignment needs an API change **and** a database change; database operations/deployment authority is distinct from writing migrations.

Likewise, one frontend specialization may handle UI implementation in one assignment and actual frontend-side API integration in another. Assignment scope, readiness and authorization are not automatically expanded when a provider becomes available.

The original **Integrated Application** remains an accountable cross-component result rather than being silently assigned to the frontend producer alone. **Test & Verification Results** remain evidence obligations, including genuinely independent review where required, not proof derived solely from a producer's completion claim.

These candidates use current observed demand to choose **what to research now**, not to insert any specific project's business semantics or technical rules into reusable definitions.

## 5. Current focus and open decisions

**Current discussion position:** The next focused work is **Go Backend Builder I/P/O/O**, starting from **Output + Outcome** so that Process and Input can be derived from a specific coherent result. Stay at high-level responsibility/skill/input-output reasoning before any Space formation work.

Open, deliberately not settled here:

1. Exact **Go Backend Builder OUTPUT + OUTCOME** and sufficient completion/evidence boundary for API and persistence, including whether they genuinely belong to one cohesive result in real cases.
2. Resulting **PROCESS responsibilities/skill sets**, their technical decision latitude, and where specialized independent assessment is warranted.
3. Resulting **INPUT contract**: effective Engineering Solution, API/data contracts, actual codebase, Engineering Project Standards, verification requirements, authorization and technical feasibility; distinguish required/conditional information, not document counts.
4. **Rancang → Builder consumer sufficiency**: which Product-derived technical obligations are missing or underspecified, who has authority to resolve them, and what counts as effective versus merely proposed contracts.
5. The accountable join between frontend, backend, database, verification and end-to-end delivered outcome.
6. Later **cross-stage A6** checks of source→consumer authority/evidence, without silently changing approved upstream definitions.
7. Later **A5.2/A5.3/A5.4** responsibility decomposition, Space architecture and existing-definition reconciliation, **only after the Builder target model is sufficiently settled**.

## 6. Next step and constraints

**Next research step:** Discuss the **Go Backend Builder's specific OUTPUT + OUTCOME** against original Builder O02/O03, with clear distinction from O04 Integrated Application and O05 Test & Verification Results. Then derive relevant Process and Input; discuss one boundary at a time.

**No authority conferred:** This checkpoint is not Human approval of A5.1 Target Model, Go Backend Builder formation, modification of Rancang or NextJS Builder, actual task invocation, project repository write, runtime validation or promotion to Harscode `main`. Subsequent new evidence or decisions should be recorded in the appropriate owning artifact with their own approval standing.
