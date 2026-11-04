# A2 — UX Lo-Fi Deep Audit & Experiment-Led Target Design

> **Standing:** DRAFT FOR ANHAR REVIEW, research audit and proposal only. **Not accepted Design guidance, not target-project Design authority, not a formed Space and not an invocation approval.**
> **Repository and exact audit checkpoint:** anhsbolic/harscode-workspace at research/cross-stage-mapping, a6f6293971bc7f1eb9fe8243fe5a945233467f36 (2026-11-04).
> **Frozen reference:** refactor/harscode-foundation at 96b479c1a4e1ead77bb1614ef49bf09aca435c0d (read-only, not modified).
> **Method:** the [UX Lo-Fi reverse-lifecycle experiment](ux-design-lofi.md) is the **primary design reference**, challengeable when evidence or scope warrants. Existing Design guidance is the subject of audit, **not** the default architecture to preserve.
> **Decision owner:** Anhar. Approval of A1 Product working research guidance does not automatically approve this A2 proposal.

## 1. Scope and source evidence

**Owning Design files inspected in full at the exact research checkpoint:**

| Path | Verified blob | Observed responsibility |
| --- | --- | --- |
| design/README.md | fa38ef7c958a5b2dfd8fd8278fb508980b937d78 | Broad Design concern routing: interaction, content, accessibility, brand and visual |
| design/AGENTS.md | ff2e1f3764ed5f107518a94f6a2b901542ff7f31 | Authority-aware source routing, avoid Product invention, truthful states |
| design/exploration.md | 19dd26c2e45ececb21ad8a67cc183ce53decac4a | General interaction/brand/visual exploratory work; conditional evidence and review |
| design/authority-and-handoff.md | 46607a2ec7003b7a98cf4a50a4f671db2680eded | General Design authority standing and Engineering consumer packet |

**Consumer/reference checks:** experimental [Product Definition](product-definition.md), [UX Lo-Fi](ux-design-lofi.md), [UI Hi-Fi](ui-design-hifi.md), [Input–Source Mapping](input-source-mapping.md), [Candidate Reference Model](candidate-reference-model.md); new [Product core](../../product/product-definition.md) and [Product consumer handoff](../../product/consumer-handoff.md); relevant [Engineering Solution Input Contract](../../engineering/spaces/feature-solution-design/contracts.md) and [frontend Engineering Development Input Contract](../../engineering/spaces/nextjs-builder/contracts.md).

No Kencleng artifact or operational Harscode baseline was audited. Exact project-level source existence, usability, runtime behavior, formed Space acceptance, and actual consumer fit were not checked.

## 2. Target semantic model, led by the experiment

**Concern name for target model:** **Interaction & Experience Definition** (UX). “Lo-Fi” denotes a suitable fidelity/evidence approach, **not** a required lifecycle node, producing Space, or fixed prerequisite of visual design or Engineering.

### Inputs — 11 candidate information categories

| No. | Information needed | Decision-specific standing / acquisition |
| --- | --- | --- |
| 1 | Product Intent & Selected Outcome | Effective Product meaning or explicit bounded exploratory hypothesis |
| 2 | Actor Definition & Goals | Accepted source when binding, hypotheses clearly marked in exploration |
| 3 | Product User Journey | Meaningful Product progression, not fabricated UX flow |
| 4 | Product Requirements & Business Rules | Binding when consequential decision relies on them; otherwise explicit proposal |
| 5 | Product Acceptance Criteria | Required for affected binding design decisions; not evidence that tests ran |
| 6 | Content & Information Requirements | Product-owned consequential information and disclosure duties; project domain information may supplement |
| 7 | Accessibility & Device Requirements | Applicable accessibility/device constraints; relevant project standards and actual context |
| 8 | Existing IA & Navigation Patterns | Required when current and relevant; inspected for authority rather than inherited blindly |
| 9 | Known Technical Constraints | Material ones from accepted project/technical context; no requirement to wait for a named engineering Space |
| 10 | User Research & Usability Findings | Consider available relevant evidence; do not quietly discard it because the experiment says nice to have |
| 11 | UX Patterns & Design References | Optional aid, not normative precedence over project standards |

Inputs may originate directly from project Product/Design authority, Humans, research, standards, code evidence, and accepted technical constraints. **11 categories do not require 11 files.** Proposed and unverified Product meaning cannot silently become accepted business rules.

### Processes — nine logical activities

1. Actor Scenario Analysis.
2. UX Flow Design.
3. Information Architecture.
4. Webpage Map & Route Design **when the relevant experience has webpage routing**; otherwise equivalent navigation/surface definition as appropriate.
5. Lo-Fi Wireframing **when a low-fidelity structural proof adds value**.
6. Interaction & State Design, including truthful loading, validation, authorization, failure and uncertain results.
7. Lo-Fi Prototyping **when interactive proof can resolve a material question**.
8. UX Evaluation & Refinement, proportional to actual evidence and accessibility needs.
9. Human UX Review & Acceptance for consequential Design decisions.

These activities are **iterative** and selectively applicable. They are not nine gates, automatic stage transitions, or mandatory tool operations.

### Outputs — nine logical UX meanings

| No. | Experiment output | Research target interpretation |
| --- | --- | --- |
| O1 | Actor Scenario & UX Journey | Concrete UX interaction perspective grounded in Product actor/goals and meaningful domain journey; distinct from Product User Journey |
| O2 | UX Flow Diagram | Interaction progression, relevant branches, exit/recovery and user-visible decision points; suitable format may be prose, diagram or prototype |
| O3 | Information Architecture | Information hierarchy, grouping, priority and semantic organization without changing Product-required information |
| O4 | Navigation Structure | Actual navigational relationships and route/entry/exit meaning where material |
| O5 | Webpage Map & Route Specification | **Explicit consumable web Design contract when applicable**: accepted/proposed webpage paths, purpose, entry/exit, navigation relations, page-vs-UI-state distinction; not backend API routes |
| O6 | Lo-Fi Wireframes | Screen/structural representation as needed for decision, not always mandatory separate file |
| O7 | Interaction & UI State Requirements | User-facing default, validation, loading, disabled, permission, success, failure, partial, uncertain and recovery behaviors **when applicable** |
| O8 | Lo-Fi Interactive Prototype | Bounded interaction simulation/evidence when justified; **not proof of real backend behavior or actual user usability** |
| O9 | UX Review & Decision Record | Legitimate Human UX decisions, exact reviewed artifacts and effective standing, scope, evidence and open issues; not Product approval |

Nine outputs are **logical content/decision obligations** for the relevant scope; no nine-file or universal nine-artifact requirement. Some outputs may be combined into one consumable Design source or marked not applicable with reason. A web route specification is a first-class accepted Design input for visual UI decisions that depend on routing; a non-web or non-route task does not need a pretend webpage map.

### Outcome — six desired quality properties

**Goal-Oriented, Intuitive, Clear IA, Efficient, Trustworthy, Accessible.**

They describe desired UX design quality. Approval of a prototype or good same-session walkthrough is **not** independent usability research, accessibility testing, implementation verification or proof that an actor actually succeeded.

## 3. Evidence-backed findings

| ID | Priority / disposition | Actual source and observation | Material gap / consequence | Proposed correction |
| --- | --- | --- | --- | --- |
| A2-F01 | HIGH — REPLACE primary model | design/README.md and design/exploration.md describe broad interaction/brand/visual responsibility but not a coherent UX-specific Input → Process → Output → Outcome contract | UX completeness is inferred ad hoc; receiving responsibilities may not know which interaction meanings are accepted | Define **Interaction & Experience Definition** as coherent concern with 11/9/9/6 semantic coverage |
| A2-F02 | HIGH — REVISE entry rules | design/exploration.md says to **start with approved Product experience** and return missing material meaning. A1 Product explicitly allows labeled hypotheses for bounded exploration | Could block legitimate discovery or conceal assumed Product semantics; material binding UX decisions still need proper Product authority | Separate exploratory hypothesis-based UX from binding accepted Design decisions, proportional to consequence |
| A2-F03 | HIGH — REVISE output contract | design/README.md, exploration.md, and authority-and-handoff.md mention interaction/priority/states broadly, but no explicit UX Flow, IA, Navigation, Webpage Map/Route and Lo-Fi output semantics | Visual design or technical solution responsibility may infer webpage routing, material states, or information grouping without accepted Design source | Explicit logical UX outputs, especially web route/page-vs-state contract and accessible interaction-state requirements |
| A2-F04 | HIGH — CLARIFY concern boundary | Design entrypoint combines UX and visual expression; authority/handoff refers to generic “Design intent” | UX acceptance and visual design acceptance may be conflated; a design artifact can inadvertently overrule accepted Product or UX navigation | Separate **functional responsibility** for Interaction & Experience Design from Visual Interface & Content Design. Don't prescribe separate Spaces/agents; defer final physical Design layout until A3 |
| A2-F05 | HIGH — REVISE consumer-fidelity rules | design/authority-and-handoff.md already supports revision standing and generic consumer packet, but no explicit UX-specific exact-revision contract for downstream navigation/state decisions | A useful prototype, old wireframe, or proposed route could be mistaken for effective accepted Design constraint | Make accepted UX decisions / exact sources / scope / unresolved matters consumable by **what** receiving responsibility needs; no direct named-Hi-Fi/Rancang/Builder dependency |
| A2-F06 | MEDIUM — CLARIFY web-specific conditionality | ORG-01 UX experiment enumerates webpage paths, Lo-Fi wireframes and clickable prototype for a web scenario | Promoting all into universal UX requirements causes fictitious webpages or mandatory prototype ceremony for other tasks | Preserve web route contract **when applicable**, with explicit N/A; require a proof only if it informs a real decision |
| A2-F07 | MEDIUM — KEEP safeguards, extend evaluation | design/exploration.md and design/AGENTS.md already prohibit simulated success from becoming backend evidence and require truthful/accessibility states | Those safeguards are good, but a UX evaluation activity/decision record has no explicit coverage/evidence standing in current guidance | Retain safeguards; define what walkthrough, heuristic/a11y check, prototype and real user test each can and cannot prove |
| A2-F08 | MEDIUM — CLARIFY source acquisition | design/AGENTS.md says verify project Product/Design authority and existing constraints; experiment maps Product Contract, standards, research and technical constraints from multiple sources | An agent could presume fully approved Product inputs or a prior engineering handoff is always required | State **information-first, many-to-many, source/standing-based** discovery; no mandatory prior phase/Space |

**Important positive findings to preserve:** The current four Design files already honor target-project authority, delegation, security/privacy implications, truthful states, accessibility, Human review, evidence vs approval and no automatic Engineering invocation. They are source material to preserve semantically—not a document layout to retain by default.

**Unproven risks:** No actual project UX decision, independent consumer, or usability test was run here. These are risks of under-specified reusable guidance, not observed ORG-01 UX failures.

## 4. Revised Design domain architecture — 2026-11-04, still PROPOSED

After the original A2 audit, Anhar proposed three **independent concerns under `design/`**: `ux/`, `ui/`, and `project-standard/`, seeking focused ownership and recalling legacy project-wide Design exploration. This proposal is materially better than the previous flat `design/ux-definition.md` candidate **as a review direction**, but is not yet a final approved Harscode guidance revision.

```text
design/
├── README.md                   # Cross-concern navigation; current subject mapping only here when actual
├── AGENTS.md                   # Research routing and authority boundaries
├── authority-and-handoff.md    # Shared standing, approvals, source and consumer checks
├── ux/
│   └── definition.md           # Interaction & Experience Definition, A2
├── ui/
│   └── definition.md           # Visual Interface & Content Definition, A3
└── project-standard/
    └── definition.md           # Reusable project-level Design Standard formation/evolution
```

Folders are **responsibility scopes, not runtime Spaces or required sequential phases**. Lo-Fi and Hi-Fi describe possible design fidelity and proofs; they are not the names of permanent upstream/downstream producers. New templates, additional `README.md` files, workflow states and a new audit unit are not justified by a folder split alone.

**Separate but connected meaning:**
- **UX Definition** owns bounded interaction progression, IA, navigation/webpage paths where relevant, interaction state meaning and UX decision acceptance. Its UX decisions may reference established reusable project standards, but are not automatically standards themselves.
- **UI Definition** owns bounded visual/interface, UI copy, composition, responsive expression, reusable components/assets when needed, and accepted UI decisions. It may depend on accepted UX navigation/information as material **information**, not on a mandatory UX Space having run.
- **Project Design Standards** owns defining, authorizing, evolving and making discoverable **reusable project-level design rules**: judgment principles, recurring interaction patterns, brand/product-UI direction, visual-system guidance, writing/terminology conventions and asset-governance rules when legitimately in scope. It does not own Product semantics, all feature UX/UI decisions or implementation technology.
- **Shared Design authority/handoff** defines cross-concern approval standing, exact revisions, original-source checks and functional consumer needs. It must not turn independent UX/UI decisions into one blanket Design approval.

An accepted UX/UI finding may motivate a proposed standard change; it **does not** automatically become project-wide precedent. A project-wide standard may constrain multiple UX/UI decisions, but those receiving responsibilities remain separately owned. A Design Standard may have working/research standing and need not be canonical. A project may use a single accepted standard artifact or several subject-specific sources; **these folders belong to reusable Harscode guidance, not a mandatory layout inside each project's `docs/design/`.**

**Scope discipline:** A2 only drafts/reviews `design/ux/definition.md` and relevant cross-cutting navigation/authority effects after Anhar approval. A3 will independently examine `design/ui/` and project-standard separation using Hi-Fi experiment and project evidence. No extra A7 audit unit or automatic parallel `project-standard/` Space is implied. `design/exploration.md` remains pending disposition after review; no legacy history index is proposed.

**No UX template yet.** A template should solve a real authoring or consumption need, not follow from nine logical outputs.

## 5. Cross-responsibility boundaries and two critical tests

**Product vs UX:** Product User Journey gives actor/domain meaning, rights, consequential information and success. UX Journey and UX Flow give human interaction progression, information grouping, navigation and interaction behavior. UX never fabricates Product role authority, consent/legal status, or success semantics.

**UX vs Visual Interface Design:** accepted UX navigation, flow, IA and interaction-state obligations are consumable Design constraints; visual/interface expression can propose revisions but cannot silently replace binding UX decisions. Where webpage paths are accepted, any material technical infeasibility is a reconciliation finding for the Design owner; technical Engineering owns backend API routes, not automatic ownership of webpage navigation.

**Consumer input check:** Distinguish (a) generic fit with a real declared receiving Input Contract, if one exists, from (b) actual project-bound consumer fit, which is not proven here. Source inspection/authorization duties of a real consumer are not waived by an apparently self-contained UX handoff.

**Evidence check:** Prototype clickability, hypothetical scenario, accepted UX revision, independent accessibility check and observed real-user usability are separate evidence claims. Do not certify more than the actual method supports.

## 6. Revised recommendation and decision gate

**Strong recommendation:** Adopt **one Design domain with three independent functional concerns**: `design/ux/`, `design/ui/`, `design/project-standard/`. This is a **proposed design**, not a Human-approved owning-source revision. The original A2 UX Input → Process → Output → Outcome (11/9/9/6) remains a challengeable core reference with conditional UX proofs and web-specific route obligations.

The core split protects both **feature-specific Design decisions** and **reusable project-standard authority**. Ownership must follow actual meaning: some UX patterns are reusable Design Standards, some are bounded UX decisions; some visual assets are canonical identity, others merely prototype evidence. Distinguish source standing explicitly.

For A2, request Anhar's decision on the **three-concern architecture** and scoped draft of `design/ux/definition.md`; do not prematurely finalize `design/ui/definition.md` or `design/project-standard/definition.md` before A3 evidence review. The existing shared `design/authority-and-handoff.md` can be reconciled as one cross-cutting contract if sufficient, avoiding competing approval systems.

A2 settlement requires Human decision on material UX semantics, source-level revised research guidance with checked links and consumer boundaries, explicit uncertainty on real usability/project consumption, and scoped actual revision evidence. Do not alter Engineering Space formation or adopt Kencleng project standards as Harscode defaults.

**Review status:** A2 remains **REVIEW_PENDING**. No owning `design/` changes, Kencleng edits, or operational promotion in this checkpoint.

## 7. Project-level and historical Design evidence — 2026-11-04

**Kencleng source inspected read-only:** `anhsbolic/kencleng@d6738298f43313d8c58afcec7b5131b33e0b26d0`, branch `pilot/station5-c1-space-only`, `docs/design/`. This was requested by Anhar to validate the proposed architecture, **not to change Kencleng authority, its effective project baseline, or its feature decisions**.

- [Design authority router](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/README.md) distinguishes **project-wide reusable design authority** from Product meaning, and routes to different owning concerns: Product Design Principles, brand/Product UI brief, visual-system guidelines, UX patterns, asset governance, working IA and writing heuristics, selected reference evidence.
- [Product Design Principles](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/product-design-principles.md), [Brand/Product UI Brief](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/brand-product-ui-brief.md), [Visual Guidelines](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/design-guidelines.md), [UX Patterns](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/patterns.md), and [Asset Governance](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/asset-governance.md) carry **canonical** project Design standing in their headers.
- [Information Architecture](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/information-architecture.md) and [Indonesian UX Copywriting](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/copywriting-id.md) explicitly say **working supplemental guidance**, **not** amendments to canonical Product/Design meaning; work may be explored without claiming a new standard.
- [Selected visual references](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/visual-references/selected-direction/README.md) are approved **direction evidence**, not production assets/pixel specifications or Product-state authority. No PNG pixel analysis is claimed.
- [ORG-01 Design Candidate handoff](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/outcomes/org-01/handoff.md) explicitly says **DESIGN CANDIDATE / NOT HUMAN APPROVED**. It references project-wide Design standards without making its experimental feature UI a canonical project-wide rule.
- [Optional Hi-Fi kickoff](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/templates/hi-fi-static-html-kickoff.md) is an **optional session aid**, not a new Design Standard, Space, or permission to write/commit.

**Interpretation:** Kencleng demonstrates the **useful authority distinction** between reusable project Design rules, working guidance, approved direction evidence and outcome-specific candidate Design. It supports considering `project-standard/` as a **separate reusable responsibility**; it does **not** prove Harscode needs a mandatory standardization stage, a particular file count, these exact Kencleng standards, or a new formed Space.

**Legacy supporting evidence (read-only, not current Harscode guidance):** `deprecated/legacy/product-design/product-brand-and-ui-exploration.md` discusses Product-truth-grounded Design direction exploration and later concrete visual system; `deprecated/legacy/product-design/design-authority-and-canonicalization.md` distinguishes exploratory proof from Human-approved durable reusable authority. Their valid insight is **explore → decide/approve → persist reusable rule when justified**, not a required waterfall or a mandate to copy legacy files into the active foundation.

**Unverified:** Actual cross-project applicability, independent source consumption, real rendered UX tests and project-specific adoption. No claim that a new three-concern documentation arrangement has been tested in real work.
