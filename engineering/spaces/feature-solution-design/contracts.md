# Rancang — External Input / Output Contract

> **Standing:** Post-formation material research amendment candidate / **NOT FORMATION APPROVED**. The approved six-Agent vNext definition remains pinned to `9663a3fa73ac0101e66764d63af8711f291a66ab`; semantic edits on this branch require a separate exact-revision Human formation decision. This document grants no invocation, source writes, or runtime claims.
> **Owner:** Reusable Rancang Engineering Solution Design capability; effective project inputs, standards and accepted artifacts remain owned by the target project.

## 1. Input Contract: meaning versus acquisition

Rancang has **one logical Input Contract**, not a requirement that Human or Product deliver four files. Each category below has an explicit producer/authority and an acquisition path.

| Category | Required meaning | Acquisition and boundary |
| --- | --- | --- |
| **Bounded Work Input** | Identifiable objective, intended outcome or defect, binding obligations, observable acceptance, exclusions, scope, standing and effective source revision | Human reference or upstream handoff. For Product-origin work, a self-contained approved Product Contract plus exact-revision approval may suffice. For technical-origin work, an authorized technical objective/defect with sufficient acceptance may suffice. |
| **Applicable Project Standards** | Effective, materially applicable Product-wide constraints and Design, Engineering and security standards, with their scope/revisions | Discover from project-owned authoritative sources; these are not automatically separate upstream handoff artifacts. Specific approved Design deliverables are binding when the assignment requires them. |
| **Technical Context** | Relevant current codebase, repository/ref, active interfaces, architecture evidence and consumer constraints, with known freshness/limits | Scoped read-only inspection of target-project sources. Existing implementation is evidence, not Product/Design authority. Local development environment preparation and Harness certification are outside Rancang. |
| **Human Authorization** | Resolved bounded assignment, tools/actions, write destinations, intended consumers, supervision mode and consequential gates | Obtained through Human-direct invocation. A short identifier is enough to begin permitted discovery; it is **not** blanket production or write authorization. |

**Input acceptance** checks the relevant declared work input's scope, approval/authorization standing, revision, and sufficient behavioral/technical obligations for a bounded design task. It does **not** audit an upstream Product/Design process, relitigate settled meaning, or reconstruct extra Product policy from old research. The owning approved artifact remains binding in its declared scope.

For user-facing assignments, relevant accepted actor goals, journey consequences and applicable Design constraints are first-class Engineering design inputs, not after-the-fact labels for a selected mechanism. For technical-only assignments, derive the relevant operational/consumer consequences without inventing a user journey or requiring UI exploration. Neither case grants Rancang new Product/Design authority or mandates additional upstream artifacts.

**Work readiness** separately assesses applicability of standards and technical facts. Absence of a file is not necessarily absence of a needed rule; absence of a *material* Design/Product decision cannot be filled with Engineering guesses. Lack of an Engineering standard is not an automatic refusal: evaluate whether a delegated solution suffices, then consider bounded Engineering Standards Evolution.

## 2. Entry, sufficiency, and Human questions

Coordinator accepts concise natural-language start/resume plus an identifier and resolves project, artifact standing, prior assignment(s), and authorized scope from accessible durable sources. It asks Human only for genuine ambiguity, unresolvable material input, consequential authorization, or decisions beyond delegated Engineering scope.

- **Invalid input:** Required bounded authority, binding acceptance or scope is absent/contradictory/unverifiable for affected work; report exact deficiency and hold dependent production. No automatic duty to send work back to an upstream Space.
- **Valid input with missing external decision:** Report specific blocked solution edge to Human; Product/Design decisions are not made by Rancang. Human may discuss in the same session, but a changed owning authority must be approved and durably effective before being relied upon.
- **Valid input with unknown Engineering mechanism:** Assigned Agents must investigate substantively within delegated authority; explain tried/reasoned approaches and evidence before returning unresolved. Unknown mechanism alone is not invalid input.
- **Authorization or capability gap:** Hold only affected actions, state what permission/evidence is missing; recommend Human-scoped specialist assistance if a material gap remains beyond the Space.

Independent permitted work may continue without laundering unresolved decisions into approved contracts.

## 3. Bounded Engineering Standards Evolution

Existing effective Engineering Project Standards are the default authority. Architect checks their **adequacy for the assigned solution**, not their theoretical optimality. No speculative modernization or rewriting project standards for taste.

Where a **material** missing, contradictory, unsafe, insufficient, or disproportionately costly Engineering standard would compromise the actual assigned solution:

1. Solution Architect first checks whether an ordinary delegated feature-level decision can solve the problem.
2. If not, Architect produces a **bounded standards proposal**: actual deficiency, effective source and revision or explicit absence, proposed smallest sufficient rule/change, alternatives where consequential, security implications, impacted consumers, compatibility/migration/rollback as relevant.
3. Security Specialist independently examines material security effects; Solution Reviewer assesses necessity and wider contract/consumer fit.
4. Coordinator presents the **exact proposed standard revision and owning artifact/action** for authorized Human approval.
5. Only separately authorized writes may persist the approved standard to its project-owned location; Architect may execute such a scoped update inside this Rancang assignment. Approval is not effective persistence.
6. Reopen the effective revision and revalidate only affected solution outputs, consumer edges and independent reviews.

This conditional capability does **not** grant general Engineering governance authority or permission to update canonical *feature* API/OpenAPI/schema contracts, implementation, protected security code or deployment. Proposed feature-level interface/state contracts remain Rancang handoff payloads for their authorized downstream owners.

## 4. Engineering Obligation Map (legacy anchor X1)

Requirements Analyst derives a compact, revision-anchored **Engineering Obligation Map** from the accepted effective work input and materially applicable standards: obligations/invariants, negative paths, exclusions, decision freedoms, verification and consumer implications. It is a trace and derivation aid, not new Product/Design authority or an upstream policy reconstruction. Producer and independent Reviewer re-read effective originals when material.

## 5. Output Contract: Engineering Solution Handoff

One coherent, revision-pinned bundle must provide **applicable logical coverage** of the following, with named accountable producers. Relevant experience needs and feasibility/cost constraints must inform material solution selection **before those decisions are treated as settled**, with iterative Architect–Experience challenge where useful; output anchors do not dictate a sequential production order. The legacy anchors X1/O1–O5 remain navigation/trace labels during this amendment; semantic names define the obligations and **do not mandate separate files or execution phases**.

| Semantic output (legacy anchor) | Accountable owner | Acceptance obligation |
| --- | --- | --- |
| **Engineering Obligation Map (X1)** | Requirements Analyst | Accepted input → bounded engineering obligations, freedoms, exclusions, negative paths and source links |
| **Shared Solution Decisions (O1)** | Solution Architect | Material design choices, rationale, relevant experience/consumer constraints, feasibility and proportional alternatives/trade-offs; standards proposals/revision refs when needed |
| **Technical Interface & State Contracts (O2)** | Solution Architect | Consumer/producer behavior, data/state ownership, authorization, consistency, results/errors/unknowns and typed proposals when actually required |
| **Engineering Experience Contract (O3)** | Experience Specialist | Relevant actor/consumer experience needs informing O1/O2, truthful action/state/consequence semantics reconciled with actual O2 guarantees, and material downstream interaction-readiness gaps where applicable; no mandatory wireframe or UX design approval |
| **Verification Obligations (O4)** | One named accountable **producer per obligation** | Checkable success/negative/risk outcomes, intended verification owner, performed vs not-run evidence |
| **Independent Findings and Handoff (O5)** | Security Specialist owns security findings; Solution Reviewer owns independent solution review; Coordinator owns bundle assembly and Human-facing standing | Original/effective source and exact-output review, material experience-versus-Engineering trade-off recommendation, security-finding disposition, consumer fit, unresolved decision/limits, revisioned index and Human gates |

Design/readiness consideration is proportional: a material user-facing interaction ambiguity must have a visible owner and disposition under effective project Design rules; Rancang may explain or compare bounded alternatives but does not impose mandatory low-fidelity artifacts, issue Design approval, or take over downstream implementation. A non-UI task needs only materially relevant consumer/operational experience checks.

Security Findings are **independently owned evidence**, not additional mandatory file count or an automatically passed security gate. Security Specialist documents proportionate assessment and limitations; risk-heavy scope demands deeper scrutiny. Solution Reviewer checks disposition and coherent overall contract coverage, not a substitute self-made security verdict. If independence or original-source access cannot be demonstrated, it remains **UNVERIFIED**.

Every applicable output/section has an exact source/producer/output revision, decision standing (approved external authority versus delegated proposal), review/evidence status, intended consumer and actionable limitations. Choose the target project's applicable representation; an index/section anchor is sufficient unless the consumer actually requires a separate typed handoff.

### Per-consumer compatibility (two distinct checks)

For **each intended downstream consumer**, record the applicable compatibility checks:

- **Generic compatibility:** When the consumer has an applicable **declared reusable Input Contract**, check whether the output type, semantics, completeness and standing satisfy it. For a consumer without such a contract (for example, a direct frontend/backend implementation owner), record **NOT APPLICABLE** with the reason; do not fabricate a reusable Space contract or misclassify true non-applicability as UNVERIFIED.
- **Project-bound compatibility:** **Always** check whether this actual handoff revision satisfies that consumer's current target-project accepted input, required format, security and authorization constraints, whether the consumer is a Space or not.

For each applicable consumer check report the exact checked source/output revisions and evidence, or label **CONDITIONAL / BLOCKED / UNVERIFIED** with the missing decision, format or evidence. **NOT APPLICABLE** is reserved for a genuinely absent/inapplicable generic contract, never for project-bound compatibility. Generic fit does not imply project-bound fit. In particular, a proposed O2 technical contract is not an adopted canonical feature API/schema; where an intended consumer requires a separately addressable typed interface or authorized spec adoption, identify that external dependency and do not claim implementation readiness. A plausible handoff is not evidence of an executed consumer compatibility check.

**Design handoff fit** and **actual canonical-contract or implementation readiness** are different claims. Rancang never edits the target project's canonical feature API/spec as a consequence of authoring O2; authorized downstream owners incorporate Human-accepted proposals under their own gates.

## 6. Contract conformance and stopping rules

Coordinator is accountable for the **external Input → Output Contract**, including assignment identity, source/output joins, **confirming and recording one accountable producer per applicable O4 obligation**, internal Agent returns, required independent review and an inspectable Human-facing bundle. Material Architect–Experience disagreement requires bounded examination, an independent Reviewer recommendation and accountable producer disposition; consensus is not a universal gate. If a consequential decision remains unresolved beyond delegated authority or sufficient evidence, hold only the affected edge and present precise alternatives, trade-offs, recommendation, dissent and required Human decision. Producers may propose ownership, but do not unilaterally assign other Agents. Coordinator does not silently write producers' substantive decisions or rewrite independent findings.

- **COMPLETE**: all applicable production, reconciliation, verification-obligation and required independent assessment/review obligations are fulfilled **and no unresolved material finding or consequential undecided trade-off defeats a binding obligation or consumer-critical solution contract**. Non-blocking findings/limits may remain explicitly recorded. Completing a review or listing an unresolved blocking finding is not sufficient. Not Human acceptance or implementation readiness.
- **PARTIAL**: required output coverage/evidence or correction remains incomplete but meaningful, accurately scoped deliverables exist; identify the affected consumer/obligation and unresolved finding.
- **BLOCKED**: material authority, authorization, unresolved blocking finding or critical dependency prevents the affected production/consumer-ready claim; unaffected authorized work may continue.
- **FAILED**: attempted production did not succeed.

Distinguish PROPOSED, DELEGATED, HUMAN-ACCEPTED external revisions, UNRESOLVED and actually tested/NOT RUN evidence; do not equate them. If original/standard/solution revision changes, invalidate only affected acceptance or review edges and re-evaluate them.

Human acceptance of exact bundle revision is separate from Rancang COMPLETE and from authorization of downstream canonical contracts or implementation. Runtime enforcement/readiness remains with the selected Harness and its owner, **not** established by this definition.

## 7. Runtime binding requirements (external to Rancang)

The selected Harness must demonstrate the material, applicable capabilities below before concrete authorized production. This is a **declarative requirement contract for the Harness owner**, not permission or a duty for Rancang to certify/install the runtime.

| ID | Required capability and observable evidence |
| --- | --- |
| **R1 — Source fidelity** | Required Agents can inspect current effective originals, relevant standards, actual code evidence and exact source revisions rather than relying on summaries alone. |
| **R2 — Bounded artifact writes** | Actual tool permissions/write containment respect scoped artifacts and protected paths, or the unenforced boundary is reported accurately and affected writes are held. |
| **R3 — Scoped Specialist context** | Role-specific references, knowledge and permissions can be supplied without uncontrolled expansion of context or authority. |
| **R4 — Independent assessments** | Security Specialist and Solution Reviewer can inspect original sources and exact producer outputs in meaningfully independent contexts. Naming two roles is not evidence of independence. |
| **R5 — Versioned handoffs** | Producer, reviewer, source, output and decision revisions remain traceable across role returns, final bundle and durable project-owned state. |
| **R6 — Enforceable Human gates** | Exact-revision/action-scoped Human approval and permission controls hold consequential, protected, Engineering Standard and scope-expansion actions until authorized. |
| **R7 — Truthful executed evidence** | Actual tool/test/review observations and limits are distinguishable from planned, omitted, unverified or simulated work. |
| **R8 — Observable Human-direct coordination** | Human can invoke and supervise the named Coordinator and observe material gates, results and resumable state; no Balad dispatch or hidden Orchestrator is assumed. |

Assess actual runtime evidence under [Engineering Runtime Binding](../../../harness/runtime-binding.md), with depth proportional to the risks and requirements of the authorized assignment. Missing evidence is **NOT READY / UNVERIFIED**; definition approval does not prove security containment, independent context, resumption or executable readiness. This section specifies properties only and creates no mandatory scheduler, state engine, process topology or environment-preparation responsibility.

## 8. Hard exclusions and quality floor

No self-invocation, fabricated approvals or independent review, unapproved protected writes, Product/Design policy decisions, Design Standards creation, local environment setup, Harness certification, feature code/migrations/deployment, canonical feature contract mutation, or general project orchestration. Consequential external decisions go **to Human**; Rancang does not own routing/repair of another authority's artifacts.

Every Engineering Agent must prefer the least additional complexity sufficient for accepted correctness, material security/privacy, reliability, operability and verification needs. A technical unknown calls for substantive effort and evidence, not reflexive refusal; complexity must justify its cost. Do not weaken mandatory safeguards for simplicity.
