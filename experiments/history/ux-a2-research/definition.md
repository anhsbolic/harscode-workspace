# UX Definition — Interaction & Experience Design

> **Standing:** A2 PROPOSED RESEARCH DESIGN / REVIEW PENDING, 2026-11-04. The folder architecture is approved; the UX semantic contract below still requires Anhar's review. Not operational policy, a formed Space, or project UX authority.
> **Basis:** [A2 evidence-based audit](../../experiments/org-01-reverse-lifecycle/a2-ux-lofi-deep-audit-and-target-design.md) and its challengeable [UX Lo-Fi working experiment](../../experiments/org-01-reverse-lifecycle/ux-design-lofi.md).

## 1. Purpose

Define **how an actor encounters, understands, navigates, interacts and recovers** through a bounded experience without changing legitimate Product meaning.

**Product User Journey** = Product-owned meaningful domain progression/actor rights/outcomes. **UX Journey** = actor experience of information, decisions and actions. **UX Flow** = concrete user interaction/navigation transitions. These may relate but are **not interchangeable**. UX owns flow, IA, navigation and interaction meaning; not Product policy, visual styling, design standard promotion, backend API paths or implementation mechanisms.

**Lo-Fi is a representation/fidelity method, not a mandatory phase or Space.**

## 2. INPUT — 11 information needs

| # | Input | Necessity and authority |
| --- | --- | --- |
| 1 | Product Intent & Selected Outcome | Bounded value and scope, accepted or explicitly hypothesized for exploration |
| 2 | Actor Definition & Goals | Actor context, needs and actual goals; evidence/hypothesis standing explicit |
| 3 | Product User Journey | Product-owned meaningful progression and negative/uncertain consequences relevant to UX |
| 4 | Product Requirements & Business Rules | Effective binding rules when material to accepted interaction; provisional only in exploration |
| 5 | Product Acceptance Criteria | Required for material interaction choices and truthful success; **not** executed test evidence |
| 6 | Content & Information Requirements | Product-owned consequential information, disclosure/provenance/verification duties; UX owns priority, placement and access |
| 7 | Accessibility & Device Requirements | Applicable device/input modalities, accessibility obligations, project standards |
| 8 | Existing IA & Navigation Patterns | Inspect effective patterns if available/relevant; existing UI is evidence, not automatic authority |
| 9 | Known Technical Constraints | Actual material, verified facts; no prerequisite Engineering Space invocation |
| 10 | User Research & Usability Findings | Consider available relevant evidence; absence does not justify usability claims |
| 11 | UX Patterns & Design References | Optional inspiration/support; authority only if project legitimately accepts them |

**11 inputs are information categories, not eleven files or eleven upstream producers.** Read effective project-owned sources directly; Human evidence, user research, Product and technical context may contribute concurrently. Bounded UX exploration may use clearly labeled Product hypotheses; material accepted UX decisions relying on Product obligations require accepted Product authority. Missing truth blocks only affected decisions.

Not universal prerequisites: Hi-Fi designs, finalized visual components, brand tokens, API/schema, backend solution completion or a preexisting prototype.

## 3. PROCESS — Nine conditional iterative activities

1. **Actor Scenario Analysis** — goals, context, expectations, effort and possible misleading inferences.
2. **UX Flow Design** — actions, decision points, alternatives, exit/re-entry and recovery paths.
3. **Information Architecture (IA)** — information hierarchy, grouping, priority, disclosure timing and discoverability.
4. **Webpage Map & Route Design** — pages, paths, entries/exits, navigation, page-vs-state distinctions **when web routing is material**; other surfaces use appropriate navigation structures.
5. **Lo-Fi Wireframing** — produce or verify representative structural screen/surface proofs **by default for new/material screen UX**; accepted equivalents or evidenced exceptions are documented for the affected scope.
6. **Interaction & State Design** — focus/keyboard, forms, feedback, validation, loading, empty, denied, failed, partial, uncertain and recovery behaviors where applicable.
7. **Lo-Fi Prototyping** — bounded clickable/simulated proof **when useful**, with explicit simulated-data limits.
8. **UX Evaluation & Refinement** — evidence-aware walkthroughs, accessibility checks, user research when available, risk/trade-off review and iteration.
9. **Human UX Review & Acceptance** — legitimate owner decision for material UX meaning, accepted scope, exact artifact and uncertainty.

Order is **not linear**. Existing effective UX may already be sufficient. Do not run nine gates to produce a label of completion.

## 4. OUTPUT — Nine logical UX meanings

### New/material UX work — required output baseline

**Applicability.** A new bounded experience or a material change to interaction progression, screen/surface structure, information priority, navigation or consequential states must establish the affected UX baseline before claiming consumer-ready UX. For a change to an existing experience, cover the affected scope, not the whole product. This is **required information and representation coverage**, not a mandatory upstream UX Space, sequential phase or separate file count.

- **O1 Actor Scenario & UX Journey, O3 IA, O4 Navigation Structure and O7 Interaction & UI State Requirements:** required decision-relevant meaning for the affected actor, surfaces and negative/unknown paths.
- **O2 UX Flow Diagram — REQUIRED BY DEFAULT** for new/material UX: an inspectable representation of material transitions, decisions, alternatives, exits and recovery. **Mermaid in Markdown is the default newly authored form**. A sufficient exact-revision accepted equivalent can meet O2 without duplication.
- **O6 Lo-Fi Wireframes — REQUIRED BY DEFAULT** for new/material screen/surface UX: inspectable representative structural screens, content priority, actions and affected states. **HTML/CSS is the default newly authored structural proof** when authorized tooling permits it. An already accepted equivalent may satisfy O6. A genuinely non-screen experience requires an evidence-based non-applicability record, not imaginary screens.
- **O5 Webpage Map & Route Specification — required whenever material web routing is involved.** O8 clickable prototype remains conditional on a specific interaction question. O9 records actual scoped UX review/decisions where acceptance is material.

**Exception rule (not an agent preference).** Either point to an *accepted and still-applicable exact-revision equivalent* that already supplies the output, or document which output and affected decision are genuinely inapplicable/unchanged, concrete source evidence, legitimate UX owner or delegated authority, and consumer impact. For a new/material screen experience, “optional”, “not needed”, and “no time” without evidence are not valid reasons to omit O2 or O6. A missing materially required UX output is a **consumer-discovered gap**; do not mark the affected UI decision accepted.

**Tooling limitation is not automatic exemption.** If Mermaid preview or an HTML browser is unavailable, provide the clearest permitted inspectable source/equivalent, record **NOT RENDERED / NOT CHECKED**, and retain the relevant visual-review evidence gap. A generated file is not evidence of rendered usability, accessibility, real API behavior or Product truth. UX owns the missing UX decision; Product owns missing Product meaning; the actual consumer can continue independent authorized exploratory work but not finalize a decision that depends on the gap.

**Format vs output:** O2/O6 are default *logical deliverable obligations* for material experience work, not mandatory newly created files in every UX task. One durable project-owned artifact may satisfy several outputs; no fixed invocation chain or nine-artifact packet is created.


| Output | What must be understandable when applicable |
| --- | --- |
| **O1 Actor Scenario & UX Journey** | Actor situation, UX progression, encountered information, meaningful decision/recovery; Product consequences traced to Product source |
| **O2 UX Flow Diagram** | **Required by default for new/material UX:** real flow branches, entry/exit, error/unknown and recovery; Mermaid default for new authoring, exact accepted equivalent or evidence-backed exception allowed |
| **O3 Information Architecture** | Grouping, content priority, disclosure/access, relevant provenance and relationship among required information |
| **O4 Navigation Structure** | Relevant surfaces, transitions, destinations and return/recovery relationships |
| **O5 Webpage Map & Route Specification** | Webpage paths, purpose, entry/exit, navigation and page-vs-UI-state meaning, **if routing applies**; not backend API routes |
| **O6 Lo-Fi Wireframes** | **Required by default for new/material screen UX:** representative structural surface/screens, hierarchy, actions and affected states; existing accepted equivalent or justified non-applicability allowed |
| **O7 Interaction & UI State Requirements** | User-facing interaction, validation, focus, loading/error/denied/unknown/recovery, accessibility and truthful action result |
| **O8 Lo-Fi Interactive Prototype** | Bounded, labeled simulation of interaction/navigation; conditional evidence, not server/real-user proof |
| **O9 UX Review & Decision Record** | Actual Human decisions, accepted scope/exclusions, exact reviewed revision(s), evidence and material unresolved matters |

Logical outputs **may be combined** in existing project-owned artifacts. They are not nine required files. O5 is an explicit Design information contract for **applicable web routing decisions**, not a new mandatory UI page list. When technical constraints materially challenge accepted webpage paths, reconcile with UX owner; Engineering owns backend API paths and implementation mechanics, not silent UX routing changes.

**Truthfulness:** Product determines whether an action can succeed or fail and what is known; UX determines how to show that meaning. A timeout with unknown mutation outcome cannot be labeled success or definitive failure without authoritative evidence. User-asserted, pending, verified and reported information should not visually collapse when distinct in accepted Product meaning.

## 5. OUTCOME — Six desired quality properties

| Quality | Target |
| --- | --- |
| **Goal-Oriented** | Supports real bounded actor goals, not internal workflow ceremony |
| **Intuitive** | Understandable actions, navigation, affordances and recovery |
| **Clear IA** | Information discoverable and appropriately prioritized at decision points |
| **Efficient** | Reduce non-value friction without concealing material consequences |
| **Trustworthy** | No misleading legitimacy, certainty, outcome, provenance or state claims |
| **Accessible** | Appropriate keyboard/focus, assistive interaction and responsive information priority |

Desired qualities are **not** user-tested evidence, accessibility certification, rendered implementation or actual delivered actor outcome.

## 6. Functional authority and consumer boundaries

**Product Definition** owns actor/domain goals, meaningful Product User Journey, binding consequential information, roles, business rules and acceptance. **UX** owns interaction choices, IA, navigation/web routes, state treatment and UX evidence. **Visual Interface & Content Design** owns final screen expression/copy/components; **Project Design Standards** owns reusable cross-outcome principles/patterns/brand/visual/asset standards; **Engineering Solution Design** owns technical feasibility, API/auth/state architecture; **Engineering Development** owns permitted implementation and observed runtime evidence.

These are **responsibilities, not named lifecycle phases, Spaces, teams or individuals**. Consumers may use accepted UX information without a named upstream UX producer. Material UX feedback can return to Product/UX/Standards/Engineering legitimate decision owners, never automatically amend their sources.

## 7. Artifact Representation & Tooling Constraints — UX Lo-Fi

> **Research format baseline:** Anhar approved the following format-selection direction on 2026-11-04. This scoped addition is for research review; it does not reapprove earlier UX artifact bytes or alter target-project Design authority.

**Choose the least complex representation that meets the decision AND the new/material required output baseline in §4.** For affected new/material UX, O2 and O6 are **required by default**; equivalent accepted outputs and evidence-backed exceptions do not require new files. Other visual/prototype representations remain conditional and are not separate authorities.

| Format | Default use / decision it makes clearer | Selection boundary |
| --- | --- | --- |
| **Markdown (`.md`)** | Default durable UX artifact: decisions, scenarios, flow/state tables, IA/navigation/route specifications, source links and handoff | Use text/tables alone when they communicate the relevant meaning sufficiently |
| **Mermaid fenced in Markdown** | Default for a newly authored **O2 required-baseline UX Flow**; also useful for journeys/branches, IA/navigation and webpage routes | For new/material UX provide O2 flow or an accepted equivalent / justified exception. Do not infer Product authority from diagrams |
| **HTML + CSS (`.html`)** | Default newly authored **O6 required-baseline Lo-Fi** representation for material screen/surface UX; hierarchy, disclosure and state coverage | Accepted existing equivalent or evidence-based non-applicability may suffice. Keep non-production; do not invent Hi-Fi styling or backend behavior |
| **Minimal JavaScript with HTML** | Conditional clickable simulation to investigate a specific interaction, branch or recovery question | Only if interaction is needed, tools and **authorized** preview/runtime are available, and simulated data/actions are explicit. Do not call real APIs, change project state, or trigger side effects by default |

An illustration, screenshot, SVG/PNG or external Figma artifact may be cited as **supplemental evidence when actually available and permitted**; none is required by this baseline. Avoid adding image-generation/Figma/tool dependencies merely to fulfill a file-format checkbox. If the preferred representation cannot be created or verified with available authorized tools, use the clearest sufficient Markdown fallback and record the limitation; **never fabricate a render, diagram check or usability result**.

**Format decision rule:** for **new/material experience work**, establish O2 (normally Mermaid) and O6 (normally HTML/CSS structural Lo-Fi) or inspect accepted equivalents/evidence-based exceptions; also cover applicable O1/O3/O4/O7 and conditional web O5. For a bounded task where accepted UX already suffices, Markdown source pointers/tables may be enough without creating a new diagram or wireframe. Minimal JavaScript stays optional and authorized. Multiple logical outputs may share one file; no universal interactive prototype, nine-file packet or named Space invocation.

**Authority and proof limits:** The owning UX decision must be identifiable by exact project source/revision and legitimate Human approval standing. Any diagram, wireframe or prototype is **a representation of a scoped decision or hypothesis**, not self-authorizing Product/UX policy. If representation and textual binding source conflict, record the contradiction and return it to the legitimate owner; do not silently let either override the other.

For each material representation, make discoverable: **covered logical UX output(s), artifact type/format, purpose/question, source path + exact revision (when available), standing, actual render/interaction verification (`CHECKED` with evidence / `NOT CHECKED`), simulated versus observed content, and proof limitations.** A Markdown/Mermaid source review is not a rendered visual inspection; a Git-tracked HTML file is not proof a browser rendered it; a clickable simulation is not independent user testing, accessibility certification, real API mutation or delivered outcome.

Apply target-project accessibility, privacy, security, licensing, repository and action-authorization requirements. In particular, avoid external libraries/assets/network and real credentials or data in a Lo-Fi proof unless the relevant project authority and actual tool/runtime explicitly permit them.

## 8. Sufficiency and completion

For a particular decision, find: accepted/provisional UX intent, effective Product constraints, relevant interaction/navigation/IA states, accessibility, authority/scope/revision, actual evidence, unresolved materially blocked edges and legitimate owner. **For new/material UX, check O2 diagram and O6 structural Lo-Fi coverage or accepted exact-revision equivalents/evidence-backed exceptions** before declaring affected UX consumer-sufficient. Do not generate redundant files once required content and proof are available.

An accepted UX design does not automatically approve Product, Hi-Fi, Project Design Standards, code, release or runtime validity. See local [UX Authority & Handoff](authority-and-handoff.md) for exact revision and consumer standing.

**Principle:** UX depends on the information and decisions needed, **not the identity or invocation of a preceding/following subject**.
