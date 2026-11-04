# A3 — UI Definition & Project Design Standards: Deep Audit and Target Design

> **Standing:** A3 RESEARCH DRAFT / REVIEW_PENDING (2026-11-04). Evidence-backed comparison and recommended target semantics **only**, not approved reusable UI/Project Standard guidance, not Kencleng Design authority, not a formed Space, not operational Harscode.
> **Decision owner:** Anhar. The **three independent direct-entrypoint design concern directories** were approved earlier, not the unreviewed A3 I/P/O/O/authority content.
> **Audit baseline:** `anhsbolic/harscode-workspace@7ff01bdcef7487b24e7a142adbb4425a37e39ffe` on `research/cross-stage-mapping`. Frozen initial comparison: `refactor/harscode-foundation@96b479c1a4e1ead77bb1614ef49bf09aca435c0d`.
> **Project evidence (read-only):** `anhsbolic/kencleng@d6738298f43313d8c58afcec7b5131b33e0b26d0`, branch `pilot/station5-c1-space-only`, `docs/design/`.
> **Method:** [UI Hi-Fi experimental I/P/O/O](ui-design-hifi.md) is the **primary challengeable reference** for UI; no comparable independent Project Standard I/P/O/O experiment has been approved. Treat existing project standards and old Harscode Design guidance as observed/source evidence, **not** general Harscode policy.

## 1. Inspected evidence and authority limits

**Current Harscode owning source:**
- `design/exploration.md` (blob `19dd26c2e45ececb21ad8a67cc183ce53decac4a`): general interaction, brand/visual exploration, Product truth, proof and bounded Human acceptance; **transitional root source**, not active UI/project-standard contract.
- `design/authority-and-handoff.md` (blob `46607a2ec7003b7a98cf4a50a4f671db2680eded`): generic Design approval standing, canonicalization, handoff and Engineering freedom; **transitional**, not accepted independent UI/project-standard guidance.
- `design/ux/definition.md` and `design/ux/authority-and-handoff.md`: A2 UX semantics, scoped decisions, web-route information contract, optional visual proof formats and separate exact-revision acceptance. UX is a **distinct concern already SETTLED_FOR_RESEARCH**; do not redefine it under UI.
- `product/product-definition.md`, `product/consumer-handoff.md`: Product owns meaningful actor consequences, Domain Roles, required information and acceptance; no UI design may silently alter them.
- `engineering/spaces/feature-solution-design/contracts.md` and `engineering/spaces/nextjs-builder/contracts.md`: Engineering consumes **applicable** Product/Design/standard sources and actual source revisions; no mandatory Hi-Fi or Lo-Fi file chain. Their formation/execution standing remains their own, not changed here.

**Kencleng real project evidence, pinned:**
- [Project Design entrypoint](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/README.md): explicitly owns **reusable project Design Standards**, not feature routes/delivery scope.
- [Product Design Principles](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/product-design-principles.md), [Brand/Product UI Brief](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/brand-product-ui-brief.md), [Visual Design Guidelines](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/design-guidelines.md), [UX Pattern System](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/patterns.md), [Asset Governance](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/asset-governance.md): independent **canonical project-wide concerns** at that pinned revision.
- [Information Architecture](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/information-architecture.md), [Indonesian UX Writing](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/copywriting-id.md): **working supplemental project guidance**, not automatically new canonical standards.
- [ORG-01 UI handoff](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/outcomes/org-01/handoff.md) and [static HTML candidate](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/outcomes/org-01/prototype.html): outcome-specific **DESIGN CANDIDATE / NOT HUMAN APPROVED**, explicitly no backend effects, no real visual/browser verification; prototype's mere existence does not create project standard, Product authority or implementation permission.
- [Selected-direction visual references](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/visual-references/selected-direction/README.md): approved **direction-level visual evidence**, not production assets or pixel authority. PNG pixels were **not independently inspected** in this audit.
- [Optional Hi-Fi HTML kickoff](https://github.com/anhsbolic/kencleng/blob/d6738298f43313d8c58afcec7b5131b33e0b26d0/docs/design/templates/hi-fi-static-html-kickoff.md): **optional project session aid**, not a Harscode universal HTML mandate, approval or write/commit authorization.

**Historical supporting context:** `deprecated/legacy/product-design/product-brand-and-ui-exploration.md` and `deprecated/legacy/product-design/design-authority-and-canonicalization.md` distinguish exploration evidence, selected direction, reusable system rules and Human-authorized canonicalization. Only the **reusable concern and authority insights** are considered; no historical phase, document or style is reactivated.

**Evidence limitations:** This audit is source-level; no Figma/PNG visual inspection, HTML browser rendering, real independent user study, A3 agent harness session, actual project-bound consuming test or runtime proof was performed. Kencleng project-specific standards are evidence of a **pattern that worked for that project**, not universally correct Harscode default values.

## 2. Proposed UI Definition model — challengeable 13 / 9 / 9 / 6

**Concern:** `design/ui/` — **Visual Interface & Content Definition**, independently addressable. “Hi-Fi” denotes a fidelity/evidence level, **not a Space, agent, stage, or universal precondition**.

### INPUT — 13 information needs from the experiment

| # | UI information needed | Revised conditionality / owning truth |
| --- | --- | --- |
| 1 | UX Flow Diagram | **Accepted interaction meaning** required if material; Mermaid/file is **not** universally mandatory |
| 2 | Lo-Fi Wireframes | Structural UX/surface decisions **if available and material**; a wireframe artifact is not a universal prerequisite |
| 3 | Webpage Map & Route Specification | Accepted UX **web navigation/path contract when web routing is materially in scope**; not backend API routes |
| 4 | Product Requirements & Business Rules | Applicable effective Product meaning / clear bounded hypotheses for exploration; UI cannot approve or change business consequences |
| 5 | Screen Content & Information | Product-owned consequential content, UX information priority, required disclosures and accepted source wording when material |
| 6 | UI States & Interaction Requirements | Applicable UX/technical state meanings and observable behavior including pending, failure, unauthorized, incomplete, unknown and recovery |
| 7 | Brand & Visual Guidelines | Effective target-project visual authority when present; absent direction requires explicit bounded Design freedom or escalation **only for material brand decisions** |
| 8 | Responsive & Accessibility Requirements | Applicable accessibility, input modes, device widths and real design priorities; don't infer a universal device matrix |
| 9 | Design Quality Criteria / Anti-AI Slop Guidelines | Contextual craft/evaluation heuristics: intentional hierarchy, non-filler visuals, truthful copy and fit-for-purpose density; **not** an aesthetic scoring machine |
| 10 | Existing Design System & UI Component Library | Applicable effective tokens/components, if they exist; existing code alone is not accepted Design authority |
| 11 | Web Assets | Actual approved assets, provenance/licensing and reuse constraints if applicable; no forced generation |
| 12 | Visual References / Moodboard | Supporting evidence when relevant, with bounded authority; must inspect actual pixels before claiming visual fidelity |
| 13 | Usability Research / User Feedback | Evaluate available reliable findings proportionately; lack of evidence is not proof of usability |

**Inputs are information categories, not 13 required files or producers.** UX accepted flow, IA, navigation and route decisions matter **when the UI task relies on them**. If material input is absent, explicitly distinguish a bounded proposal/hypothesis from binding UI. No forced completed Product → UX → UI chain.

### PROCESS — nine conditional/iterative UI responsibilities

1. Screen & Content Planning — real surfaces, decision-point hierarchy and faithful material information.
2. Visual Direction — style/composition consistent with effective project authority, or bounded new exploratory proposals.
3. Reusable UI Component Design & Management — reuse first; design/extend component states and variants **when warranted**. Reusable promotion authority is **not** automatically UI-owned.
4. Hi-Fi Screen Design — actual scoped screens/views; no mandate to produce final Hi-Fi for trivial delegated changes.
5. Responsive Design — behavior and information priority across relevant form factors.
6. Interaction & UI States Design — visual treatment for accepted transitions, errors/unknowns, focus and recovery.
7. UI Copywriting & Visual Assets — natural localized final UI expression, truthful asset provenance and purpose.
8. Interactive Prototyping — **conditional** reviewable representation when interactive proof answers a real question.
9. Design Review & Refinement — proportional visual/interaction/accessibility/copy checks, Human review where consequential and actual findings.

Anti-AI-Slop criteria apply as contextual craft discipline **within** direction, screen, copy and review work, not a new procedural gate. Activities may interleave and need not run when existing effective UI is sufficient.

### OUTPUT — nine logical UI results

| ID | Output meaning / ownership | Representation and standing |
| --- | --- | --- |
| O1 | **Hi-Fi Screen Designs** | Actual bounded visual/interface design for necessary surfaces; image, HTML or other inspectable medium as tools permit; not a requirement for every UI task |
| O2 | **Interactive Prototype** | Conditional simulated interaction, showing evidence limits; no inferred API or usability proof |
| O3 | **Responsive Designs** | Viewport/interaction adaptations that preserve real priority and accessibility, represented as actual examples or traceable rules |
| O4 | **UI Interaction States** | Visually expressed accepted success/loading/denied/error/unknown/recovery states; not new Product/state authority |
| O5 | **UI Components & Styles** | Specific visual components, variants, type/color/spacing and scope-relevant visual specification for consumption |
| O6 | **Reusable UI Component Library** | Conditional **candidate** Design-level reusable patterns/variants; effective project-wide standardization and supersession require separate Project Standard owner approval |
| O7 | **Final UI Copywriting** | Actual UI language/copy, provenance and approval boundaries where consequential Product/legal terms apply |
| O8 | **Final Visual Assets** | Scoped UI assets/references, ownership, evidence, licensing and approval standing; brand-defining project-wide canon is separate |
| O9 | **Design Review & Acceptance Record** | Legitimate Human dispositions, exact inspected revisions, evidence/limits and accepted scope; separate from UI candidate to preserve immutable bytes |

Nine logical outputs **do not imply nine files**. Reuse what is already accepted. A representative HTML file may combine O1/O3/O4/O5/O7 evidence. A component library is neither automatically required nor automatically canonical just because a component was authored.

### OUTCOME — six desired Design qualities

**Clear · Intuitive · Informative · Transparent · Accessible · Visually Coherent.**

These are **design-level targets**, not measured real-user satisfaction, completed accessibility testing, approved project UI, delivered application or successful backend behavior.

## 3. Proposed Project Design Standards concern — no invented fixed I/P/O/O count

**Concern:** `design/project-standard/` — **Project Design Standards Definition & Evolution**, not a directory containing the actual project's standard files. It provides reusable guidance for **how a project decides, adopts, scopes, revises, supersedes and exposes project-wide Design rules**, while actual Product/Design authority stays inside the target project.

No independent project-standard experiment established a 13/9/9/6-style contract; **do not fabricate fixed input/output counts** merely to mirror UI or Product. Start with a simple open semantic model:

| Dimension | Candidate responsibility |
| --- | --- |
| **Input information** | Project Product/design truth and scope; existing effective principles/patterns/visual/brand/copy/asset standards; repeat-use evidence or material uncovered gap; available design exploration, representative visual proofs, accessibility/device requirements and consuming implementation constraints; legitimate Human authority and actual change impact |
| **Process meaning** | Find whether an accepted rule already covers the need; test if the proposed rule is **genuinely reusable within the target project**; distinguish ordinary feature-specific solution from stable project precedent; explore material options/proof proportionately; inspect contradictions and affected consumers; request authorized Human decision where durable precedent is at stake; persist **only the accepted exact bounded standard revision** to its project owner source; update real routing; reconcile superseded guidance and affected consumers |
| **Output meaning** | Effective **project-owned Design Standards** with scoped decision, exact revision and approval standing where warranted; candidate standard proposal/visual evidence when still open; a clear authority map/ownership pointers; applicable adoption/supersession/consumer impact record; open items with their legitimate owner; no universal mandatory file inventory |
| **Outcome quality** | Discoverable, truthful, internally coherent, reusable enough to justify its governance cost, appropriately evidenced, navigable from fresh sessions and not silently contradicted by active feature guidance or implementation |

**Project standard categories may include** Product Design principles, reusable UX interaction patterns, Brand/Product UI direction, visual system/tokens, content/writing conventions, component-system design rules and asset governance **when real project scope calls for them**. Categories are not mandatory per-project documents or required completion gates.

**Authority distinction:** A project-standard *rule* may constrain multiple UX/UI outcomes. A feature-specific UX or UI design can propose a new generalizable rule but **does not approve or promote that rule**. A Design-level reusable component library may be authored as UI output, but its **binding reusable project-wide behavior** and change governance are standard-owned. Visual references can be approved as **bounded direction evidence** without being production assets or pixel specs.

**One authority per distinct decision, not one giant standard master file.** The project can distribute standard ownership over several project-owned documents as Kencleng does. No Harscode requirement for a `docs/design/project-standard/` physical folder in the target project. Avoid duplicating canonical rules in a mandatory Harscode copy.

**Exploration is conditional:** Don't run a brand workshop for each feature or impose a standardization phase. If effective project standards are sufficient, consume them directly. If a materially missing standard would create unsafe/inconsistent precedent, propose the smallest legitimate improvement, preserve ordinary work that can continue independently, and apply appropriate Human approval.

## 4. Evidence-backed A3 findings

| Finding | Priority | Observation at inspected source | Risk / target disposition |
| --- | --- | --- | --- |
| **A3-F01** | HIGH | `design/exploration.md` mixes interaction, visual expression, brand and accessibility; `design/authority-and-handoff.md` owns generic Design review only | **REPLACE root routing** with self-contained `design/ui/` and `design/project-standard/` guidance, preserving reusable safeguards without a parent Design agent dependency |
| **A3-F02** | HIGH | UI experiment calls **UX Flow, Lo-Fi Wireframes, Webpage Map** all “Wajib” for illustrative web ORG-01; A2 now explicitly makes Lo-Fi proofs conditional | **REVISE input acquisition** to accepted information where material; web routes first-class when applicable, not mandatory Lo-Fi deliverable or mandatory UX actor/Space |
| **A3-F03** | HIGH | UI experiment assigns reusable components/library to UI work; Kencleng has separate canonical Design Standards and project-owned asset governance | **SPLIT production vs promotion:** UI can produce component candidates and scoped assets; Project Standard owns authorization of reusable project-wide rules, not every feature UI artifact |
| **A3-F04** | HIGH | Kencleng `docs/design/README.md` routes five independently canonical standard concerns; working IA/copy docs have lower authority | **MODEL Project Standard separately** with explicit selection, evidence, exact-revision approval and change/consumption rules; no universal mandatory standards file set |
| **A3-F05** | HIGH | Kencleng ORG-01 `prototype.html` + `handoff.md` is **NOT HUMAN APPROVED**, even though a project-wide design system is canonical | **DISTINGUISH standing** of visual evidence, candidate UI, accepted bounded UI, project standard and implementation; no image/mock/prototype self-approval |
| **A3-F06** | MEDIUM | Experiment includes Interactive Prototype and 9 outputs; Kencleng principles explicitly say Hi-Fi is **not a universal prerequisite** to frontend work | **CONDITIONAL proof**: visually inspect when needed for material UI correctness; require actual browser/render evidence before claiming rendering verified; don't force nine artifacts or HTML for every UI choice |
| **A3-F07** | HIGH | Project Design rules preserve Product truth, asset provenance and accessibility; current generic Design guidance forbids false status, evidence and simulated success | **KEEP safety invariants**: no invented business/legal/security status; realistic states/copy, truthful provenance, non-color-only cues; project standards cannot override Product authority |
| **A3-F08** | MEDIUM | Kencleng optional HTML Hi-Fi kickoff has particular multi-page-file and review/persist stops; ORG-01 candidate uses one standalone HTML | **DO NOT UNIVERSALIZE local mechanism**: HTML is one useful preview format, but file count, split pages and tooling follow actual task, evidence and authorized environment |
| **A3-F09** | MEDIUM | Hi-Fi experiment's “Anti-AI Slop” heuristic is useful but subjective; effective visual guidelines already define concrete project-specific design quality | **CLARIFY quality** through inspectable task-based criteria: hierarchy, usable copy, density, asset purpose, composition and actual rendering when possible; no universal visual taste scoring gate |
| **A3-F10** | MEDIUM | Rancang and NextJS Builder consume **applicable original Design sources** rather than a named universal upstream design document | **KEEP responsibility-based consumption** with source standing, exact revisions, delegated implementation freedom and project-bound verification; don't create mandatory stage handoff files |

**Observed positives:** Existing Harscode Design generic guidance already distinguishes Product truth, generated proofs, source status, visual evidence, Human approval, accessibility and Engineering implementation freedom. Preserve those **semantics**, not the root-file package. Kencleng demonstrates real project reusable standards, working supplemental aids and feature candidates in one project tree **without making them one authority**.

## 5. Proposed direct-entrypoint target architecture (agreed structure, A3 content not yet approved)

```text
design/
├── ux/                         # A2 accepted research design + optional ID/EN UX templates
│   ├── README.md
│   ├── AGENTS.md
│   ├── definition.md
│   └── authority-and-handoff.md
├── ui/                         # A3 target only — not yet created
│   ├── README.md
│   ├── AGENTS.md
│   ├── definition.md
│   └── authority-and-handoff.md
└── project-standard/           # A3 target only — not yet created
    ├── README.md
    ├── AGENTS.md
    ├── definition.md
    └── authority-and-handoff.md
```

Each concern's four files must suffice **without loading `design/` root guidance or sibling Harscode guidance**, but must still respect repository-root/project/harness security and actual owning source authority.

**No mandatory template decision yet for UI or Project Standard.** The A2 UX output template is evidence that a compact optional authoring shape can be useful; whether UI needs a design-handoff template or Project Standard needs an evolution template should be decided based on concrete review/consumer needs. Avoid making templates whose only function is to repeat a definitions file.

**Transitional root disposition:** After scoped A3 content approval and migration checks, retire `design/exploration.md` and `design/authority-and-handoff.md` from active research tree. Harvest necessary semantics into the two appropriate concerns, pin any historically evidence-bearing citations to inspected immutable sources, check inbound active links, and avoid a legacy/history index. Don't delete those transitional files prematurely in a read-only audit.

## 6. Visual artifact policy candidate for A3 (NOT yet approved)

**UI expression often needs visual inspection to be meaningfully reviewed**, but neither the A2 Markdown/Mermaid/HTML choices nor Kencleng's particular HTML kickoff should be copied into a universal A3 tooling mandate.

Potential minimum: Markdown as durable decision/handoff index; a **tool-supported inspectable visual representation** for material composition/state/responsiveness (e.g., self-contained HTML/CSS, images when owned/permitted, or another genuinely available tool); minimal JS only for a useful bounded interaction simulation; exact source, proof purpose, representative states/viewports, observed inspection, and **NOT RENDERED / NOT TESTED** where appropriate.

**A visual artifact is not a Product Contract, accepted UI authority, reusable Project Standard, implementation instruction, or real user evidence.** Material Human acceptance attaches to the exact reviewed UI meaning/revision, not just the mock being attractive. A project can legitimately implement a bounded UI change from effective design standards without producing new Hi-Fi artifacts if actual task information is sufficient.

## 7. Recommendation, scope and decision gate

**Strong recommendation:** Proceed with **two independent direct-entrypoint A3 concerns**, not a shared `design/` authority file:

1. **UI Definition:** retain experiment-led 13/9/9/6 semantics **conditionally**, with distinct bounded visual/component/copy/asset decisions, explicit visual-review evidence and acceptance standing.
2. **Project Design Standards Definition & Evolution:** define how genuinely reusable within-project standards are formed/maintained from evidence and legitimate Human decisions; **do not** invent fixed output counts or a universal list of standard files. Keep UI component/library creation distinct from standard promotion.

**Proposed next scoped implementation after Human decision:** draft four files under `design/ui/` and four under `design/project-standard/` on `research/cross-stage-mapping`. Update root README to route directly to both. Retire the two transitional root Design files only after successful semantic migration and link review. Avoid modifying A2 settled files, current Engineering Space definitions, Kencleng, `main` or frozen original.

**A3 audit status: `REVIEW_PENDING`.** This source-based proposal is **not accepted A3 owning guidance**. Needed for A3 closure: Human review of material A3 semantics; scoped owning-source authoring; direct-routing/inbound-link checks; authority/consumer and 13/9/9/6 validation; material residuals/independent runtime limits; no accidental project-standard promotion.

## 8. A3 consumer gap — compatibility correction after Human decision (2026-11-04)

Anhar accepted the **required-by-default O2 UX Flow Diagram and O6 Lo-Fi Wireframes baseline for new/material UX**, subject to evidence-backed exceptions and reuse of accepted existing equivalents. This corrects the initial A3-F02 risk of relying on optional producer outputs. See [UI 13-input → UX/other-owner compatibility matrix](a3-ui-input-to-ux-output-compatibility.md) for the complete experimental UI I01–I13 source/requiredness mapping and a proposed UI Input Sufficiency Check.

**Boundary:** This approval authorizes a scoped amendment to `design/ux/` research guidance. The `design/ui/` Input Sufficiency Check remains **A3 PROPOSAL / REVIEW_PENDING** until UI owning guidance is reviewed. Older O2/O6 optional language elsewhere above records the original A3 audit checkpoint and is superseded for ongoing recommendation by the amended UX baseline. No mandatory physical files or stage/Space invocation, no new project-wide Design Standards, no Kencleng or Engineering formation edits, and no actual runtime/UI consumer proof.

## 9. Subsequent UI-only owning-guidance draft (2026-11-04)

Anhar accepted exact scoped A2/UX amendment and 13-input source mapping at `8d53c1ac3baccb8e277382f2b583281ff89c8f51`, and authorized continuing **UI guidance only**, explicitly deferring Project Design Standards authoring. As a result, the four **independent self-contained `design/ui/` documents** were authored on the research branch at `44e513e0199ca9ea31e61a90b3f0760d8e1d0dc6`:

- [UI direct README](../../design/ui/README.md)
- [UI AGENTS](../../design/ui/AGENTS.md)
- [UI Definition](../../design/ui/definition.md)
- [UI Authority & Handoff](../../design/ui/authority-and-handoff.md)

The revised draft follows experiment-led **13 inputs / 9 iterative responsibilities / 9 logical outputs / 6 quality targets**, integrates the accepted UX O2/O6 required-by-default baseline, and proposes **UI Input Sufficiency Check** and **inspectable new/material UI visual evidence** before binding affected final UI decisions. Existing accepted target-project UI can be reused; static HTML / PNG / tools are conditional actual representations, not universal mandatory file formats or invocation permissions. UI-local component candidates do **not** silently become project-wide standard rules. Older 'no UI files authored' statements above record the earlier audit checkpoint and no longer describe the current research branch tree.

**Standing:** New `design/ui/` content is **A3 DRAFT FOR HUMAN REVIEW**, not accepted/settled, and no actual independent UI consumer, live browser/rendered tests, Kencleng project adoption, operational promotion, or Project Standard guidance creation is claimed. The root `design/exploration.md` and `design/authority-and-handoff.md` remain transitional reference pending their separate Project Standard review. See [audit tracker](audit-revision-plan-and-tracker.md) for exact A2 approval references and later source-level validation.
