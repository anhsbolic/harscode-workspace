# A4 — Engineering Solution: Experiment-Led Source Audit & Bounded Alignment Proposal

> **Standing:** A4 SOURCE-LEVEL RESEARCH AUDIT / HUMAN REVIEW PENDING (2026-11-04). This is an evidence-backed proposal, **not** an approved change to an existing formed Space, not a new formation, not operational Harscode `main`, not a runtime test, and not a target-project decision.
> **Decision owner:** Anhar.
> **Repository/branch:** `anhsbolic/harscode-workspace` / `research/cross-stage-mapping`.
> **Experiment precedence:** The previously Human-approved [Engineering Solution working model at immutable historical revision](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/rancang-engineering-solution.md) is the **target semantic reference**. The older formed Rancang definition is the subject of alignment. Where its existing design may be materially better, surface the evidence and seek Human decision; **do not silently substitute it for the approved experiment**.

## 1. Scope, exact source evidence, authority

Read-only inspected research-branch source at the A4 entry checkpoint:

| Source | Inspected Git blob SHA | Role in audit |
| --- | --- | --- |
| [Engineering Solution Space entry](../../engineering/spaces/feature-solution-design/README.md) | `16ed0713bf93be3099f8fc8ff5df6a9f6a3fdcac` | Mission, boundaries, existing formation standing |
| [External Input / Output Contract](../../engineering/spaces/feature-solution-design/contracts.md) | `98185cd1b1b75b4bb1be499370b0673fb4e69d07` | Existing binding logical input/output semantics |
| [Coordination](../../engineering/spaces/feature-solution-design/coordination.md) | `51d4f338e9592a5c4e58c12f3fd034374a18cbcc` | Human gates, producer/reviewer ownership, durable resumption |
| [FR-01–FR-04 formation record](../../engineering/spaces/feature-solution-design/formation-approval-2026-10-30.md) | `2f7a029872b019e8e483c738b28cad210de06fda` | Current-tree historical approval pointer; original exact content in immutable Git |
| [Product Definition](../../product/product-definition.md) | `1d423cee38b7cc159d9855f99b519d5c065277cd` | Approved-research Product boundary and input meaning |
| [UX Definition](../../design/ux/definition.md) | `a503a571342868bb960973de4c9df9f3f9a190d8` | Approved-research UX O2/O6 and other material UX responsibilities |
| [UI Definition](../../design/ui/definition.md) | `53d293cdf8a5f635690123a76de521f63e78b83f` | Approved-research UI boundary; Hi-Fi is not a universal Rancang predecessor |
| [Project Design Standards](../../design/project-standard/definition.md) | `7ebb9d3c90630c1884e89136deca6157683182fe` | Accepted research project-level reusable Design authority |
| [NextJS Builder contract](../../engineering/spaces/nextjs-builder/contracts.md) | `73d86ccc2589164b6155533047d3babb7f02aeb6` | Known generic frontend consumer shape, not actual project-bound execution |

Also inspected all six Rancang `agents/*/agent.md`, their six agent-owned `knowledge.md` references, relevant artifact contract/templates and [Engineering Space formation discipline](../../engineering/space-formation.md).

**Formation safeguard:** The exact Rancang definition `6dfc4be790c526026529ed7ef397c61567809de4` received **FORMATION APPROVED / RESEARCH-ONLY** on 2026-10-30. Comparison against the current research branch shows external `contracts.md`, `coordination.md` and six Agent definition contents retain their exact approved blobs; later Rancang-tree edits affect entry/status/formation-record documents, not those substantive contracts. Approval is **not** runtime readiness or permission to invoke/write. Any substantive amended Space definition requires its **own new formation review and Human approval**.

## 2. Input sufficiency against the approved experimental 13 information needs

The existing Rancang contract has four **acquisition categories**, not 13 physical inputs: Bounded Work Input; Applicable Project Standards; Technical Context; Human Authorization. This packaging is not a defect by itself. Audit actual meaning and material requiredness:

| Experiment input | Existing source coverage / disposition |
| --- | --- |
| I01 Product Contract | **COVERED.** Bounded Work Input includes accepted Product semantics and exact standing, with technical-origin authorized alternative. |
| I02 UX Flow Diagram | **UNDER-EXPLICIT.** Accepted Design is mentioned generally, but the current external contract does not explicitly identify decision-relevant UX flow evidence. |
| I03 Lo-Fi Wireframes | **UNDER-EXPLICIT.** Rancang should consume applicable accepted UX O6 evidence for new/material screen UX; this is **not** a requirement for Rancang to create wireframes or for technical-only assignments to invent screens. |
| I04 Information Architecture & Navigation | **UNDER-EXPLICIT.** Current text discusses actor experience but not explicit original UX IA, webpage route/page-vs-state semantics and their owner. |
| I05 Interaction & UI State Requirements | **PARTIALLY COVERED.** Engineering Experience O3 covers truthful action/result/unknown/recovery; explicit source from accepted UX O7 and Product distinction should be tightened where material. |
| I06 Existing Codebase & Architecture | **COVERED.** Technical Context and Architect source inspection. |
| I07 Engineering Standards & Tech Stack | **COVERED.** Effective project standards, applicable architecture and Engineering Standards Evolution when justified. |
| I08 Security & Privacy Requirements | **COVERED.** Applicable source standards plus independent Security Analyst and Human gates. |
| I09 Existing API Contracts & DB Schema | **PARTIALLY EXPLICIT.** Technical Context includes active interfaces; Architect knowledge includes data model/consistency, but database/schema material inputs are not clearly named in external contract. |
| I10 Integration Requirements | **COVERED CONDITIONALLY.** Technical Context and consumer/producer integration constraints. |
| I11 Non-Functional Requirements | **COVERED IN PRACTICE / UNDER-EXPLICIT IN CONTRACT.** Architect knowledge considers latency, reliability, scale, deployment/operational cost; no need for a universal NFR checklist. |
| I12 Test & Acceptance Scenarios | **COVERED.** Binding acceptance, Requirements X1 and verification obligations O4. Planned vs performed evidence distinguished. |
| I13 Technical Research / PoC | **CONDITIONAL BY NEED.** Architect must investigate unresolved delegated mechanisms, but a PoC is not a universal pre-existing input. |

**Main input finding:** For materially user-facing solution decisions, the approved Product/UX information contract should be discoverable explicitly from effective project originals. Approved UX O2 Flow and O6 representative Lo-Fi are **required by default for new/material UX scope** (or accepted exact-revision equivalents/evidence-backed exceptions). The Rancang contract must not silently downgrade them into Engineer-invented experience assumptions. Exploratory engineering may continue with clearly labeled provisional UX information; binding dependent solution/consumer claims require sufficient actual UX authority. Rancang must not force completion of a named UX Space or require Hi-Fi as a default input.

## 3. Process and output alignment

The experiment defines **ten logical iterative activities**: requirements, feasibility, architecture, auth, API/data, failure/recovery, security, verification planning, review, handoff. Existing Rancang assigns them across Requirements Analyst (X1), Architect (O1/O2), Experience Specialist (O3), Security Analyst and independent Solution Reviewer (separate findings), per-obligation O4 producers, and Coordinator (O5/handoff). **Substantial functional coverage exists.** Ten activities do not justify ten Agent roles, a ten-step waterfall or a second Space.

The experiment's **eight logical Engineering Solution outputs** map to Rancang's existing **X1 + O1–O5** as follows:

| Experiment output | Existing Rancang coverage / outstanding clarification |
| --- | --- |
| Engineering Solution Blueprint | O1/O2 decisions, feasible architecture, rationale and inter-consumer boundaries; **covered**. |
| Authentication & Authorization Design | O2 technical authorization/state design, Architect and independent Security assessment; **covered where material**. |
| API Contract | O2 includes complete proposed typed contract when an actual consumer requires it; **covered**, with separate canonical adoption. |
| Data Model & Database Design | O2/Architect knowledge covers data ownership, consistency/transactions; **UNDER-EXPLICIT** for entities, relations, constraints, schema/persistence, migration/compatibility when a solution needs them. |
| State & Error Handling Design | O2 experience-aligned errors, unknowns, idempotency/recovery and O3 bridge; **covered**. |
| Security Design | O1/O2 proposed controls plus independent Security Findings and O4 obligations; **coverage present**, but assurance findings must not substitute for the accountable producer's actual security mechanism design. |
| Technical Verification Specification | O4 per-obligation checkable criteria and evidence distinctions; **covered**. |
| Engineering Solution Handoff | O5 revisioned, consumer-aware, Human-facing package with independent findings; **covered**. |

Six desired experimental qualities — **Feasible, Secure, Consistent, Reliable, Implementable, Verifiable** — have credible coverage through the formed contracts and reviews. They remain desired **design** outcomes, not measured runtime success. Atomicity/consistency must be traced to *material accepted Product invariants*; it is not a blanket distributed-transaction mandate.

**Preserve existing justified safeguards:** independent Security assessment and Solution Review; actual Human gates; O4 producer ownership; source original/revision checks; conditional deterministic typed O2 for real consumers; per-consumer generic vs project-bound compatibility; durable resumption and refusal of invented runtime PASS. These are additions of substance, not contradicting experiment authority.

## 4. Findings and recommended disposition

| ID | Priority | Evidence-backed gap / risk | Recommended disposition |
| --- | --- | --- | --- |
| **A4-F01** | **HIGH** | Existing Rancang input contract does not make applicable accepted UX O2/O6, IA/navigation/web routes and UX O7 source/standing sufficiently explicit. Engineer could proceed from inferred experience while the approved UX material remains absent. | **CLARIFY** `contracts.md` input sufficiency, with narrowly aligned Coordinator/Requirements/Experience checks only if necessary. Scope UX requirements by actual decision; no mandatory upstream Space or fresh documents. |
| **A4-F02** | **MEDIUM–HIGH** | Database/data-model solution obligations live in broad O2 and Architect knowledge rather than explicit externally inspectable model/constraint requirements. Two implementers could infer incompatible persistence and transaction behavior. | **CLARIFY** conditional O2 coverage for entities/relations/constraints, persistence, transaction/invariant and migration/compatibility decisions when material. Check verification O4 consumer trace. |
| **A4-F03** | **MEDIUM (preventive)** | Security mechanism design is distributed across O1/O2 while independent Security Findings live in O5; without explicit review trace, an assessor report could be mistaken for a complete protection design. | **CLARIFY only if needed** in output/Reviewer sufficiency: accountable Engineering design plus independent risk assessment and test obligations, not an extra mandatory Security Design file. |
| **A4-F04** | **LOW / project-agnostic hygiene** | Current Rancang README uses a case-style historical identifier as a Human invocation example. It needlessly exposes a particular experimental lineage in reusable active guidance. | **REPLACE example identifier with neutral placeholder** only within an authorized revision; do not rewrite historical exact formation records or hide provenance. |

**Important nonfindings:** Four Rancang input categories instead of thirteen are not a defect; X1/O1–O5 instead of eight files are not a defect; six Agents instead of ten activities are not a defect. Rancang's bounded Engineering Standards Evolution remains a legitimate conditional supporting responsibility, not a new project Design Standards authority. Hi-Fi UI is **not** a mandatory Rancang predecessor or default media-processing requirement. The NextJS Builder contract is frontend-specific and does not prove end-to-end backend/DB consumer readiness.

## 5. Proposed scoped next change — not authorized yet

**Recommendation:** preserve the existing formed Rancang capability and its independent assurance, and perform the **smallest semantic alignment** of its contract to the approved experiment: first make material UX original inputs and acceptance/default evidence explicit; second make required data-model/persistence design outcomes explicit; clarify security design/assurance attribution only to the extent source-based consumer checks show necessary. Neutralize the active reusable README's case-specific invocation example. Do **not** rewrite the whole Space into ten phases, add Agents/Spaces, duplicate project authority or replace current effective formation by assumption.

Before any owning Rancang semantic edits:
1. Anhar reviews the A4 gap classification and exact recommended scope.
2. Prepare a minimal affected-file proposal and check formation/consumer/security impact against the immutable approved `6dfc4be` definition.
3. If material definition bytes change, conduct fresh **formation review and exact Human approval**. Preserve old approved revisions and clearly label new unapproved candidate until accepted.
4. Continue A5 Builder and A6 cross-stage coherence only after A4 research decision is settled or appropriately bounded.

## 6. Verification standing and limits

**Performed:** GitHub source-level inspection of experiment original and current formed Rancang definition, six Agent roles/knowledge, artifact envelope/templates, formation history, Product/UX/UI/Project Standard research boundaries and the existing frontend Builder generic contract. Existing Rancang contracts, coordination and Agent definition SHA equality with approved `6dfc4be` confirmed; no owning Rancang files were edited.

**Not performed:** real independent Rancang/Builder consumer run, native Harness tool/role isolation, end-to-end runtime consistency/security, live API/schema adoption, project-bound implementation, browser/UX usability or formation review of any new A4 proposal. **A4 remains HUMAN REVIEW PENDING**; findings are source-based proposals, not a confirmed runtime failure or automatic authorization to revise the formed capability.
