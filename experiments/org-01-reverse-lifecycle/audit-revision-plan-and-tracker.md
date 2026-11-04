# Cross-Stage Foundation — Sequential Audit & Revision Plan / Tracker

> **Status:** PLAN AGREED; A1 experiment-led reassessment and approved research guidance persisted; A1 still REVIEW_PENDING; A2–A6 NOT_STARTED.
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
| **A1 Product** | `REVIEW_PENDING` | A1 v2 read-only reassessment of all 11 Product files; experiment-led I/P/O/O, actor/journey/role/content/approval and subject-independent consumption | Anhar approved new 4-guidance/3-optional-template target and core/authority/consumer working design (2026-11-04); authorized research branch persistence and additional draft templates | Research redesign commits; three templates **DRAFT for review**, legacy migration and independent consumer fit **not checked** | Review draft templates, source/references and legacy cleanup before settlement |
| **A2 UX Lo-Fi** | `NOT_STARTED` | F-01/F-03 candidate only | None | None | After A1 adequately settled |
| **A3 UI Hi-Fi** | `NOT_STARTED` | F-01 candidate only | None | None | After A2 adequately settled |
| **A4 Rancang** | `NOT_STARTED` | F-03/F-05 candidate only | None | None | After A3 adequately settled |
| **A5 Builder** | `NOT_STARTED` | F-04/F-05 candidate only | None | None | After A4 adequately settled |
| **A6 Final coherence** | `NOT_STARTED` | F-06 candidate only; revisit all accepted changes | None | None | After A1–A5 |

**Progress accounting:** `0 / 6` audit units settled (A1 redesign persisted but still pending template/compatibility review). Setup is complete, **not** counted as A1 progress. Do not award a phase PASS based on the earlier first-pass assessment, candidate mapping coverage, or approved experiment snapshots.

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

**A1 — Product deep audit, read-only first.** Inspect the 11 existing Product files at their exact revisions; map content and consumer contracts against the [Product experiment model](product-definition.md). Produce an evidence-backed gap/recommendation summary for Anhar before making owning-source edits. Update the A1 row only after actual work, with the observed scope and refs.

## 8. A1 v2 — persisted redesign checkpoint (2026-11-04)

Anhar explicitly shifted A1 to **experiment-led fundamental reassessment**, without preservation bias toward the prior six-phase layout or historical ORG-01. The experiment remains challengeable, not canonical. A1 v2 evaluated all 11 Product files and approved a new **4-guidance / 3-optional-template design**, where Product Definition is one concern with 13 information inputs, nine iterative activities, six logical outputs and six quality properties. Dependency direction is **required information and functional responsibility (what), not named Space/Agent (who)**.

**Persisted guidance:** `product/README.md`, `product/AGENTS.md`, `product/product-definition.md`, `product/authority-and-approval.md`, `product/consumer-handoff.md`. **Templates (unapproved drafts for Anhar's repository review):** `product/templates/product-definition.id.md`, `product/templates/product-contract.id.md`, `product/templates/product-approval-record.id.md`. The former phase files and English template remain temporarily for scoped migration, and are not active entrypoints to the proposed new research model. New Product research guidance is **not** operational policy and does not amend approved Engineering Space definitions.

**Evidence limitations:** This is source/draft design work, not a validated Product process, target-project ORG-01 reapproval, independent fresh consumer check or runtime test. Actual deletion/redirect and compatibility work remain open. The research commit/revision should be verified against the branch when closing A1.
