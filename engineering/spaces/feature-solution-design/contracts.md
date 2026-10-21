# Rancang — External Contract and Safeguards

> **Applicability:** Definition approval standing is tracked at the Space entrypoint and its exact-revision Human formation decision. This contract alone authorizes no runtime work.
> **Owner:** Rancang reusable Engineering capability; concrete project inputs/outputs belong to their owners.

## Required input classes

| ID | Meaning |
| --- | --- |
| **I1** | Approved bounded product/technical objective, behaviors, acceptance and owning source revisions; binding versus evidence explicit |
| **I2** | Current Design, architecture, security and implementation constraints, source precedence and protected-path policy |
| **I3** | Exact project repository/ref/SHA, relevant active code/contracts, read access and environment facts |
| **I4** | **Human-direct** assignment: bounded design responsibility, downstream consumers, output/state paths, permitted tools/writes, mode and consequential Human gates |

Missing or contradictory material authority, inaccessible code, incompatible consumer expectation or unauthorized write scope means REFUSE/BLOCK the affected action. Engineering design freedom is not by itself missing Product Authority.

## Source-obligation bridge (X1)

Before producing solution decisions, the assigned source/authority responsibility maps **original** I1–I3 anchors to accepted behaviors, invariants, acceptance evidence, relevant Design constraints, owners, source revisions, delegated freedoms, and unresolved Human decisions. Call this logical map **X1**; it may be a section of the bundle rather than a separate file or Agent. X1 is a trace aid, not new Product/Design authority. An original-source conflict stays unresolved until its owner decides; a summary cannot override the original.

## Required outputs (logical coverage)

| ID | Result |
| --- | --- |
| **O1** | Shared material solution decisions, rationale, ownership and meaningful cross-boundary trade-offs |
| **O2** | Producer/consumer interface, data, authorization, persistence, state, result/error and invariant contracts |
| **O3** | Interaction/experience contracts protecting approved consequential meaning, uncertain/error/unauthorized states and durable inspectability |
| **O4** | **Producer-owned** verification obligations derived from X1, O1–O3, original acceptance, relevant risks and negative paths |
| **O5** | Original source revision → decisions/output trace, independent review findings and limits, revisioned handoff, Human approval standing and consumers |

Coverage is compulsory when applicable; a five-file bundle is **not** required. Use [artifact guidance and optional representations](artifacts/README.md) only when useful for the actual consumer. **Current project-owned standards/templates prevail over Space examples**, subject to original Product/Design authority, security and Human gates. A consumer may require an independently addressable typed API contract; formal OpenAPI/spec edits need separate project authorization. An API shape cannot be invented as an approved project contract.

## Bundle and consumer conformance

The Solution Delivery Bundle must offer an inspectable, **revision-pinned** index of X1 and applicable O1–O5 sections or linked payloads. For each material payload, identify type/ID, owning producer and source authority, actual artifact ref/revision, input/source revisions, approval or proposal standing, review/evidence standing, intended consumer, outstanding decisions and consumption limits. A section with a stable anchor is sufficient; do not require one file per output. Where a consumer needs a separately addressable formal interface, mark its owner, expected form and authorization/availability instead of silently treating draft O2 as approved OpenAPI.

For each intended consumer, distinguish (a) **generic contract fit** from (b) **current project-bound fit** against that consumer's actual accepted input, source and security constraints. State whether each consumer edge was actually checked, remains conditional, or is blocked, and name the specific missing evidence or decision. Never report that consumer implementation-ready while a binding dependency is unresolved. Human acceptance applies to an exact bundle/payload revision; it is not implied by `COMPLETE` production or internal review. Actual acceptance and compatibility evidence live with the owning project.

## Internal responsibility and evidence

Required functions are owned by explicit [Agent actors](coordination.md): Requirements Analyst (X1), Solution Architect (O1/O2 and applicable O4), Experience Specialist (O3 and applicable O4), Independent Solution Reviewer (O5 findings), and Space Coordinator (revisioned assembly and Human-facing O5 gate/state/handoff). The two producers may jointly author O4, with a named accountable artifact owner. Reviewer independently inspects original I1–I4 and current X1/O1–O4 for acceptance coverage, source fidelity, O4 adequacy and consumer compatibility, without editing producer deliverables. **Agent identity is defined, while runtime instance/session count, context isolation and effective enforcement remain UNVERIFIED.** A producer self-check cannot be independent assurance.

Minimum runtime demands remain: **R1** source fidelity, **R2** bounded artifact writes, **R3** scoped Specialist context/knowledge, **R4** reviewer independence, **R5** versioned handoffs, **R6** enforceable revision-bound Human gates, **R7** truthful executed evidence, **R8** observable Human-direct coordination. Actual readiness is NOT VERIFIED by this document; [Harness runtime binding](../../../harness/runtime-binding.md) owns observed enforcement evidence, not this declarative definition.

Human formation approval is separate from Human-direct invocation. Conditional Human gates stop unresolved owner product decisions and protected/security scope changes. Final Human acceptance of the **exact output revision** is separate from Space completion. Default supervised; autonomous requires explicit separate Human authorization and still obeys hard gates.

## Result standing

Production result `COMPLETE / PARTIAL / BLOCKED / FAILED` is distinct from item standing `APPROVED SOURCE / DELEGATED / PROPOSED / UNRESOLVED`, Human acceptance, and evidence scope (`DESIGN REVIEWED` does not mean `RUNTIME VERIFIED`). `COMPLETE` means applicable outputs and internal review obligations are fulfilled with truthful limits, not Human acceptance or runtime verification. `PARTIAL` means some required coverage or evidence remains incomplete; `BLOCKED` means a material authority, permission or consumer-critical dependency prevents the affected action/claim; `FAILED` means attempted production did not succeed. Mark unperformed checks `UNVERIFIED` without upgrading them to independent assurance. No untested output is called implementation-ready if a consumer-critical invariant or contract is unresolved.
