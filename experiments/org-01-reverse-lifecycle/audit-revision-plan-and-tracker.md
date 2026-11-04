# Cross-Stage Foundation — Sequential Audit & Revision Plan / Tracker

> **Status:** PLAN AGREED; A1–A2 SETTLED_FOR_RESEARCH after source-level validation; A3 REVIEW_PENDING with evidence-based research proposal; A4–A6 NOT_STARTED.
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
| **A2 UX Lo-Fi** | `SETTLED_FOR_RESEARCH` | A2 source-level 11/9/9/6; new/material UX O2 Flow Diagram and O6 Lo-Fi required-by-default, evidence-backed exceptions; exact amendment at `8d53c1a` | Anhar explicitly **approved exact research revision `8d53c1a`** (2026-11-04), including scoped UX guidance/template amendment; content blobs recorded in section 16 | Approved exact UX artifact blobs preserved; no actual independent UI consumer, browser, usability or runtime validation implied | Reopen only with materially new evidence or actual consumer incompatibility |
| **A3 UI Hi-Fi** | `REVIEW_PENDING` (guidance accepted; templates drafted) | [A3 source audit](a3-ui-and-project-standard-deep-audit-and-target-design.md), [13-input UI compatibility](a3-ui-input-to-ux-output-compatibility.md); four accepted UI guidance files; ID/EN authoring template proposals | Anhar explicitly approved the four UI guidance drafts from `2fe4c72` on 2026-11-04; newly authored UI templates **not yet approved** | Original approved UI blobs pinned in section 17; ID/EN templates + navigation-only UI README update; source/parity check pending, runtime/independent consumer UNVERIFIED | Review standardized UI output templates; keep Project Standard out of scope |
| **A4 Rancang** | `NOT_STARTED` | F-03/F-05 candidate only | None | None | After A3 adequately settled |
| **A5 Builder** | `NOT_STARTED` | F-04/F-05 candidate only | None | None | After A4 adequately settled |
| **A6 Final coherence** | `NOT_STARTED` | F-06 candidate only; revisit all accepted changes | None | None | After A1–A5 |

**Progress accounting:** `2 / 6` audit units **SETTLED_FOR_RESEARCH** (A1 Product, A2 UX). Setup is complete, not a seventh audit. Research closure does not prove independent consumer fit, project Product/Design authority, actual use, or runtime.

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

**A3 UI CONTENT REVIEW — REVIEW_PENDING.** Four self-contained `design/ui/` research guidance drafts now exist under the [direct UI entrypoint](../../design/ui/README.md), based on [13-input compatibility mapping](a3-ui-input-to-ux-output-compatibility.md) and [A3 source audit](a3-ui-and-project-standard-deep-audit-and-target-design.md). Anhar approved A2 exact scoped revision `8d53c1a` and requested UI drafting, **not automatic acceptance of the new UI semantic bytes**. A1 and A2 remain SETTLED_FOR_RESEARCH (2/6). Project Standard concern will be addressed separately.

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

**A2 UX standardized output proposal (2026-11-04):** In response to Anhar's request for a consistent output authoring artifact, one optional `design/ux/templates/ux-output.id.md` was added as a **DRAFT FOR HUMAN REVIEW**. It organizes applicable O1–O9 logical information and UX decision/consumer standing in one bounded vehicle; it does not impose nine files, mandatory Lo-Fi work, a new UX Space, automatic Product/Design authority, or a second approval system. Existing sufficient target-project formats are acceptable. Root UX README/AGENTS direct routing updated; A2 remains REVIEW_PENDING until Anhar accepts substantive content and research validation completes.

## 11. A2 UX guidance and Indonesian output template acceptance (2026-11-04)

**Human decision:** Anhar explicitly approved the four owning UX research guidance files and the optional **Indonesian** UX output authoring template after reviewing branch revision `1658b5dad08e3f7b95c8bb8ccfbd3d67367a5c51`. This is **acceptance of the reusable Harscode UX research design and Indonesian authoring shape**, not Product/UX approval in Kencleng, actual UX consumer fitness, a formed Design Space, or operational Harscode promotion. Exact reviewed files/blobs:

| Reviewed research guidance/template | Approved content blob at `1658b5d` |
| --- | --- |
| `design/ux/README.md` | `98146c6f58331dd41350fdbbad894aea6f27c2f2` |
| `design/ux/AGENTS.md` | `ed71e825707df7417d07d5967d7f144e5162feed` |
| `design/ux/definition.md` | `e6295602331bcdfe88e9f2693f85ecb63bdb924c` |
| `design/ux/authority-and-handoff.md` | `f06cd62969d1eab09cd972a9d88c4b0b027046c2` |
| `design/ux/templates/ux-output.id.md` | `82c7e670d386142993f6588d096cdc0bbb8c67ec` |

No approved UX meaning or ID template was changed to insert an approval status/hash, so original DRAFT headers remain part of immutable reviewed bytes. The README is subsequently changed **only for discoverability of the newly requested English template**; this does not silently create a new substantive approval of different bytes. Verify source semantic equivalence before A2 closure.

**English-language request:** Anhar requested an English counterpart of the approved Indonesian template. `design/ux/templates/ux-output.en.md` is an English translation with the same O1–O9 identifiers, field/table structure, conditional applicability, consumer handoff and non-authorization boundaries. It remains **DRAFT FOR REVIEW** as a newly created artifact. The English version must not add binding requirements, alter Product/UX authority or replace the accepted ID version. No independent bilingual user test is claimed.

## 12. A2 — Source validation and research settlement (2026-11-04)

**Approval scope:** Anhar approved A2 owning UX research semantics and the Indonesian UX Output template after reviewing exact commit `1658b5dad08e3f7b95c8bb8ccfbd3d67367a5c51`; section 11 pins the exact five approved content blobs. That approval covers reusable Harscode **research design**, not actual target-project UX decisions, a UX Space, invocation, or operational Harscode.

**Source validation:**
- Four local UX guidance files cover the stated 11 input information classes, nine conditional activities, nine logical output meanings and six desired quality properties. Lo-Fi proofs and web route specifications are conditional; no mandatory phase/Space/producer dependency was introduced.
- `design/ux/templates/ux-output.id.md` remained identical to approved blob `82c7e670d386142993f6588d096cdc0bbb8c67ec`. The three other UX guidance files (`AGENTS.md`, `definition.md`, `authority-and-handoff.md`) also retained approved blob identities.
- `design/ux/README.md` was revised only for **two-language template navigation**. Its substantive UX semantics and authority boundaries did not change; the accepted reviewed README content remains retrievable at blob `98146c6f58331dd41350fdbbad894aea6f27c2f2`. This editorial update is not treated as retroactively approved new semantic meaning.
- The requested `design/ux/templates/ux-output.en.md` is a newly authored English **DRAFT FOR HUMAN REVIEW** translated from the approved Indonesian template: the nine `O1–O9` identifiers/headings match, the source and translation have 41 Markdown table rows each, 40 placeholder rows each, and retain consumer handoff, exact-revision approval separation, and no implicit execution authorization. This parity check is structural/source-level, not independent user-language testing.
- **35 Markdown local relative links across seven directly related files checked; zero broken.** Direct UX routing has no `design/README.md` or parent `design/AGENTS.md`. No target-project, Engineering Space, `main`, or frozen baseline changes were made.
- Original Design root `design/exploration.md` and `design/authority-and-handoff.md` remain source-only transitional inputs to A3, not active UX instructions. No sibling UI or Project Standard guidance was invented before its audit.

**Residual:** English authoring template content is **not separately Human-approved**. Actual independent UX consumer checks, live agent-harness instructions, rendered/usability/accessibility validation, and project Product/UX authority compatibility are **NOT CHECKED / UNVERIFIED**. No approval or runtime claim is inferred from document existence. These limits are suitable for research closure; revisit A2 only with material new evidence, not merely to align file counts.

**A2 status: `SETTLED_FOR_RESEARCH`.** This is a source-level research settlement, not project Design acceptance or operational promotion.

## 13. A2 post-settlement — scoped Lo-Fi artifact representation formats (2026-11-04)

**Human working decision:** Anhar explicitly approved the **format-selection direction** for UX Lo-Fi: Markdown as default durable artifact; Mermaid fenced in Markdown for material diagrams; conditional HTML/CSS for structural Lo-Fi; minimal JavaScript only for justified, authorized interaction simulation. Diagram/wireframe/prototype formats are **not universal mandatory outputs**. The definition and both output authoring templates were revised under this bounded authorization; the new exact bytes remain subject to content review and source validation, and earlier approved blobs remain preserved in section 11.

**Amendment scope:** `design/ux/definition.md` adds format-selection, tool availability/fallback, renderer/interaction verification standing, simulation/proof limits, and prevention of competing artifact authority. `design/ux/templates/ux-output.id.md` and `ux-output.en.md` gain bilingual equivalent instructions and five metadata rows for covered logical output/proof question, artifact form, exact source, actual render/interaction verification, and evidence limits. No new template file, mandatory format, Space, runtime behavior or project-specific standards are introduced.

**Authority and validation:** The previously approved semantic UX contract and ID template remain available at their earlier exact blobs; adding this policy changes current file bytes and must not be mislabeled as automatically covered by the previous exact-revision approval. The English template was already a draft prior to this scoped amendment. Research A2 remains `SETTLED_FOR_RESEARCH` on its previously reviewed architecture and semantics; the new format-amendment revision is an **approved direction / newly authored reviewable content**, with source/consumer evidence checked separately. No actual diagram rendering, HTML browser run, real user test or independent consumer check is implied.

## 14. A2 exact-format acceptance and A3 research audit (2026-11-04)

**New A2 Human approval:** After reviewing UX Lo-Fi Artifact Format Policy v1, Anhar explicitly said **“approve bro. lanjut”**. This accepts the scoped A2 format amendment at `7ff01bdcef7487b24e7a142adbb4425a37e39ffe` **as Harscode research guidance content**, including the revised Indonesian and English authoring templates. Exact reviewed blobs:

| A2 format-amendment file | Accepted blob at `7ff01bd` |
| --- | --- |
| `design/ux/definition.md` | `6dba24605401866becc6901c81ef1c68cca04b5f` |
| `design/ux/templates/ux-output.id.md` | `eb3439e768e58e864efaed0a91d05f69b3e88263` |
| `design/ux/templates/ux-output.en.md` | `7c62b7dad2dddbbf0579c1285b719cdb3434e08a` |

The approval covers the **reusable research authoring formats** and does **not** create approved UX decisions for Kencleng, a new Space, runtime artifact-render evidence, or operational Harscode policy. Pre-existing DRAFT template headers are left untouched; this tracker carries external exact-revision decision evidence. A2 remains `SETTLED_FOR_RESEARCH`.

**A3 read-only source assessment:** [A3 UI & Project Design Standards audit](a3-ui-and-project-standard-deep-audit-and-target-design.md) compares the experimental UI 13 input / 9 process / 9 output / 6 outcome model with root transitional Design guidance, settled A2 UX boundary, actual Rancang/NextJS Builder consumer sources and Kencleng pilot project Design artifacts at `d6738298f43313d8c58afcec7b5131b33e0b26d0`. Findings `A3-F01–F10` recommend separate direct-entrypoint UI and Project Standard concerns, with explicit bounded UI vs project-wide standards promotion boundaries and conditional visual evidence. **No comparable Project Standard experimental I/P/O/O exists**, so the proposed standard model intentionally does not invent a fixed numeric contract. No owning `design/ui/` or `design/project-standard/` guidance was written in this audit commit; A3 remains `REVIEW_PENDING` for Anhar's review. Kencleng observed project policy is not imported as reusable Harscode policy.

**Unverified:** Actual UI visual/browser inspection, independent consumer execution, full target-project compatibility, and agent-harness/runtime behavior are **NOT CHECKED**; no claims of rendered/implemented acceptance.

## 15. A3-discovered A2 output sufficiency correction (2026-11-04)

**Evidence and decision:** The [A3 13-input compatibility mapping](a3-ui-input-to-ux-output-compatibility.md) exposed a material UX→UI quality failure mode: with optional O2/O6 a producer might deliver prose while UI lacks inspectable accepted flow or screen structure. Anhar explicitly approved **required-by-default O2 UX Flow and O6 representative Lo-Fi Wireframes on new/material UX work with evidence-based exceptions**. Reuse accepted exact-revision equivalent artifacts; exceptions require evidence, affected scope/O-ID, legitimate owner/delegation and consumer impact. Neither new file count nor a mandatory named UX Space/phase is implied.

**Scoped research amendment:** `design/ux/README.md`, `AGENTS.md`, `definition.md`, `authority-and-handoff.md`, and both output templates were revised at `f2e795c50d2c42b269f85bd69384aa91d982e5a3`. Current amended UX source is **authorized working research revision, pending exact-content review**, not retroactively covered by earlier blob approvals in sections 11–14. A2 remains `SETTLED_FOR_RESEARCH` for prior reviewed baseline with a **scoped revision under review**; no independent receiving UI test, browser visual checks or target-project design adoption yet.

**A3 receiving side (proposal):** The matrix classifies all 13 UI experimental inputs by true owning authority and material requiredness. It proposes a UI Input Sufficiency Check before dependent **final** visual decisions, allowing unaffected provisional visual exploration but preventing UI from inventing missing Product/UX/navigation/standard meaning. **A3 remains `REVIEW_PENDING`; neither the UI guidance nor the Project Standard concern has been created or approved.**

## 16. A2 exact revision approval and A3 UI direct-entrypoint drafting (2026-11-04)

**Human decision:** Anhar explicitly approved the **exact source revision `8d53c1ac3baccb8e277382f2b583281ff89c8f51`** of the scoped A2 UX required-baseline amendment and UI input compatibility mapping, then said **“lanjut”**. This authorizes scoped research drafting of UI guidance; it is **not** UI semantics approval, Kencleng authority amendment, operational Harscode promotion or permission to invoke any Space. Exact reviewed content blobs:

| Reviewed research file | Accepted exact blob at `8d53c1a` |
| --- | --- |
| `design/ux/README.md` | `095dbfa8d71f16701ba54d03a061fe0a87c46d51` |
| `design/ux/AGENTS.md` | `0fe4be40d7b2e5e62ff6a0ef06b46ad719c7044c` |
| `design/ux/definition.md` | `a503a571342868bb960973de4c9df9f3f9a190d8` |
| `design/ux/authority-and-handoff.md` | `17ecc553fa113a74c9d40c03a0b95ffd0f0213ea` |
| `design/ux/templates/ux-output.id.md` | `802b432b9b93ab65b1f0c2cc6c19ced029e14be5` |
| `design/ux/templates/ux-output.en.md` | `efab1db7e80c4df4d50b5bd1d339ed18b2a1db52` |
| `experiments/org-01-reverse-lifecycle/a3-ui-input-to-ux-output-compatibility.md` | `042eac8cafcdbd9fa8e681caf572b02fcf74df7e` |

The six UX guidance/template files preserve their original DRAFT/proposed metadata in the accepted bytes. The approval record here provides external exact-revision standing without silently editing the approved content to insert hashes/status. The compatibility map is **accepted research input analysis**, not an approved `design/ui/` owning definition.

**UI drafting checkpoint:** Four files authored at `44e513e0199ca9ea31e61a90b3f0760d8e1d0dc6` under `design/ui/`: `README.md`, `AGENTS.md`, `definition.md`, and `authority-and-handoff.md`. No shared Design parent router or sibling Harscode guidance dependency is introduced. The root README now directly links both UX and UI; the future Project Design Standard concern has **no owning files yet** and remains out of the current UI review scope.

**Substantive UI research design under review:** 13 experiment-led inputs classified by actual owning information, nine iterative responsibilities, nine logical UI outputs, six desired quality properties; explicit **UI Input Sufficiency Check**, evidence-backed UX O2/O6 source availability for new/material UX; default **inspectable visual proof for new/material UI** with responsive/state/copy coverage; conditional interactive prototype; UI candidate component vs separately approved reusable project Standard authority; project original-source and exact-revision Human review discipline.

**Residual validation:** Source-level link/semantic checks can establish only consistency of authored research files. No real target-project UI design case, rendered/browser comparison, accessibility/user usability test, independent Engineering consumer check, or agent harness run has been performed. `design/ui/` is **DRAFT / HUMAN CONTENT REVIEW PENDING**, not `SETTLED_FOR_RESEARCH`. A3 overall remains `REVIEW_PENDING`; project-standard research is not automatically accepted from the shared A3 audit.

## 17. UI guidance exact acceptance and bilingual artifact template proposal (2026-11-04)

**Human decision:** After reviewing the four owning UI guidance drafts at `2fe4c729c08f2cf277943c6be0bbf54ced7db7e4`, Anhar explicitly **approved the four guidance documents** and requested a standardized UI output artifact template. This accepts the scoped Harscode **research design content**, not a target-project Hi-Fi design, an actual Engineering handoff, a Design Space, or Harscode operational promotion. Exact approved original blobs:

| Reviewed UI research guidance | Accepted blob at `2fe4c72` |
| --- | --- |
| `design/ui/README.md` | `4c260d09c96ffb8d6f13e283b8be326a2c928d48` |
| `design/ui/AGENTS.md` | `abb826e81a3a5b1ba552446055d0f2f3ab502efb` |
| `design/ui/definition.md` | `571edef14ea98a975b764f06002f3204719ad0e4` |
| `design/ui/authority-and-handoff.md` | `70684a76892af5d628301ac5676694f3f5bd3bd5` |

**New authoring proposal:** `design/ui/templates/ui-output.id.md` and `ui-output.en.md` are matched-language **DRAFT FOR HUMAN REVIEW** authoring aids. Both preserve O1–O9 output semantics, default visual proof for new/material UI, conditional interactive prototype and library/asset needs, an I01–I13 source sufficiency summary, exact-revision review evidence, actual visual/viewport/state inspection standing and downstream consumer handoff. They are one logical output record (or navigable index), **not nine mandatory files or a second Design Authority**. A filled template cannot prove browser rendering or accept UI. No project-owned UI output is created, and no HTML mock, Product rule, UI Space or Design Standard change is required by this template itself.

**Revision boundary:** The previously approved four UI content blobs are retained in history. The UI README gets **navigation-only/editorial changes** to link the bilingual new templates and remove the previously accurate 'no output template' statement; that revised README's exact bytes are **not retroactively approved** by acceptance of the original README. The other three guidance documents are unchanged. This record is separate from approved content so no self-referential hash cycle occurs.

**A3 UI status:** Guidance semantics accepted **for research**; UI template authoring shape remains **review pending**. Overall A3 stays `REVIEW_PENDING` until template/content review and source checks; project-standard concern remains unstarted and not silently approved. Actual independent UI/Engineering consumer checks, browser rendering, visual fidelity, accessibility/usability and runtime proof remain `UNVERIFIED`.
