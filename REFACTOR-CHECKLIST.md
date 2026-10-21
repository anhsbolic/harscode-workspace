# Harscode Foundation Refactor — Checklist

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

**Candidate guidance (WORKING / RESEARCH-ONLY):** [Product entrypoint](product/README.md), [foundation](product/foundation.md), [experiences and commitments](product/experiences-and-commitments.md), [handoff](product/handoff.md).

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
- **Observation:** Current [Product Foundation](product/foundation.md) and [Experiences and Commitments](product/experiences-and-commitments.md) could support a coherent Stage 1 human-value narrative without turning Product Design principles into unsupported Product Truth. **Stage 1 sufficient for Stage 2 exploration**, as a Human-accepted working pilot reconstruction; not evidence that cross-actor dependency discovery or Stage 3B commitment convergence already succeeds.
- **Decision:** **NO REUSABLE PRODUCT GUIDANCE CHANGE YET.** The proposed *Interconnected Journey Blueprint* is a reversible visualization experiment, not a mandatory artifact or canonical Harscode method. Test actor-specific initial situation → outcome continuity and validated cross-actor dependencies through Stage 2–3 before deciding whether guidance needs targeted revision.
- **Research-format checkpoint (Anhar-approved to persist, 2026-10-21):** [Interconnected Journey Blueprint — Experimental Research v0](product/interconnected-journey-blueprint-research.md) records the *draft* value anchor, actor initial situation → resulting outcome, meaningful progression, typed cross-actor edges, truth/authority standing, optional commitment frontier, Mermaid illustration and Stage 2–3 validation questions. **Status: EXPERIMENTAL / RESEARCH-ONLY; NOT a reusable Harscode standard or mandatory Product deliverable.** Format and mechanism remain replaceable. No Product guidance policy, Kencleng `main`, or runtime approval changes. Review observed usefulness, confusion and dependency accuracy at subsequent checkpoints.
- **Unverified:** Independent fresh-context consumption, actual Kencleng behavior, downstream Rancang suitability, Engineering Space execution, and runtime.
- **Checkpoint owner:** Harscode Foundation Refactor research; project-specific truth remains in Kencleng. Preserve the Kencleng pilot/main authority boundary.

**Global gate:** Never equate documentation completeness, formation approval, or clean directory structure with runtime correctness.
