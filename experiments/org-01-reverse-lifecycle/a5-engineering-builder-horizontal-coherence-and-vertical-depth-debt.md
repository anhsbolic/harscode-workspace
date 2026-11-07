# A5 — Engineering Builder Horizontal Coherence & Deferred Go Backend Vertical Depth

> **Standing:** WORKING RESEARCH DIRECTION / SCOPE DECISION, approved by Anhar in the project discussion on 2026-11-07. **Not** the result of an A5 horizontal audit, A6 final foundation closure, formation approval, operational policy, runtime validation, or authorization to modify an external project.
> **Owning status tracker:** [Cross-Stage Research Standing & Historical Provenance](audit-revision-plan-and-tracker.md). **This document is a scope/closure-criteria reference, not a second tracker or approval ledger.**
> **Repository/branch:** `anhsbolic/harscode-workspace` / `research/cross-stage-mapping`.
> **Decision checkpoint:** follows the [Unified Go Backend Builder I/P/O/O research definition](a5-go-backend-builder-unified-ipoo-research-definition.md) at `9f70f195177e862e3744243454d4ae88c1c844e8` and its [derivation-method record](a5-go-backend-builder-ipoo-derivation-method.md) at `ef5dbf0400775a7b5cb6163a153ef9e6fc716c7b`.

## 1. Decision and rationale

**Decision:** Continue with **horizontal Engineering I/P/O/O coherence** before going deeper into **Go Backend Builder Space/Agent design**.

**Reasoning:** One specialized Go Backend Builder has a sufficiently coherent conceptual I/P/O/O contract. Its **technical implementation depth** is intentionally unfinished; deepening its Agent composition, skillsets and runtime machinery now risks optimizing one Space before the broader Engineering **upstream/downstream responsibility and integration boundaries** are understood. On the other hand, enumerating many future Spaces without examining responsibility edges would produce breadth without coherent outcomes.

**Chosen sequencing principle:** **Horizontal semantic coherence first, then justified vertical specialization depth and explicitly authorized execution evidence.** This is a research ordering decision, **not** a mandatory implementation workflow, waterfall, or rule that all Engineering work must pass through a single chain.

The **vertical depth is deferred, not cancelled**. It remains an explicit follow-up obligation in the **same cross-stage research tracker**, with bounded closure criteria in section 5. Do not silently mark it resolved when horizontal coherence is accepted.

## 1.1 Audit-level correction: A5 is the Engineering Builder umbrella

This selected horizontal work is **within A5 — Engineering / Builder**, not a replacement label for A6. The original frozen [cross-stage audit worklist](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md) distinguishes:

- **A5 — Engineering / Builder:** assess the existing NextJS/frontend implementation specialization, proposed Go/backend implementation specialization, missing backend/integration ownership, verification and handoffs needed for end-to-end Engineering results. Go Backend Builder I/P/O/O is **one A5 sub-research**, not the complete A5 audit.
- **A6 — Cross-stage coherence & foundation closure:** subsequently reconcile **all A1–A5** inputs/outputs and source authority, broader domain routing, Harness/Collaboration boundaries, evidence standing and foundation closure. **A6 is still pending**; a horizontal A5 audit supplies inputs to it, not its entire scope.

The decision to discuss horizontal responsibilities **before Go-specific Agent/skillset depth** is a sequencing preference inside the current Engineering research, **not** proof that all A5 scope is finished or that A6 has started.

**2026-11-07 clarification after source revisit:** The [single owning tracker](audit-revision-plan-and-tracker.md#a5-original-p1p8-process-coverage--baseline-review-2026-11-07) now explicitly enumerates original **A5-P1–P8** process coverage. **Only the Go Backend Builder conceptual I/P/O/O has been consolidated during the current A5 research**. The existing NextJS Builder (`FORMATION APPROVED / RESEARCH-ONLY` at an earlier exact revision) is a **historical/pre-A5 baseline requiring a fresh P3 audit**, not completed A5 frontend research. The other original processes are not closed by the Go model. The earlier idea to **start immediately with P6 Integration** was a candidate prioritization, **not a completed or newly approved P6 audit**; first re-evaluate pending frontend scope and other original P1–P8 responsibilities. This section clarifies coverage; it does not revise the original ORG-01 experiment or reopen historical NextJS formation approval.

## 2. What horizontal coherence means here

**Question:** Can the existing and still-to-be-assessed Engineering responsibilities, together with legitimate upstream providers and downstream consumers, account for the intended **end-to-end technical outcome** without an unowned critical handoff, conflicting authority, duplicate ownership, or unsupported completion claims?

This is about the **semantic relationship of I/P/O/O contracts and accountability**, not a universal execution sequence.

### Boundaries to inspect, without presuming a mandatory producer chain

1. **Upstream authority → effective Engineering obligations:** legitimate Product outcome/acceptance, relevant UX/UI/Design inputs and applicable project standards; trace actual provenance, revisions and standing. A Design artifact may be relevant but is not mandatory for every backend task.
2. **Engineering Solution/Rancang or another legitimate technical source → implementers:** who owns architecture, behavior, interface/state/security contracts and technical gaps? **Rancang is a possible producer, not a mandatory dependency** for every Engineering assignment.
3. **Implementation specializations → technical results:** NextJS frontend and generalized Go backend are available research cases, not exhaustive required Space types. Verify scope and authority edges instead of inferring technology choices or required Agent structures.
4. **Cross-boundary application integration:** who is accountable when separately correct frontend/backend/dependency implementations must work together? Check API/identity/state/error/uncertain-result compatibility and handoff; **do not pre-decide that a new Integration Space is required**.
5. **Technical verification, independent review and acceptance:** distinguish producer self-tests, independent assurance when justified, cross-boundary/system evidence, Human acceptance and operational delivery. Verify who may *claim* which outcome, and with which evidence.
6. **Downstream product/actor outcome and feedback:** engineering technical success is not automatically the actor outcome or project release. Clarify where unmet requirements, partial outputs, ambiguous real behavior and revisions are returned to legitimate owners.

**Non-linear applicability:** For a valid bounded task, some providers/consumers may be absent or handled in the same authorized responsibility. Do not create mandatory Product → UX → UI → Rancang → FE → BE → QA ordering. More than one legitimate producer can feed an implementation, and implementation can expose findings that must return upstream for a decision.

## 3. Proposed bounded A5 Engineering Builder coherence audit, not yet performed

Use currently authoritative *research* I/P/O/O definitions and exact approved standing, with immutable ORG-01 experiment as **case-specific traceability**, not as proof of general runtime success.

For each **material producer/consumer edge**, inspect:
- **Provided output → consumed input:** exact semantic obligation, completeness, source standing and version/acceptance scope.
- **Authority:** who can approve contract changes, clarify Product meaning, own technical decisions or authorize a consequential action.
- **Integration ownership:** who reconciles cross-component behavior and contract drift, including failure/partial/ambiguous outcomes.
- **Verification/evidence:** what work/result is asserted, what is genuinely observed, whether assurance is independent if required, and who receives partial/blocked results.
- **Missing/overlapping responsibility:** an actual unowned obligation, or duplicate ownership with conflicting decisions, rather than a gap invented by assuming an Agent per process/technology.

Suggested reasoning flow: gather relevant current research contract refs → map real required responsibility edges → challenge gaps/overlap/authority conflicts → recommend the **least new structure sufficient** for observed issues → record grounded findings and open questions in the **existing tracker**, linking any substantive audit artifact if separately needed.

### Candidate checks from original experiment

Original ORG-01 [Engineering / Builder snapshot](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/engineering-builder.md) describes **Integrated Application** and **Test & Verification Results** as end-to-end outputs. A specialized Go Backend Builder **does not own those whole outcomes automatically**. The next substantive question is whether and where the responsibility for **cross-boundary integration, verification and truthful handoff** is accounted for.

This is a *candidate gap to investigate*, **not** a finding that an Integration or QA Space must exist. The research must also check external upstream and downstream boundaries, not only relations among Engineering Spaces.

## 4. Horizontal episode completion boundary

The horizontal conceptual/source-level research episode is sufficiently complete when it has:
- An inspectable **responsibility/contract edge map** from legitimate upstream obligations through Engineering contributions to downstream consumers and relevant outcome claims, with exact source standing where available.
- For each material integration and verification concern, an accountable owner **or an explicit unresolved ownership decision** with legitimate owner/escalation recommendation; no silent filling of Product/Engineering authority gaps.
- Disposition of meaningful overlaps, contradictions, and partial/failure/uncertain-result handoffs; material open items clearly labeled rather than hidden.
- A bounded conclusion: what is **conceptually/source-coherent**, what remains a hypothesis, and what needs future real integration/Agent execution evidence.
- A recommendation to reuse existing responsibilities when sufficient, rather than a Space/Agent formation proposal by default.

Completion of this episode **does not establish integrated runtime behavior, independent end-to-end acceptance, or readiness of any Agent**. Do not stamp "all Engineering is proven" merely because the edge map looks complete.

## 5. Deferred Go Backend Builder vertical depth — explicit debt and closure level

**Debt:** The generalized Go Backend Builder's **I/P/O/O is sufficiently settled for working research**, but its detailed Space responsibility allocation, Agent composition, relevant skillset standards and actual execution behavior are **not yet designed/proven**. Postponement is intentional **sequencing**, not removal from scope.

**Resume trigger:** After horizontal boundary review is sufficiently coherent to inform legitimate specialized responsibilities (or if new material evidence makes earlier return necessary), explicitly revisit the debt. The tracker remains the status owner; no automatic background work or deadline is implied.

**Depth expected is fit-for-purpose, not exhaustive:**

### V1 — Formation-ready vertical *design depth* (required, not yet done)

- Derive one coherent **external capability/responsibility and I/P/O/O contract** from the current generalized research definition, accounting for partial/blocked/refused result semantics and consumer handoff.
- Decide the **smallest justified Agent/responsibility composition**, including meaningful reviewer independence and ownership of planning, implementation, integration, verification, technical escalation; **not** one Agent per Process or technology.
- Specify **core Engineering competence and conditional technology-specific skillsets** to the level needed for actual planned consumption: applicability/selection criteria, quality/safety/verification expectations, precedence below the effective project authority, and missing-competence handling. Do **not** implement every speculative Redis/Kafka/GraphQL/vendor variant upfront.
- Define how delegated authority, Human-in-the-Loop decisions, security, compatibility, failure/recoverability, environment boundaries and **truthful evidence claims** must survive Agent execution and handoff.
- Identify actual source/tool/runtime affordances and constraints as **requirements** without turning the Space into an Agent harness or mandating a universal skill-loader.
- Review the **exact proposed definition** for internal coherence and relevant upstream/downstream fit. Formation approval, if pursued, remains a **separate Human decision tied to exact bytes**.

**V1 closure means:** `VERTICAL_DESIGN_REVIEWED` / *formation-ready conceptual design*, **not** `SPACE_FORMED`, `RUNTIME_PROVEN`, or proof that Agent + skillset architecture works.

### V2 — Authorized real-use *execution depth* (required for a fully proven vertical claim; later episode)

- When **explicitly authorized** and supported by a real bounded assignment, run the intended Agent responsibility/competency arrangement in an actual available environment; test applicable contracts, integration, security/failure paths, and review independence **proportionally to risk**.
- Preserve revisioned evidence for source inputs, decisions/authority, produced artifacts, real checks/results, unverified portions, feedback and handoff; distinguish successful tool execution from correctly delivered backend behavior.
- Reconcile evidence-backed gaps in the Space/skillset/Agent design; re-review and reapprove materially changed exact definitions before claiming new formation standing.
- Declare only the level actually observed (e.g. source-reviewed, scoped test-run, integration-verified); **not production-ready by default**.

**V2 closure means:** Bounded **execution evidence** sufficient to support the claimed scope and conditions, **not** exhaustive proof for every possible Go technology, project, deployment, or error mode. If a suitable assignment has not yet been authorized/run, keep `VERTICAL_DESIGN_REVIEWED / EXECUTION_PENDING`; **do not close the full vertical-depth debt**.

The vertical debt is satisfied only to the extent **both design and relevant authorized execution** have evidence. A complete catalog of all backend technology skills, public onboarding, universal runtime orchestration or cross-project production deployments are **not required** to settle this bounded research debt.

## 6. Anti-duplication and standing discipline

- **Only active A1–A6 and horizontal/vertical debt status owner:** [existing cross-stage tracker](audit-revision-plan-and-tracker.md). This file has **no second status tables, IDs, checklist progress register or independent tracker authority**.
- Engineering [production and verification](../../engineering/production-and-verification.md) and [space formation](../../engineering/space-formation.md) remain relevant generic research guidance; this document does not override them.
- Research artifacts and historical commits are evidence/working definitions. `main` remains operational baseline; target-project contracts and runtime state remain owned by their actual projects.
- Do not modify current exact formed Rancang/NextJS definition merely to record this directional research decision; no Space/Agent invocations, project writes or runtime audits are approved by it.

**Next A5 research step (proposed for Anhar's sequencing decision, not executed):** perform a fresh **P3 Frontend Development / existing NextJS Builder source audit** against original P3 and current relevant Product/Design/Engineering authority. Reconcile P1–P2 and the scoped Go P4–P5 contribution, then inspect P6 **Integrated Application** accountability, P7 **Testing & Verification**, and P8 **Review & Handoff** with actual upstream/downstream joins. The [single tracker](audit-revision-plan-and-tracker.md#a5-original-p1p8-process-coverage--baseline-review-2026-11-07) owns progress. Vertical Go depth remains deferred and required; A6 remains later foundation-wide closure. No execution/formation or runtime evidence is implied.
