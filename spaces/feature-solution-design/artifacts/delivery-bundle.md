# S1 Solution Delivery Bundle — Consumer Contract

This is the **required logical shape** of an S1 delivery, not five mandatory files or a pre-written product solution. A single logical bundle may index **multiple output artifacts** with different types and consumers. The target project owns actual artifact locations, canonical contract authority and acceptance.

## Required sections

1. **Envelope:** project, target pinned baseline, Space definition pinned commit, invocation authorization, output-contract identity, actual producer/reviewer evidence, bundle revision, delivery status and **separate Human acceptance standing**.
2. **Authority & scope map (X1 link):** accepted original sources, approved/out-of-scope boundaries, affected consumers and relevant capability gap; explicitly separate proposed decisions from binding product requirements.
3. **O1 Shared solution decisions:** one coherent cross-boundary design, justification and responsibility allocation, approval standing for each material decision.
4. **O2 Interface, data & invariant contracts:** producers/consumers, types/transport, data-state ownership, error and incomplete semantics, persistence/atomicity obligations, identity/trust boundaries and contract versions needed by downstream work; authorized source contracts linked where actually written.
5. **O3 Experience solution contract:** significant entry/action/result/inspection states, positive and negative paths, consequence-before-effect, truthful provenance and UI/UX source adherence to the level required by project.
6. **O4 Verification obligations:** original acceptance → observable conditions, intended execution-level evidence (unit/contract/integration/rendered/security etc.) and responsible future actor; separate evidence planned from evidence executed.
7. **O5 Independent internal review:** material source-fidelity and O1↔O2↔O3 compatibility findings, revisions checked, unresolved decisions, precise conformance verdict and caveats.
8. **Artifact index and handoff:** list each separately consumable payload artifact (including logically addressable O1–O5 sections) with **type/kind, source and output contract refs, owning producer/project authority, artifact ref + pinned revision, required/conditional standing, intended consumers, review evidence, Human acceptance/decision standing and blockers**. State which consumer can use which current artifact and under which condition; finish with one next authorized action.

## Multiple payload artifacts (consumer-driven, not file-driven)

An S1 bundle can index shared **API/interface**, **state/data**, or **experience** contract artifacts in addition to the solution content **only when downstream needs or project authority justify them**. An API interface may be an O2 section or a separately linked contract; it becomes an authorized formal project API specification **only when the project owning authority approves its standing and writes**. FE and BE consume the **same compatible pinned shared-interface revision**, while their other input requirements may differ. If consumer-specific formal representation is missing or pending, label that consumer edge `conditional` or `BLOCKED` rather than silently claiming compatibility.

This index may be a compact table inside the same bundle: no mandatory manifest file, new directory structure or universal serializer. Duplicate references are acceptable, but **do not create competing owners or independent versions of the same binding interface**. If an artifact changes materially, recheck affected review, approval and consuming bindings before downstream use.

## Consumer acceptance check

The future Go Backend/Next.js Frontend/Integration/Assurance actor must inspect the actual versioned bundle plus owning originals. Identify **generic port conformance** separately from **concrete assignment binding compatibility**; do not claim this passed before those Spaces/contracts exist. A Human may accept a bounded residual risk, but it must be explicitly understood and scoped, not silently converted to a generic PASS.

**COMPLETE** means S1's design-delivery obligations were fulfilled and internally reviewed; it does **not** claim C1 implemented, product integration tested, project solution approved, security permissions granted, or acceptance by Human. Human acceptance for downstream is a separate recorded fact.

Use [artifact standards](format-and-traceability.md) for record metadata, [output contract](../contracts/output.md) for mandatory semantic coverage and [shared handoff requirements](../../../space-formation/contract-and-readiness.md) for package/consumer facts.
