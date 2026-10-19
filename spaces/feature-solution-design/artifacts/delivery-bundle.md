# S1 Solution Delivery Bundle — Consumer Contract

This is the **required logical shape** of an S1 delivery, not five mandatory files or a pre-written product solution. The target project owns the actual artifact location and any accepted contract.

## Required sections

1. **Envelope:** project, target pinned baseline, Space definition pinned commit, invocation authorization, actual producer/reviewer evidence, output revision and status.
2. **Authority & scope map (X1 link):** accepted original sources, approved/out-of-scope boundaries, affected consumers and relevant capability gap; explicitly separate proposed decisions from binding product requirements.
3. **O1 Shared solution decisions:** one coherent cross-boundary design, justification and responsibility allocation, approval standing for each material decision.
4. **O2 Interface, data & invariant contracts:** producers/consumers, types/transport, data-state ownership, error and incomplete semantics, persistence/atomicity obligations, identity/trust boundaries and contract versions needed by downstream work; authorized source contracts linked where actually written.
5. **O3 Experience solution contract:** significant entry/action/result/inspection states, positive and negative paths, consequence-before-effect, truthful provenance and UI/UX source adherence to the level required by project.
6. **O4 Verification obligations:** original acceptance → observable conditions, intended execution-level evidence (unit/contract/integration/rendered/security etc.) and responsible future actor; separate evidence planned from evidence executed.
7. **O5 Independent internal review:** material source-fidelity and O1↔O2↔O3 compatibility findings, revisions checked, unresolved decisions, precise conformance verdict and caveats.
8. **Handoff:** which downstream responsibilities can consume which current output refs, at what confidence, which gates or missing input block consumption, and one next authorized action.

## Consumer acceptance check

The future Go Backend/Next.js Frontend/Integration/Assurance actor must inspect the actual versioned bundle plus owning originals. Identify **generic port conformance** separately from **concrete assignment binding compatibility**; do not claim this passed before those Spaces/contracts exist. A Human may accept a bounded residual risk, but it must be explicitly understood and scoped, not silently converted to a generic PASS.

**COMPLETE** means S1's design-delivery obligations were fulfilled and internally reviewed; it does **not** claim C1 implemented, product integration tested, project solution approved, security permissions granted, or acceptance by Human. Human acceptance for downstream is a separate recorded fact.

Use [artifact standards](format-and-traceability.md) for record metadata and [output contract](../contracts/output.md) for mandatory semantic coverage.
