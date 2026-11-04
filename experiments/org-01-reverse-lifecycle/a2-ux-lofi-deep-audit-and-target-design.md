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

## 4. Proposed target Design architecture — intentionally not final before A3

A2 should **not** decide all future UI Hi-Fi structure under the name of UX. The next target layout is a **candidate**, not a mandatory file schema:

- **design/README.md** — concern-level navigation, source standing, current capability/subject examples **only when actual**.
- **design/AGENTS.md** — lean authority-aware routing.
- **design/ux-definition.md** *(new candidate)* — reusable Interaction & Experience Definition I/P/O/O; conditional UX flows, IA/navigation, state and web route contract.
- **design/authority-and-handoff.md** *(shared candidate)* — effective Design decisions, exact-revision Human acceptance, responsibility-based information consumption, producer/consumer compatibility; review with A3 to avoid duplicating UI-specific authority.
- **design/exploration.md** — remain unchanged pending A3; decide later whether unique visual/brand exploration semantics belong in a future UI-specific core or common exploration guidance.
- **Future UI/Hi-Fi core** — intentionally deferred to A3, which evaluates the Hi-Fi experiment, not silently specified by A2.

**No new UX template yet.** Whether an optional template solves a concrete authoring/consumer problem should be shown before adding it. A project can use its accepted document shape; UX output types do not mandate new files.

## 5. Cross-responsibility boundaries and two critical tests

**Product vs UX:** Product User Journey gives actor/domain meaning, rights, consequential information and success. UX Journey and UX Flow give human interaction progression, information grouping, navigation and interaction behavior. UX never fabricates Product role authority, consent/legal status, or success semantics.

**UX vs Visual Interface Design:** accepted UX navigation, flow, IA and interaction-state obligations are consumable Design constraints; visual/interface expression can propose revisions but cannot silently replace binding UX decisions. Where webpage paths are accepted, any material technical infeasibility is a reconciliation finding for the Design owner; technical Engineering owns backend API routes, not automatic ownership of webpage navigation.

**Consumer input check:** Distinguish (a) generic fit with a real declared receiving Input Contract, if one exists, from (b) actual project-bound consumer fit, which is not proven here. Source inspection/authorization duties of a real consumer are not waived by an apparently self-contained UX handoff.

**Evidence check:** Prototype clickability, hypothetical scenario, accepted UX revision, independent accessibility check and observed real-user usability are separate evidence claims. Do not certify more than the actual method supports.

## 6. Recommended change direction and decision gate

**Strong recommendation:** Approve creation of a reusable **Interaction & Experience Definition** concern as the A2 target, using the experiment's 11 inputs / nine activities / nine logical outputs / six desired properties as a *conditional semantic reference*. Keep UX responsibility independent of the identity or existence of Product, Visual Design, Engineering Solution, or Engineering Development Spaces. Do **not** form a new UX Space or impose nine mandatory deliverables.

After Anhar's decision, propose bounded updates to **design/README.md**, **design/AGENTS.md**, a new **design/ux-definition.md**, and **design/authority-and-handoff.md** (only UX/consumer-related parts); leave **design/exploration.md** for A3 unless evidence warrants a smaller specific edit. Avoid rewriting or reapproving existing Engineering Space definitions in A2.

**Required for A2 settlement:** Human decision on material target semantics; source-branch research revision; diff/source/link checks; preservation of Product/UX/Visual/Engineering authority boundaries; explicit limitation of unverified consumer and real usability. Approval of A2 research guidance is not operational promotion or actual UX authority for Kencleng.

**Review status:** A2 is **REVIEW_PENDING**, not SETTLED_FOR_RESEARCH. No owning Design guidance has been changed by this audit.
