# Cross-Stage Foundation — Sequential Audit & Revision Plan / Tracker

> **Status:** PLAN AGREED; A1 experiment-led reassessment and approved research guidance persisted; A1 SETTLED_FOR_RESEARCH after source-level validation; A2–A6 NOT_STARTED.
> **Decision owner:** Anhar. **Plan agreed:** 2026-11-04. **Tracking owner:** research collaboration; record actual approvals and evidence, do not infer them.
> **Repository:** `anhsbolic/harscode-workspace`.
> **Frozen subject baseline:** `refactor/harscode-foundation@96b479c1a4e1ead77bb1614ef49bf09aca435c0d`.
> **Only write branch:** `research/cross-stage-mapping`, created from that exact checkpoint.
> **Explicit boundary:** **Do not audit, edit, merge into, or propose changes against `main` in this program. Do not modify `refactor/harscode-foundation`.** This program addresses Harscode foundation only; Kencleng Product Output/Outcome audit is a separate future episode.

## 1. Objective and reference

Audit and reconcile Harscode foundation **one concern at a time, starting with Product**, using the existing experiment as a *challengable candidate*, not a predetermined replacement. Identify material semantic, authority, input/process/output/outcome, consumer, and evidence gaps; **keep, clarify, revise, replace, or remove** only where justified. Revisions are made solely in this research branch after relevant Human agreement. Do not add an orchestration/workflow engine or Space just to match phase labels.

**Working references:**
- [Candidate Reference Model](candidate-reference-model.md) — five logical concerns, information/authority boundaries and ORG-01 illustrative scenario.
- [Five-stage Input–Source Mapping](input-source-mapping.md) — 60 candidate inputs; sources are not automatically verified or binding.
- [Foundation Gap Assessment — First Pass](foundation-gap-assessment.md) — checkpoint-wide tree inventory and **candidate** findings F-01..F-06; not a completed phase-by-phase audit.
- [Product working snapshot](product-definition.md), [UX Lo-Fi](ux-design-lofi.md), [UI Hi-Fi](ui-design-hifi.md), [Rancang](rancang-engineering-solution.md), [Builder](engineering-builder.md) — detailed phase-specific audit hypotheses.

**Evidence order:** current owning repository sources and exact approvals → explicitly agreed working decisions → historical context → memory. Source baseline above is frozen for audit reproducibility; each revision must be assessed at the latest actual research-branch commit and reported as a delta. Original formation approvals on immutable revisions **do not transfer** to changed definitions.

## 2. Method — complete one concern before the next

For each sequential audit **unit**:

1. **Understand & inventory.** Read the relevant actual Harscode guidance, routing, Spaces/Agents (if applicable), I/O contracts, templates, approval/formation records, output/evidence requirements and their version standing. Inspect related project-level source-consumption rules. Do not blindly read every historical file.
2. **Verify & challenge.** Map actual semantics to candidate **Input → Process → Output → Outcome**, source provenance, authority/owner, Human gates and intended consumers. Challenge candidate assumptions too. Distinguish a missing explicit contract from merely different packaging/granularity.
3. **Gap assessment.** For each consequential issue record: exact source path/ref; current behavior and evidence; candidate expectation; actual consequence; classification (`KEEP`, `CLARIFY`, `REVISE`, `REPLACE`, `REMOVE`, or `UNPROVEN`); affected consumer; risk/priority; smallest sufficient recommendation. Note security/privacy blast radius, reversibility and fallback where material.
4. **Decision gate.** Share material findings and a concrete recommended change set with Anhar. **Do not change owning guidance or formed Space definitions before approval.** Small independently reversible edits may be bundled under a scoped approval; binding semantics, role/authority boundary, security, formation, Human gates, protected execution and externally consumed contracts require explicit scope/revision review.
5. **Execute approved revision.** Change only approved owning paths on `research/cross-stage-mapping`. Prefer minimal corrections; avoid redundant new phases/files, cloned source authority, invented project facts, or automatic canonicalization.
6. **Validate & close unit.** Review diff and references; recheck input–source and logical-output consistency; verify standing/approval and known consumer boundaries; record what was actually inspected/tested, residual issues and exact commit(s). Source review cannot be labeled runtime validation.
7. **Advance.** Proceed to the next audit unit after the prior unit is *sufficiently settled for downstream comparison*. Cross-cutting concerns are revisited only for materially new evidence; do not re-open decisions to make a linear process look neat.

**Important:** The sequence below is **audit/revision order**, not a required execution dependency, mandatory waterfall or runtime Space invocation order. Rancang and Hi-Fi may consume parallel sufficient inputs in actual projects. Multiple source producers may feed one consumer directly.

## 3. Sequential audit and revision worklist

| ID | Audit unit (order) | Primary source surface at frozen baseline | Key tests / exit question | Initial state |
| --- | --- | --- | --- | --- |
| **A1** | **Product** | `product/` (11 files: catalog, AGENTS, foundation, journey mapping, outcome selection/definition, review/approval, handoff, history and two Contract templates) | Does current Product guidance produce sufficient actor/value/journey/selected outcome, **Actor vs Domain Role**, consequential **Content & Information Requirements**, Product Contract, scoped approval and consumer handoff? Are six named subphases useful navigation or harmful fragmentation? | `NOT_STARTED` |
| **A2** | **UX Design — Lo-Fi** | `design/` (shared four-file baseline) plus Product accepted research result and relevant engineering interface constraints | Does Design explicitly own UX flow, IA, navigation/**Webpage Map & Route Specification**, wireframes, interaction states and scoped review? Are inputs discoverable without mandatory new files/Space? | `NOT_STARTED` |
| **A3** | **UI Design — Hi-Fi** | Same `design/` shared surface; any A2-approved research changes; project-level visual/asset rule consumption patterns | Are Lo-Fi outputs (especially webpage path contract), content meaning, responsive/accessibility, visual states, final UI/asset/copy, quality criteria and acceptance/handoff adequately represented? No forced visual artifact where irrelevant. | `NOT_STARTED` |
| **A4** | **Rancang — Engineering Solution** | `engineering/spaces/feature-solution-design/` (23 files, including contracts, six-Agent guidance and historical exact formation records), shared Engineering rules | Does Rancang consume material accepted Product/Design UX contracts while owning only architecture/auth/API/data/state/security/verification decisions? Check O1–O5 semantic coverage, O3 boundary, revision/consumer-fit and formation approvals. **Do not overwrite old accepted definition by implication.** | `NOT_STARTED` |
| **A5** | **Engineering — Builder** | `engineering/spaces/nextjs-builder/` (23 files) and `engineering/production-and-verification.md`; relevant project/harness guards | Evaluate the actual **Next.js frontend-only** capability against relevant information/output needs, project authority, design state, API modes, verification and handoff. Separately identify missing backend/integration ownership for *end-to-end* outcomes; do not assume a new full-stack Space is required. | `NOT_STARTED` |
| **A6** | **Cross-stage coherence & foundation closure review** | Outputs of A1–A5; `ARCHITECTURE.md`, `AGENTS.md`, `AUTHORING.md`, `README.md`, `REFACTOR-CHECKLIST.md`, `collaboration/`, `harness/` and applicable shared Engineering guidance | Validate consumer edges, ownership, source authority, exact approval standing, no contradictory guidance/routing, security and durable-state boundaries. Explicitly record excluded runtime/consumer checks and whether a new research candidate is internally coherent. | `NOT_STARTED` |

**Inventory note:** First-pass source inventory found 349 files: **84 active foundation**, **7 initial experiment**, **258 deprecated/history**. That first pass is **not** a completed audit of A1–A6. Historical files remain non-authoritative evidence and may be inspected only if a specific gap needs their provenance. The working branch may gain files, so these counts are frozen checkpoint counts, not a live dynamic denominator.

**Cross-cutting context:** `collaboration/`, `harness/`, project-standard precedence, formation/authorization and common navigation are checked when relevant to each unit, then reconciled in A6; they are not silently ignored or treated as new product stages. Current approved Space definitions continue to have their original exact-revision standing until separately reviewed.

## 4. Exit criteria for each audit unit

A unit can be marked `SETTLED_FOR_RESEARCH` only when:
- [ ] Relevant owning sources and approvals are inspected at stated exact refs (or explicit limitations are recorded).
- [ ] Actual vs candidate **Input, Process, Output, Outcome** and downstream consumers are compared with evidence; `UNPROVEN` remains possible.
- [ ] Material ownership/security/authority and consumer compatibility gaps have a disposition and named decision owner.
- [ ] Anhar has decided consequential changes, including a conscious `KEEP` / `DEFER` decision when justified; prior approvals are not impersonated.
- [ ] Any approved edit is committed **only** to the research branch and its scope/diff/links are checked.
- [ ] Residual risk, unknowns and verification limitations are recorded; later stage assumptions are not asserted as runtime facts.

When audit finds **no needed revision**, record `KEEP` with evidence and close the unit without creating new guidance. If critical external facts are missing, record `HELD` with a precise unblock condition. Research sign-off is not Product/Design authority for Kencleng, formed Space re-approval, invocation authorization or operational promotion.

## 5. Progress tracker (current)

Statuses: `NOT_STARTED` → `AUDITING` → `REVIEW_PENDING` → (`REVISING` if authorized) → `VALIDATING` → `SETTLED_FOR_RESEARCH`. `HELD` may interrupt any stage. These are **documentation labels only**, not a Harscode execution state machine.

| Unit | Status | Audit evidence / issue refs | Decision / approval refs | Research revisions / verification | Next item |
| --- | --- | --- | --- | --- | --- |
| **Setup** | **COMPLETE** | [Candidate Reference Model](candidate-reference-model.md), [First-Pass Gap Assessment](foundation-gap-assessment.md) | Anhar agreed sequential audit-and-revision method, 2026-11-04 | New isolated branch; plan/tracker created here | Start A1 |
| **A1 Product** | `SETTLED_FOR_RESEARCH` | A1 v2 reviewed original 11 Product files; new 13/9/6/6 core; 99-file active/research legacy-reference scan and source-level link/semantic checks | Anhar accepted new guidance architecture and three research authoring templates (2026-11-04); approved template blobs pinned at `f796b2d` | Research branch redesign, seven retired files, immutable history, 110 relative links checked in 14 affected/relevant files; two historical broken references repaired; target-project independent consumer fit **UNVERIFIED** | Start A2 UX Lo-Fi research, using information/responsibility contracts; preserve A1 limitations for A6 |
| **A2 UX Lo-Fi** | `REVIEW_PENDING` | [A2 audit + reviewed architecture](a2-ux-lofi-deep-audit-and-target-design.md): 8 source-based findings, 11/9/9/6 semantic model | Anhar approved three independent direct Design concern folders and root routing retirement (2026-11-04); specific UX guidance content **NOT YET APPROVED** | Four `design/ux/` DRAFTs persisted at `32c243c`; root Design README/AGENTS removed, historical links pinned; source validation pending; independent UX/consumer/harness runtime UNVERIFIED | Review UX semantics and validate scoped source links before A2 settlement |
| **A3 UI Hi-Fi** | `NOT_STARTED` | F-01 candidate only | None | None | After A2 adequately settled |
| **A4 Rancang** | `NOT_STARTED` | F-03/F-05 candidate only | None | None | After A3 adequately settled |
| **A5 Builder** | `NOT_STARTED` | F-04/F-05 candidate only | None | None | After A4 adequately settled |
| **A6 Final coherence** | `NOT_STARTED` | F-06 candidate only; revisit all accepted changes | None | None | After A1–A5 |

**Progress accounting:** `1 / 6` audit units **SETTLED_FOR_RESEARCH** (A1). Setup is complete, not a seventh audit. Research closure does not prove independent consumer fit, project Product authority, actual use, or runtime.

## 6. Findings and decision log — append only when real evidence exists

Keep short per-item records here or link to specific unit assessment/commits **only when necessary**. Do not create a separate ticket, register or directory just to fill a template.

| Date / unit | Finding ID / exact source | Severity / observed consequence | Recommendation and ownership | Human decision / scope | Evidence / commit / residual |
| --- | --- | --- | --- | --- | --- |
| 2026-11-04 / setup | Initial F-01..F-06 in [first pass](foundation-gap-assessment.md) | **Candidate findings**, not individually validated by a sequential audit | Inspect relevant owning sources at A1–A6; no implicit adoption | Sequential method and isolated research branch agreed; no per-phase edits approved yet | Baseline `96b479c1`; reference model and first-pass report already persisted |

## 7. Stop conditions / change control

- **Do not touch or audit `main`, or change `refactor/harscode-foundation`.** If the source branch moves, continue using frozen baseline until Anhar explicitly revises scope.
- **Do not change owning Product/Design/Engineering/Harness guidance in the setup step.** For later changes, bring bounded evidence-backed proposal before editing.
- An exact **Engineering Space formation approval** belongs only to its pinned definition revision. A revised Space definition on this research branch requires new explicit Human review/approval before any `FORMATION APPROVED` claim; do not erase original approval/history.
- No silent change to target-project Product, Design, API, Engineering standards or Kencleng implementation. This program has no permission to invoke Spaces, execute protected project changes, or deploy.
- Re-check high-impact security/privacy/authority changes more strictly, with bounded rollback/fallback. Do not weaken safeguards to simplify the audit. Do not promote research standing to canonical operational policy.
- A separate **Kencleng Product Output/Outcome audit** can be planned after Harscode research assessment, under fresh explicit scope; it is **not** an implicit seventh unit of this tracker.

## Next executable unit

**A2 — REVIEW_PENDING.** [A2 research audit and proposed Interaction & Experience Definition](a2-ux-lofi-deep-audit-and-target-design.md) is ready for Anhar's decision; do not edit owning Design/Engineering Space definitions until the material target direction is approved. A1 remains SETTLED_FOR_RESEARCH (1/6).

## 8. A1 v2 — persisted redesign checkpoint (2026-11-04)

Anhar explicitly shifted A1 to **experiment-led fundamental reassessment**, without preservation bias toward the prior six-phase layout or historical ORG-01. The experiment remains challengeable, not canonical. A1 v2 evaluated all 11 Product files and approved a new **4-guidance / 3-optional-template design**, where Product Definition is one concern with 13 information inputs, nine iterative activities, six logical outputs and six quality properties. Dependency direction is **required information and functional responsibility (what), not named Space/Agent (who)**.

**Persisted guidance:** `product/README.md`, `product/AGENTS.md`, `product/product-definition.md`, `product/authority-and-approval.md`, `product/consumer-handoff.md`. **Templates (Human-accepted research authoring shapes at reviewed revision `f796b2d`; unchanged preapproval headers):** `product/templates/product-definition.id.md`, `product/templates/product-contract.id.md`, `product/templates/product-approval-record.id.md`. The former six phase files and English legacy template were retired from this research branch, with frozen original revisions recoverable via Git and source-linked first-pass audit evidence; no operational or target-project authority changed. New Product research guidance is **not** operational policy and does not amend approved Engineering Space definitions.

**Evidence limitations:** This is approved working research design and source-level migration, not a validated target-project Product process, Kencleng ORG-01 reapproval, independent fresh consumer test or runtime verification. Old files were retired and pinned to immutable sources. External consumers remain UNVERIFIED and are owned by the applicable target-project Human for any actual adoption; cross-concern coherence will be reviewed in A6.

**A1 template decision evidence (2026-11-04):** Anhar approved three research authoring templates at reviewed commit `f796b2d889168d708a49b42102947fcd59a1c156`: `product/templates/product-definition.id.md` blob `8f40b3cc2929e643f498c2a463e7f55c0e425e8c`; `product/templates/product-contract.id.md` blob `dcd5dc4505676c60aee29513e64ca3d4f64a5e65`; `product/templates/product-approval-record.id.md` blob `a34918b7ddf81c6706fcedf35d3b70a0ad3294c8`. These template bytes remain unchanged with their originally written DRAFT headers; this decision accepts the **research authoring shapes**, not target-project contracts, product decisions, or operational Harscode policy. Approval record external to template content avoids self-referential approval edits.

## 9. A1 — Source-level validation and research closure (2026-11-04)

**Human authority:** Anhar explicitly approved the experiment-led Product document architecture and core/authority/handoff drafts, then approved the three research templates at exact reviewed revision `f796b2d889168d708a49b42102947fcd59a1c156`. This approves the **research authoring formats**, not target-project Product requirements, formed capabilities or operational Harscode policy. Their unchanged template blobs and original DRAFT headers are reconciled through this separate approval evidence, not edited postapproval.

**Verified source steps:**
1. Audited all **11** pre-redesign Product files at research baseline and compared to ORG-01 experimental Product Definition as a primary but challengeable design reference. New Product core covers **13 information inputs, 9 iterative process activities, 6 logical outputs, 6 Product quality properties**, including actor/domain-role separation, consequential information obligations and subject-independent consumers.
2. Scanned **99 active/research files** in the pre-cleanup research tree for links/codes referring to legacy six-phase Product paths. Engineering Spaces had **no direct path dependency on the seven retired files** in the scanned sources. No broad Engineering formation/contract changes were made.
3. Retired six obsolete phase/template files plus legacy English Contract template (**7 total**) only on `research/cross-stage-mapping`. Preserved exact frozen originals at `96b479c1a4e1ead77bb1614ef49bf09aca435c0d`; directly fetched and verified all seven original blobs. Original first-pass assessment cites historical frozen sources, not the new Product file in their place.
4. Checked **110 local relative Markdown links across 14 A1-affected and nearby reference documents** after retirement. Identified two pre-existing broken historical Specialist links in `FOUNDATION-VERIFICATION.md`; verified original source bytes exist at `5e3beb74e4c1231993924cd39a2df47654eab59a` and pinned those links in this closure commit. Repeat changed-document link check after commit.
5. Verified the three unchanged template blob hashes agree with Anhar's approved research versions. Approval Record and Contract remain separate; Product Contract self-contained meaning does not waive original-source checks, security constraints, or downstream authorization.

**Residuals / dispositions:** Real target-project Product adoption, external references to old `PROD-*` codes, independent fresh-session Product→Design/Engineering consumption, and actual ORG-01/Product value are **NOT CHECKED / UNPROVEN**, not silently treated as PASSED. Any target-project adoption/redefinition needs separate authorized owner review (Anhar where applicable) and exact artifact revisions. A2/A4/A6 may reveal material new evidence warranting A1 reconsideration; do not reopen only for naming alignment.

**A1 status:** `SETTLED_FOR_RESEARCH` after repository-local evidence and Human research design approvals; this **does not** imply operational promotion, real consumer-fit acceptance, runtime execution or a new Product Space.

**Post-A1 documentation simplification (2026-11-04):** On Anhar's explicit direction, the standalone Product legacy-history index was removed and active Product navigation no longer surfaces legacy source material. Original Product files remain recoverable through immutable Git revisions; exact references needed for the historical audit stay in the evidence-bearing audit documents. This is a documentation/routing cleanup, **not** reopening A1, deleting Git history, changing approved template bytes or promoting research to operational policy.

## 10. A2 UX Lo-Fi — audit draft for Human decision (2026-11-04)

[A2 experiment-led deep audit and proposed target model](a2-ux-lofi-deep-audit-and-target-design.md) records complete source inspection of the four existing Design files, target information model, consumer/authority boundaries, evidence-supported findings A2-F01–F08, and a proposed concern-level redesign. Its standing is **DRAFT / REVIEW_PENDING**, **not an approved Design contract**. Owning `design/` files remain unchanged in this step, and no new Space/Agent/authorization is inferred. Human review must decide material A2 direction before research Design edits. Independent Design/project consumption, UX usability and runtime remain UNVERIFIED.

**A2 updated research finding (2026-11-04):** Anhar proposed separate `design/ux/`, `design/ui/`, and `design/project-standard/` concern directories. The [A2 research proposal](a2-ux-lofi-deep-audit-and-target-design.md) was revised after **read-only** evidence inspection of Kencleng pilot `docs/design/` at `d6738298f43313d8c58afcec7b5131b33e0b26d0` and non-authoritative historical Harscode Design exploration. Project reusable Design standards, working IA/copy heuristics, direction evidence and outcome-specific candidate handoff have different standing. **No approved three-concern Harscode architecture yet; A2 REVIEW_PENDING.**

**A2 direct-entrypoint clarification (2026-11-04):** Anhar requested each proposed `design/ux/`, `design/ui/` and `design/project-standard/` folder own its `README.md`, `AGENTS.md`, `definition.md` and `authority-and-handoff.md`. Shared `design/`-level routing/authority as an agent prerequisite is rejected as the proposed target. Migration must reconcile ancestor `AGENTS.md` load behavior and inbound root Design links; **A2 proposal revised, not approved/persisted to owning Design paths**.

**A2 UX direct-entrypoint draft checkpoint (2026-11-04):** Following Anhar's structural approval, four proposed UX files were persisted at `32c243c36239932f94f43dba5b0d88555161d164`. The shared parent `design/README.md` and `design/AGENTS.md` were subsequently retired, with root navigation now pointing directly to `design/ux/README.md`. First-pass audit citations refer to their immutable inspected revisions. Root `design/exploration.md` and `design/authority-and-handoff.md` remain transition-only sources for A3, not extra UX dependency. **A2 content remains REVIEW_PENDING**, with no independent actor-agent harness run, user usability proof, or project Design authority amendment.
