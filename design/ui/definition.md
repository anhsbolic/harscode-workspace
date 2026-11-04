# UI Definition — Visual Interface & Content Design

> **Standing:** A3 PROPOSED RESEARCH DESIGN / REVIEW PENDING (2026-11-04). The direct `design/ui/` folder architecture is already approved, but this UI I/P/O/O and consumer contract are **newly authored drafts**, not accepted Harscode operational or project Design policy.
> **Basis:** [UI Hi-Fi I/P/O/O experiment](../../experiments/org-01-reverse-lifecycle/ui-design-hifi.md), [A3 evidence-based audit](../../experiments/org-01-reverse-lifecycle/a3-ui-and-project-standard-deep-audit-and-target-design.md) and [13-input compatibility mapping](../../experiments/org-01-reverse-lifecycle/a3-ui-input-to-ux-output-compatibility.md). These are research references. Actual target-project effective sources override any illustrative ORG-01 assumptions.

## 1. Purpose and boundaries

Visual Interface & Content Definition specifies **how accepted Product and UX meaning is visually and linguistically expressed in relevant UI surfaces**, with appropriately inspectable evidence for actual Design and Engineering consumption.

UI owns scoped screen composition, hierarchy, typography/color/spacing expression within project direction, responsive presentation, visually communicated states, designed components/variants, final bounded UI copy and used/proposed visual assets. It can propose a new visual direction when duly delegated. **Hi-Fi** is a fidelity/representation choice, **not** one required agent, Space, deliverable file or mandatory phase before implementation.

- **Product** owns actor/domain meaning, business eligibility/constraints, consequential information, privacy/legal requirements and truth of outcomes.
- **UX** owns actor interaction progression, IA, navigation/webpage paths, structural Lo-Fi baseline and user-facing interaction/state obligations.
- **UI** owns visual/interface expression of accepted meaning and bounded visual evidence/acceptance.
- **Project Design Standards** owns approval and evolution of **reusable cross-feature/project-wide** design rules. UI may propose candidate components and patterns, not promote them automatically.
- **Engineering** owns DOM/framework/CSS/API/security/data/implementation mechanisms and performed integrated runtime verification.

Actual responsibilities can be performed by authorized subjects without one-to-one Spaces or mandated producer/consumer execution order.

## 2. INPUT — 13 decision-specific information needs

| ID | Input | Required information, source and trigger |
| --- | --- | --- |
| **I01** | **UX Flow Diagram** | Accepted relevant interaction progression, branches, exit/recovery, exact revision from **UX O2**. **Required by default** for new/material UX-driven UI work; use accepted equivalent or justified scoped exception, not unapproved UI-inferred flow |
| **I02** | **Lo-Fi Wireframes** | Representative accepted UX screen/surface structure and information priority from **UX O6**, informed by IA/navigation/states. **Required by default** for new/material screen UX; existing accepted equivalent/evidence-backed non-applicability may suffice |
| **I03** | **Webpage Map & Route Specification** | Accepted UX **O5/O4** page paths/purposes, entry/exit and page-vs-UI-state meaning **when material web routing applies**. Distinct from Engineering API routes |
| **I04** | **Product Requirements & Business Rules** | Binding actor, consequential fields/actions, eligibility, consent/privacy, validation and success/failure/unknown meaning from **effective target-project Product authority** |
| **I05** | **Screen Content & Information** | Exact consequential Product disclosures/fields and UX O3 information hierarchy/timing; UI may own nonconsequential wording within legitimate delegation |
| **I06** | **UI States & Interaction Requirements** | UX O7 user-facing state/interaction requirements (with Product meaning and known technical constraints) for real validation, loading, denied, error, incomplete, success, unknown and recovery |
| **I07** | **Brand & Visual Guidelines** | Applicable accepted project Brand/Visual Standards; if none, explicit bounded freedom or material direction-owner decision where needed; no new default Harscode palette/style |
| **I08** | **Responsive & Accessibility Requirements** | Applicable project accessibility/device requirements and UX O3/O6/O7 structural/focus/read-order priorities; UI responsible for visual adaptation and evidence |
| **I09** | **Design Quality / Anti-AI-Slop Criteria** | Applicable project requirements plus evidence-based craft criteria: clarity, purposeful visuals, natural copy, legibility, information density, truthful cues; not mandatory aesthetic-scoring bureaucracy |
| **I10** | **Existing Design System & UI Component Library** | Effective project-owned reusable components/tokens/variants **if available and applicable**, with actual standing; code alone isn't a Design Standard |
| **I11** | **Web Assets** | Required legitimate logo/icon/illustration/image/font assets, ownership/licensing/provenance and approved intended use; nonessential assets are not blockers |
| **I12** | **Visual References / Moodboard** | Supporting direction evidence when relevant; **inspect actual images** before asserting visual equivalence; selected proofs are not automatic pixel or production specs |
| **I13** | **Usability Research / User Feedback** | Applicable real findings when available; mandatory if a material decision/claim genuinely relies on them; absence does not mean successful usability |

**Thirteen inputs are information categories, not thirteen mandatory upstream files, owners, stages or invocation gates.** For applicability and missing-input owner, use the research [compatibility map](../../experiments/org-01-reverse-lifecycle/a3-ui-input-to-ux-output-compatibility.md) as **supporting provenance**, while the owning **target-project originals** remain binding.

## 3. UI Input Sufficiency Check

Before accepting **material, binding Hi-Fi decisions** (not before every low-risk exploration):

1. **Classify scope:** new/material UX experience, changed material UI expression, or small UI refinement with already accepted applicable UX/UI and standards?
2. **Check binding information:** actual Product outcome/content rules, accepted UX O2 flow and O6 representative Lo-Fi **by default for new/material UX**, O1/O3/O4/O7 information, conditional O5 web paths, and applicable Design Standards/responsive/accessibility. For existing sufficiency, pin the **actual exact accepted source**; do not demand fresh artifacts. Exceptions require affected O-ID, concrete reason/evidence, legitimate owner/delegation and receiving-consumer impact.
3. **Check ownership/conflicts:** Product meaning cannot be selected in UI; UX flow/route/state meanings cannot be silently redesigned; project reusable Design rules can't be invented. Return each material gap to its **actual owning responsibility**.
4. **Check proof standing:** proposed diagram/Lo-Fi, accepted UX, source-level UI candidate, rendered screens, browser-tested interactions and independent user/accessibility evidence are **different kinds of evidence**.
5. **Disposition for affected UI decision:** `SUFFICIENT` (actual accepted applicable sources), `CONDITIONAL / PROPOSED` (bounded visual exploration allowed but not binding), `BLOCKED` (material original-source/authority gap prevents final decision), or `UNVERIFIED` (a check not performed). This is a **decision-specific description**, not a global workflow state machine.

**Binding edge:** If UX O2/O6 is missing for a genuinely new/material screen experience, a prose-only UI interpretation cannot substitute for the default required representation. The UX owner must provide accepted coverage or an evidence-based exception before **dependent UI acceptance**. Unrelated authorized UI exploration may continue. Missing Brand/Visual project authority may permit a clearly labeled scoped visual **proposal**, not auto-approval of a brand-defining precedent.

## 4. PROCESS — Nine iterative UI responsibilities

1. **Screen & Content Planning:** choose in-scope UI surfaces, information timing, content slots, first-read hierarchy and consequential pre-effect disclosures using accepted Product/UX meaning.
2. **Visual Direction:** derive or propose composition, typography, color, density, atmosphere, trust/provenance grammar and appropriate contrast within effective project standards; expose material unapproved direction.
3. **UI Component Design & Management:** prefer applicable accepted project components; design scoped new variants/states and composition where justified. Treat a proposed reusable library as **candidate**, not effective project Design Standard.
4. **Hi-Fi Screen Design:** create/verify actual scoped visual treatments of required surfaces, not a speculative all-feature screen inventory.
5. **Responsive Design:** preserve meaningful content/action/read order and UX priority across relevant narrow/wide contexts; avoid treating pixel breakpoint numbers as semantic authority.
6. **Interaction & UI State Expression:** express applicable validation, focus, loading, denied, incomplete, failure, unknown, recovery and legitimate success visually without inventing their underlying Product/domain behavior.
7. **UI Copywriting & Visual Assets:** refine natural, contextual language consistent with accepted legal/Product terms; use justified, licensed and approved/clearly proposed imagery/icons/logos/fonts.
8. **Interactive Prototyping (when required by decision):** simulate material transitions or feedback that **cannot be adequately evaluated in static evidence**; make simulations conspicuous and avoid real API/auth/data effects.
9. **Design Review & Refinement:** inspect actual representative visuals/responsiveness/states, apply grounded craft/accessibility/truthfulness criteria and legitimate Human feedback; record what was actually checked or missing.

These are **responsibilities, not nine mandated sequential tasks**. When the project already has sufficient accepted UI, reuse it. “Anti-AI Slop” is a prompt for **purposeful, non-generic, actor-relevant craft**—not permission to overwrite project visual identity or invent extra review gates.

## 5. OUTPUT — Nine logical UI results

| ID | Output | Meaning and sufficiency |
| --- | --- | --- |
| **O1** | **Hi-Fi Screen Designs** | Scoped, reviewable **visual** composition of material screens/surfaces, aligned to actual accepted UX/Product and effective design direction. **Required by default for new/material visual UI design**, unless existing accepted equivalent suffices or justified inapplicable/unaffected scope |
| **O2** | **Interactive Prototype** | Conditional simulated interaction proof when dynamic UI choices, state navigation or recovery cannot be responsibly reviewed from static views alone; not real runtime/user success proof |
| **O3** | **Responsive Designs** | Relevant visual adaptations demonstrating preserved information/action hierarchy, reading order, clipping/overflow handling and accessibility. **Expected for affected responsive scope**, by new or existing accepted evidence |
| **O4** | **UI Interaction States** | Visually expressed material default/loading/validation/denied/error/partial/unknown/recovery/success states anchored to accepted UX/Product truth; combined with O1/O3 when practical |
| **O5** | **UI Components & Styles** | Enough scoped component/variant and typography/color/spacing/style decisions for target consumers; reuse effective project design system when available |
| **O6** | **Reusable UI Component Library** | **Conditional design-level candidate** when repeated cases justify shared components/variants; becomes an **effective project-wide rule only through legitimate Project Design Standard authority** |
| **O7** | **Final UI Copywriting** | Actual UI wording and placement in scope, natural and localized, with exact Product/Legal/content constraints preserved and approval standing stated |
| **O8** | **Final Visual Assets** | Applicable approved assets or clearly labeled bounded candidate assets/references, provenance/licensing and limits; no fake identity/verification and no automatic canonical brand asset |
| **O9** | **Design Review & Acceptance Record** | Scoped actual Human dispositions, inspected exact visual/UI artifact revision(s), limits, impacted decisions, open gaps and consumer-ready pointers; artifact and approval evidence may be stored separately |

**Quality baseline for new/material UI:** O1 **inspectable visual screen proof**, O3 **relevant responsive coverage**, O4 **material state examples**, O5 **visual/component expression** and O7 **actual user-facing copy** must be discoverable to the extent applicable. They can be combined in one artifact or reused from sufficient accepted project evidence. Missing proof is a **gap for the affected binding UI decision**, not a reason to label it accepted. O2 interactive prototype is **trigger-required** when interactivity is material and cannot be judged from static proofs; otherwise document that actual condition rather than creating a fake demo. O6 library and O8 assets are conditional on real need. O9 is needed for material Human acceptance, not to rubber-stamp every delegated styling adjustment.

**Nine logical outputs do not imply nine separate files, one universal Hi-Fi prototype, or a required UI Space.** The receiving engineer can consume accepted project-owned originals directly, without a second master UI spec.

## 6. OUTCOME — Six design-level properties

| Property | Desired design effect |
| --- | --- |
| **Clear** | Important screen goals, information and next actions are understandable without hidden hierarchy |
| **Intuitive** | UI expressions fit accepted UX interactions, feedback and recovery without misleading affordances |
| **Informative** | Consequential information is available at the right decision moment, not hidden by decorative hierarchy |
| **Transparent** | Visual/copy treatment distinguishes verified, provided, inferred, denied, pending, failed and **unknown** states according to Product truth |
| **Accessible** | Applicable contrast, focus, keyboard/screen-reader semantics and responsive ordering are meaningfully considered and checked when possible |
| **Visually Coherent** | Intentional, project-aligned type/color/spacing/composition/assets; no gratuitous filler or generic design-system proliferation |

These are **quality targets**, not proved independent usability, rendered correctness, accessibility certification, approved project UI, deployed software or delivered user outcome.

## 7. Visual artifact formats, verification and limits

**Default durable handoff:** Markdown with links to effective project sources and real visual evidence. For **new/material web Hi-Fi**, the standard new visual proof is **static HTML + CSS, one `.html` file per actual webpage defined by the accepted UX Webpage Map/Routes**. This is a default with **evidence-based exceptions**, not a universal production folder or a mandatory named UI/UX Space.

### Web visual artifact baseline v1 — approved direction

| Decision | Web proof default | Boundary |
| --- | --- | --- |
| **Pages** | **One HTML file per actual accepted UX webpage**; connect separate preview pages through relative links | Preview filenames may differ from production URLs; do not invent, merge or split authoritative UX page/route meanings |
| **States** | Keep default/loading/validation/error/denied/unknown/success, dialogs and overlays **within their owning page** | Do not make a file per UI state; do not simulate distinct webpages by JavaScript replacing whole-page content in one HTML by default |
| **Styling** | Use CSS local to the bounded proof; a shared `styles.css` is appropriate when multiple pages benefit | No mandated physical directory or CSS architecture; follow effective target-project styles/tokens |
| **Interaction** | Minimal JavaScript only for material local UI state/interactions that need simulated behavior | No real API, authentication, payment/data mutation, external effects, cookies, credentials or personal data without separate authorization |
| **Assets** | Use permitted project-owned/approved assets or clearly labeled candidates with provenance and licensing | No fabricated identities, verification, branding or filler visual evidence |
| **Review/handoff** | Markdown output index maps each real UX page/route to preview file and its state/viewport visual evidence | A committed HTML file, screenshot or filled template is not automatically Human-accepted or browser-tested |

**One-page vs one-state rule:** When UX defines two **actual navigable webpages**, the new default visual proof uses **two HTML files** and local relative preview links. In-page variants live in their respective page. Do not invent/rename UX web routes to fit this file structure. A sufficient existing accepted equivalent or a legitimately authorized project/tool format may replace this default **only with a recorded task scope, actual constraint, equivalent inspectable proof, legitimate Design owner/delegation and consumer impact**. Agent convenience alone does not justify skipping it. For non-web UI, use the appropriate inspectable native/project medium instead of forcing HTML.

**Illustrative only**, not a prescribed project directory or page list:

```text
ui-candidate/
├── entry.html
├── form.html
├── review.html
├── styles.css       # if shared styles help
├── preview.js       # only if simulation requires it
├── assets/          # if actually needed/permitted
└── handoff.md       # optional reference to UI output record
```

**Rendering:** Inspect actual pages, relevant material states and representative narrow/wide widths in an *authorized* browser/preview when possible. Record exact source revision, inspected evidence, method and limits. If not performed, mark **`NOT VISUALLY VERIFIED`**; HTML in Git is not a rendered inspection. A static simulation cannot prove accessibility certification, independent user usability, Product/domain correctness, actual API/backend behavior or release readiness.

**Authority:** Source Product truth and accepted UX navigation/page-vs-state meaning are binding in their concerns. Scoped UI visual evidence cannot silently become Product/UX approval, Engineering specification, reusable project-wide Design Standard or approved brand asset. Use exact Human-reviewed revision/scope and preserve unresolved evidence gaps.

If an essential visual proof cannot be made inspectable with permitted tools, report the affected final-acceptance gap and supply the closest legitimate representation; never substitute text-only claims for material visual verification.

## 8. Functional consumer sufficiency and completion

For actual receiving Engineering/Design work, make discoverable: **bounded UI surfaces and UX/Product original sources; accepted style/copy/asset constraints; material screen/state/responsive visual evidence; exact candidate/accepted revisions; Human decision standing; actual rendered/interaction checks; freedom left to Engineering; material unresolved owners**.

Do not require a fixed `ui-contract.md`, one prototype per screen, all nine outputs as physical artifacts, a named Engineering Space invocation or a new project-standard library. The applicable original target-project sources remain authority; UI handoff is a concise navigable bridge, not rival Product/UX/API truth.

A UI design can be sufficiently accepted for a bounded UI question while Engineering implementation, API availability, integrated runtime verification, user accessibility checks or product release remain independently blocked. See [UI Authority & Handoff](authority-and-handoff.md) for exact-revision approval and consumer compatibility.

**Final rule:** UI must visually express **existing legitimate meaning** with inspectable evidence at the consequence level of the decision; no aesthetic polish can confer Product, UX, Engineering or Project Standard authority.
