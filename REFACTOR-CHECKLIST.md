# Harscode Foundation Refactor — Checklist

> **CURRENT PRODUCT ROUTING (2026-10-23):** Kencleng Product output uses the [formal Product catalog](product/README.md) and [Kencleng current Product entrypoint](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/README.md). Outcome `ORG-01` is approved at [current Product Contract](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/outcomes/org-01/product-contract.md), with [exact approval](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/outcomes/org-01/approval.md). Previous O1/C1 stage decisions and the former selection/handoff checkpoint are historical evidence via immutable Git refs, not the current Product route. The branch remains separate from operational `main`. Engineering and Rancang decisions remain separately owned.


> **Status:** WORKING TRACKER — this refactor branch only; not an operational workflow.
> **Baseline:** `research/harscode-purpose-llm-fit@d972f9c4ec3470b0611da4286629a8659d96ab3d`
> **Blueprint:** [Foundation Refactor Architecture](ARCHITECTURE.md)

Mark items complete only after repository evidence. Do not interpret a checked design activity as a runtime/quality PASS.

## Phase 0 — Isolate and protect authority

- [x] Verify research and operational baseline revisions.
- [x] Create dedicated branch from the verified research HEAD.
- [x] Record immutable Rancang formation pin, project ownership boundary, and historical standing.
- [x] Mark this branch as unfinished and non-operational.
- [x] Confirm final blueprint and archive execution scope with Human before mass moves.

**Exit:** Source history and operational behavior remain intact. No legacy files moved.

## Phase 1 — Define target ownership

- [x] Propose `product/`, `design/`, `engineering/`, `collaboration/`, `harness/`, `deprecated/`.
- [x] Document concern ownership and non-ownership.
- [x] Record Product experience semantics vs Design expression.
- [x] Record Balad advisory vs Human execution vs Engineering Space/Harness authority.
- [x] Record Specialist-local engineering knowledge and allowed intentional redundancy.
- [x] Document legacy dispositions and migration/promotion constraints.
- [x] Human reviews exact blueprint before treating it as the Phase 2 migration contract.

**Exit:** Domain ownership is explicit. Specific subtrees remain demand-driven.

## Phase 2 — Archive legacy and reset navigation

- [x] Verify branch HEAD, pending modifications, source tree completeness, and migration scope.
- [x] Move legacy top-level directories into `deprecated/legacy/`, preserving file contents and lineage.
- [x] Establish `deprecated/README.md` (reference-only; no fallback authority).
- [x] Replace inherited root routing and authoring/navigation where applicable.
- [x] Create only the minimum active domain entrypoints; explicitly mark unbuilt guidance NOT READY.
- [x] Audit moved relative links, pinned SHA references, protected paths, and missing sources.
- [x] Verify the migration diff and checkpoint before further content changes.

**Exit:** Legacy is reference-only; branch is clearly incomplete; no hidden runtime dependency on legacy.

**Verified 2026-10-20:** Archive checkpoint `9f8b6cb898fddce959b812748ebecfcb030efcf7`. All 257 original legacy blobs and 306 non-ignored original tree entries match their archived Git SHA/mode/type. Eleven legacy roots are absent from the active root. All six proposed roots exist (five explicitly NOT READY). Active Markdown: 22 relative links across 10 documents checked, no missing targets. Intra-legacy relative layout preserved; absolute/historical paths are reference-only, not retargeted operational instructions. Operational `main` and the original research branch were unchanged.

## Phase 3 — Rebuild Product

- [x] Reassess product authority formation and sufficiency from actor/value/truth.
- [x] Rebuild experience discovery before commitment selection.
- [x] Rebuild commitments, eligibility, dependency closure and acceptance boundaries.
- [x] Preserve commitment-scoped actor journeys, failure paths and product truth.
- [x] Keep implementation suitability separate from product outcome suitability.
- [x] Run a source-traced C1 semantic stress test (same-session documentation inspection; **not** independent cold-start evidence).
- [x] Perform a source-based integrated Product guidance assessment against Kencleng pilot C1 **and current Kencleng main**; independent reader/use validation and any Product Authority revisit remain separate.

**Validation sequencing decision (2026-10-20):** Complete all foundation domains first; verify together afterward. The earlier isolated C1 cold-read fixture was removed from the active Product area as premature. Its prior revision remains in Git history; later verification may use a fresh protocol.

**Current branch Product catalog:** [Product phases, codes and output types](product/README.md). Historical guidance is linked by immutable SHA in [Product history](product/history.md), not used as the active routing authority.

**Historical C1 source-trace probe — 2026-10-20 (PILOT BRANCH ONLY):** Kencleng `pilot/station5-c1-space-only@91fad854301265357ba69e76182eb5c82ae71049`. **Within this pinned experiment only**, [Product Intent](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/product-intent.md) owns whole-product truth; [Stage 3B](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-3b-commitment-sequencing.md) selects C1; [Stage 4](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-4-c1-interaction-exploration.md) gives supporting actor-experience evidence, not competing Product Authority. [Approved Stage 5 B1–B7](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-5-c1-confirmed-behavior.md) and [Stage 6 XR/ER](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-6-c1-requirements.md) bind C1-specific meaning. The experience anchor preserves start without external proof, pre-effect disclosure, attributable Organization + initial Owner success together, durable inspection, no upgrade of Organization-provided truth, and truthful incomplete/known-conflict paths. Recovery is optional; conflict detection, external legal adjudication, UI form, API, and transaction design were not assumed. The [Rancang interim review](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/project/station5-c1-s1-interim-closeout.md) shows unresolved solution coupling, not an approved product split or implementation. **Outcome:** Historical C1 source consistency probe PASS; independent reader/consumer-fit evidence NOT TESTED. **Do not interpret this pilot branch as current Kencleng `main` authority or MVP scope.** Kencleng `main@e32916b597412094976e3e6263095e861ec18391` owns current product authority through `docs/product/product-overview.md`, current scope through `docs/product/mvp-scope.md`, and sequencing through `docs/product/mvp-delivery-slices.md`. The approved baseline MVP defers full Organization self-service. No Kencleng edits.

## Phase 4 — Rebuild Design

- [x] Separate product experience semantics from interaction/UI/brand expression.
- [x] Curate relevant principles, patterns and evidence governance.
- [x] Review design authority, accessibility and handoff boundaries at source level; independent effectiveness verification deferred.

## Phase 5 — Rebuild Collaboration

- [x] Rebuild Balad as cross-domain Human advisory guidance.
- [x] Preserve Human-direct Space authorization, decision ownership and durable continuity.
- [x] Remove harness-specific launch mechanics from Collaboration; Harness reconstruction pending.
- [ ] Test short-intent, fresh-session advisory behavior in combined post-refactor verification.

## Phase 6 — Rebuild Engineering

- [x] Define Engineering Space capability and formation criteria.
- [x] Reconstruct Rancang as NOT FORMED research candidate; preserve exact historical approval standing.
- [x] Draft candidate Rancang I/O, Specialist-local reasoning, gates and verification responsibility; execution not authorized.
- [x] Place scoped solution-architecture and independent-review knowledge in the Rancang Specialist packages; unneeded legacy technology guidance stays archived.
- [x] Preserve critical security/authorization and truthful evidence obligations in active Engineering contracts.
- [x] Rebuild concern-based production/verification responsibilities instead of copying legacy phase workflow.

## Phase 7 — Rebuild Harness

- [x] Rebuild harness-neutral binding requirements and the Codex adapter as research guidance; vendor-native details are not asserted without live inventory. Other adapters remain demand-driven.
- [x] Separate native permissions, semantic authorizations and Human gates.
- [ ] Validate an actual runtime binding **after foundation reconstruction**, using live tool/model/sandbox evidence; no runtime PASS claimed.

## Phase 8 — Governance and cleanup

- [x] Clarify proportional, concern-owned change control in root AUTHORING.md; no default per-domain proposal systems.
- [x] Check active root/domain routers, 68 relative Markdown links across 29 active documents (no broken targets); independent reader evidence remains Phase 9.
- [x] Confirm no active runtime/authority fallback to archived guidance; historical evidence links remain explicitly non-operative.
- [x] Review active scope/status, remove stale NOT READY claims in active routing, and retain only necessary local safeguard repetition.

**Construction closeout (2026-10-20):** Phase 0–8 source reconstruction is complete **for research evaluation**, not for operational activation. Five domains have working entrypoints; Rancang's reconstructed candidate is NOT FORMED; unused legacy technology guidance remains under `deprecated/` rather than becoming a central library or fictitious Specialist capability. Structural audit: 29 active Markdown docs, 68 internal relative links valid, 257 archived legacy blobs preserved, no outdated version-label branding in active guidance. This is a source-integrity review, **not** a fresh-reader, runtime or effectiveness PASS. Human acceptance/promotion and all actual capability tests remain distinct.

## Phase 9 — Integrated verification, Kencleng revisit, and promotion decision

**Sequencing:** Complete all foundation documentation first. Then separately review cross-domain correctness/authority and fresh-context use. Revisit Kencleng Product Authority with the reconstructed Product guidance **after** refactor evaluation; do not automatically overwrite current approved Kencleng authority. Finally test an authorized bounded Engineering Space/runtime if a suitable assignment exists; promotion to research or `main` is a separate Human decision.

- [ ] Test fresh-session authority reconstruction across Product/Design/Collaboration/Engineering/Harness.
- [x] Source-trace historical pilot C1 through the new Product → Design → Engineering candidate boundaries; no current-MVP or execution approval inferred.
- [ ] Execute an authorized bounded engineering run and verify revisioned output and consumer compatibility.
- [x] Record the source-based integrated audit findings, limits and current Kencleng main/pilot distinction in [FOUNDATION-VERIFICATION.md](FOUNDATION-VERIFICATION.md).
- [ ] Record successes, failures, deviations and unresolved risks.
- [ ] Obtain distinct Human decisions for research baseline replacement and any `main` promotion.

### Kencleng Stage 1 experience-first reconstruction checkpoint — 2026-10-21

**Standing:** Bounded **real-use research evidence**, not a new Harscode standard, Product Authority, fresh-session consumer PASS, or Space/runtime validation.

- **Experiment target:** Kencleng pilot branch `pilot/station5-c1-space-only` (not Kencleng operational `main`). Stage 1 Business / Value Loop reconstructed from pilot Product Intent, with canonical Product Design principles respected within their own concern.
- **Persisted working outcome:** [Anhar-accepted Stage 1 Business Value Story v0.2](https://github.com/anhsbolic/kencleng/blob/7b8b344e2013f5c5389d84d620b70948a3ebfd1f/docs/product/pilot-3-business-value-loop.md). The existing pilot Stage 1 artifact retains historical content and adds a revisioned checkpoint covering human/business **From → To**, meaningful value, three intersecting business-value threads, main actor/responsibility handoffs, truth boundaries, and open questions. It does **not** alter Kencleng `main` authority or supersede C1-specific commitments.
- **Observation:** Current [Product Foundation](product/foundation.md) and [Experiences and Commitments](https://github.com/anhsbolic/harscode-workspace/blob/f763f964cb99b43a65a331860282263f052de96a/product/experiences-and-commitments.md) could support a coherent Stage 1 human-value narrative without turning Product Design principles into unsupported Product Truth. **Stage 1 sufficient for Stage 2 exploration**, as a Human-accepted working pilot reconstruction; not evidence that cross-actor dependency discovery or Stage 3B commitment convergence already succeeds.
- **Decision:** **NO REUSABLE PRODUCT GUIDANCE CHANGE YET.** The proposed *Interconnected Journey Blueprint* is a reversible visualization experiment, not a mandatory artifact or canonical Harscode method. Test actor-specific initial situation → outcome continuity and validated cross-actor dependencies through Stage 2–3 before deciding whether guidance needs targeted revision.
- **Research-format checkpoint (Anhar-approved to persist, 2026-10-21):** [Interconnected Journey Blueprint — Experimental Research v0](https://github.com/anhsbolic/harscode-workspace/blob/f763f964cb99b43a65a331860282263f052de96a/product/interconnected-journey-blueprint-research.md) records the *draft* value anchor, actor initial situation → resulting outcome, meaningful progression, typed cross-actor edges, truth/authority standing, optional commitment frontier, Mermaid illustration and Stage 2–3 validation questions. **Status: EXPERIMENTAL / RESEARCH-ONLY; NOT a reusable Harscode standard or mandatory Product deliverable.** Format and mechanism remain replaceable. No Product guidance policy, Kencleng `main`, or runtime approval changes. Review observed usefulness, confusion and dependency accuracy at subsequent checkpoints.
- **Unverified:** Independent fresh-context consumption, actual Kencleng behavior, downstream Rancang suitability, Engineering Space execution, and runtime.
- **Checkpoint owner:** Harscode Foundation Refactor research; project-specific truth remains in Kencleng. Preserve the Kencleng pilot/main authority boundary.


### Kencleng Stage 2 experience-first reconstruction checkpoint — 2026-10-21

> **Standing:** Accepted **target-project working reconstruction** and Harscode **research evaluation evidence only**. It does not modify Kencleng Product Authority, existing C1 commitments, operational `main`, reusable Harscode guidance or runtime authorization.

- **Source/persistence:** Anhar-approved [Kencleng Pilot #3 Stage 2 actor outcomes reconstruction v0.2](https://github.com/anhsbolic/kencleng/blob/3f972b1cf3edb94c2c41f01b620bb038e2ed922a/docs/product/pilot-3-actor-outcomes.md#12-2026-10-21-experience-first-stage-2-reconstruction-checkpoint), branch `pilot/station5-c1-space-only`; anchored to accepted [Stage 1](https://github.com/anhsbolic/kencleng/blob/7b8b344e2013f5c5389d84d620b70948a3ebfd1f/docs/product/pilot-3-business-value-loop.md). The new Stage 2 checkpoint is appended to the prior historical actor-outcomes artifact rather than rewriting past approvals.
- **Scope actually explored:** Public Visitor `FROM → TO` and information-seeking/non-donation; Organization Representative including Owner vs Staff and distinct entry situations; Reviewer as bounded independent judgment for Organization review, Campaign curation and fund-usage verification; Donatur post-donation continuing understanding and Organization accountability; Platform Operator deliberately bounded/open; Kencleng/System as truth/state obligation rather than human actor. Typed candidate edges: information/state/authority prerequisite, conditional judgment, downstream accountability, conditional role transition.
- **Observed analytical benefit:** Smaller actor-centric fragments plus typed cross-actor edges made it easier in this same-session analysis to **spot and communicate risks of false universal prerequisites** (e.g., Reviewer as mandatory public-understanding gate; entire Organization establishment as necessary for every Visitor outcome; closure ending accountability), while keeping value continuous from Stage 1. **This is a representation/clarity observation, not evidence of improved commitment selection or runtime correctness.** Much of the underlying semantic discipline already existed in the historical pilot Stage 2.
- **Method checkpoint decision:** **NO REUSABLE PRODUCT GUIDANCE CHANGE YET.** Retain [Interconnected Journey Blueprint — Experimental Research v0](https://github.com/anhsbolic/harscode-workspace/blob/f763f964cb99b43a65a331860282263f052de96a/product/interconnected-journey-blueprint-research.md) as optional and replaceable; Stage 3 should test actual prerequisite/conditional/downstream connections, exception paths, and coherent commitment selection before recommending any method revision.
- **Not established:** Real user research, independent cold-read comprehension, engineering/Design consumer fit, Rancang convergence, actual Kencleng behavior, or Harscode Engineering Space/runtime execution. No new positive Platform Operator workflow, mandatory reporting cadence, universal review gate or full-journey diagram requirement is established.
- **Authority distinction:** This is evidence from Kencleng's **historical pilot branch**, not current Kencleng `main` Product Authority or MVP authorization. Harscode `refactor/harscode-foundation` remains research-only, with Harscode `main` operational baseline unchanged.


### Kencleng Stage 3A experience-first reconstruction checkpoint — 2026-10-21

> **Standing:** **Anhar-approved Kencleng pilot working-reconstruction checkpoint**, used as Harscode **research evidence only**. No approved reusable Harscode method, operational promotion, Kencleng Product Authority change, engineering assignment, or runtime PASS.

- **Durable source:** [Kencleng Pilot #3 Stage 3A reconstruction + final light audit](https://github.com/anhsbolic/kencleng/blob/8b54e4c8327673a466e6cf8ed132257bf8e583f3/docs/product/pilot-3-stage-3a-representative-scenarios.md#13-2026-10-21-experience-first-stage-3a-reconstruction-checkpoint), commit `8b54e4c8327673a466e6cf8ed132257bf8e583f3` on `pilot/station5-c1-space-only`, grounded in Anhar-accepted Stage 1–2 checkpoints. Historical Stage 3A findings and scoped C1/Stage 3B approvals were preserved, not replaced.
- **Bounded exercise:** Tested cross-actor handoffs R1↔R2 (Organization authority/review vs Campaign), R2↔R3 (public visibility vs donation eligibility), R3↔R4 (donation fact/funding/continuing understanding), direct R2↔R4 (Campaign accountability without Donatur), plus X1 privileged-operator boundary. Final audit judged R1–R4 + X1 **semantically sufficient for Stage 3B exploration**, not proof of delivered behavior or commitment eligibility.
- **Specific safeguards:** (1) R4 follows Campaign/fundraising state even with zero Donatur; (2) simulated money/operational results must not be represented as real external settlement or impact; (3) historical C1's Anhar-approved *internal Kencleng Owner* semantics remain scoped evidence while **current commitment relevance/priority are open**. No C1 cancellation/selection, R5, universal Reviewer approval gate, mandated Staff/Owner flow, or fabricated Platform Operator power was introduced.
- **Method evaluation:** Typed state/outcome edges and scoped actor fragments helped **make explicit** true prerequisites versus conditional judgments and downstream accountability, and prevented easy misreading as a linear delivery pipeline. Most of those product-semantic distinctions **were already recognized in historical Stage 3A**; the evidence is primarily a representation/analysis benefit, **not** independently demonstrated superiority in commitment selection, efficiency, fresh-reader comprehension or downstream Design/Rancang use.
- **Decision:** **NO REUSABLE PRODUCT GUIDANCE CHANGE YET.** [Interconnected Journey Blueprint Research v0](https://github.com/anhsbolic/harscode-workspace/blob/f763f964cb99b43a65a331860282263f052de96a/product/interconnected-journey-blueprint-research.md) remains experimental, optional and replaceable. Stage 3B will generate *fresh meaningful outcome candidates* from the connected value story, test genuine product prerequisites and boundedness, and **then** compare with historical C1/C2/C3, without presuming C1 is current first choice or invalid.
- **Unverified:** Actual Kencleng runtime and user behavior, independent cold start, consumer/Rancang compatibility, Harscode Engineering Space execution and operational usefulness. Kencleng `main` remains untouched by this pilot checkpoint; Harscode `main` remains operational and untouched by this research branch.


### Kencleng Interconnected Journeys Level 2 official research checkpoint — 2026-10-21

> **Standing:** **Anhar-approved Product research checkpoint in Kencleng pilot**; official **Harscode research evidence checkpoint** on this refactor branch. **Not** reusable Harscode methodology approval, Kencleng `main` Product Authority change, Engineering assignment or operational promotion.

- **Owning artifacts:** [Kencleng new `docs/product/interconnected-journeys/` checkpoint](https://github.com/anhsbolic/kencleng/blob/00ccf35d4f2cbec29721a6390a29804e50675760/docs/product/interconnected-journeys/README.md) and [Level 2 v0.2 map](https://github.com/anhsbolic/kencleng/blob/00ccf35d4f2cbec29721a6390a29804e50675760/docs/product/interconnected-journeys/level-2-network.md) at Kencleng pilot revision `00ccf35d4f2cbec29721a6390a29804e50675760`. Approved in-session by Anhar on 2026-10-21. Existing Stage 1–3A files, C1-specific approvals and both projects' `main` baselines remain unchanged.
- **Accepted working model:** **Level 1 Journey Landscape** (R1–R4, X1 exception overlay) plus **Level 2 Interconnected Meaningful Transitions** (26 scoped nodes; typed prerequisites/conditionals/downstream/feedback; negative and uncertainty paths). Meaningful consequence—not feature, screen or CRUD—determines node resolution. Initial 19-node version was audited and corrected before acceptance.
- **Specific research evidence:** More explicit handling of Organization review, Campaign curation revision, separate publication/eligibility, donation attempt/fact versus funding/settlement, changing states, reporting through Campaign lifecycle without Donatur, and bounded verification. Many distinctions already existed historically; representational completeness is observed, **sequencing improvement is not proven**. The informal 39-edge/connected-component check is not semantic proof.
- **Changed working experiment boundary:** Hold mandatory **Commitment-based Stage 3B** for this research continuation; examine direct interconnected-journey-derived starting-point reasoning and future Rancang-input sufficiency instead. This is **not** cancellation of historical C1, replacement of reusable Harscode guidance, or acceptance of an alternative stage model. [Harscode Blueprint research addendum](https://github.com/anhsbolic/harscode-workspace/blob/f763f964cb99b43a65a331860282263f052de96a/product/interconnected-journey-blueprint-research.md) owns detailed evaluation posture.
- **Next:** **Stop and discuss starting-point selection** from Level 2 before any additional Product-to-Engineering method design. **Engineering readiness, local environment and horizontal technical dependencies explicitly remain on hold**; no Rancang invocation or delivery sequence has been authorized. No independent consumer/runtime effectiveness PASS.

### Independent Product route / historical contamination audit — 2026-10-22

- **Kencleng current entrypoint:** [`docs/product/README.md`](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/README.md) routes fresh Product work to [Level 2](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/interconnected-journeys/level-2-network.md) and [current selection/handoff working decisions](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/interconnected-journeys/selection-and-handoff-research.md). Dated pilot artifacts were **labeled as history**, not deleted.
- **Material correction:** Level 2's O1 **may not automatically inherit** a historical initial-Owner grant model, coupled-success rule, or conflict policy. Product Intent does not alone decide those details; they are OPEN for fresh Product elaboration. O1 is a recommended research candidate, not delivery approval. Former O1 PRD specimen derived from historical requirement lists is invalid for Product Output Contract conformance claims and effective Rancang I1.
- **Scope / consumer boundary:** Product Output Contract v0.1 approved as working research by Anhar; self-contained Product semantics are producer-owned. Rancang black-box input-definition revision and any formation/runtime work need separate approval. No generic Harscode Product-guidance or `main` promotion; no new Product Space or Balad next-node capability.
- **Historical audit references:** Prior 2026-10-20/21 source-trace results and old checklist entries remain factual *historical evaluations*, not instructions to restart historical commitment selection or reuse its requirements.
- **Not proven:** Fresh-session independent O1 Product output, Rancang consumer conformance, Engineering Space readiness, real behavior, and runtime verification.

**Global gate:** Never equate documentation completeness, formation approval, or clean directory structure with runtime correctness.
