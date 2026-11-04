# Project Design Standards Definition & Evolution

> **Standing:** A3 PROPOSED RESEARCH DEFINITION / HUMAN CONTENT REVIEW PENDING (2026-11-04). Not target-project Design Authority, a required documentation system or Harscode operational policy.
> **Basis:** A reusable concern/authority model inferred from Design Standard evolution needs. The research supports a **minimal open semantic model**, **not** an independently proven numbered I/P/O/O contract or fixed artifact list. Source details from any individual target project remain owned by that project, not this guidance.

## 1. Purpose and decision boundary

**Project Design Standards Definition & Evolution** supports a target project's effective, reusable design decisions across features/contexts: **who owns the rule, when it applies, what evidence justified adoption, how it changes, and which actual consumers must reconcile it**.

A target project may distribute owning standards across Product Design Principles, reusable UX Patterns, Brand/Product UI direction, concrete Visual Guidelines/tokens, writing/terminology, accessible interaction/visual treatments and visual Asset Governance. **These are possible concerns, not mandatory file categories**. There is no Harscode-imposed project `docs/design/` structure, total number of standards, fixed lifecycle, component library or universal token schema.

The reusable rule owner is distinct from:
- **Product:** actor/domain/business/financial/legal/privacy truth and consequential status;
- **Feature UX:** accepted actor flow, information architecture, webpage path/navigation, states and Lo-Fi structure in bounded experiences;
- **Feature UI:** scoped visual screen composition, copy, variants, material Hi-Fi proofs and proposed components/assets;
- **Project Design Standards:** accepted **reusable project-level** design principles/patterns/brand/visual/copy/asset decisions and their evolution;
- **Engineering:** frontend component APIs, DOM/CSS/framework, backend/API, actual accessibility/runtime verification and production release.

A project-wide rule may constrain feature UX/UI; feature-specific work may suggest a generalizable candidate, **not accept it automatically**. Actual target-project owner/delegation and branch determine authority, never Harscode conversational recall.

## 2. INPUT — actual information necessary for a specific rule decision

Consult only what is material:

| Information | Owning original / when relevant |
| --- | --- |
| Project meaning and constraints | Actual current target-project Product authority, committed scope and legal/privacy/accessibility/security obligations; **always for rules whose meaning depends on them** |
| Existing Design Standards & standing | Project-owned effective authority routing; actual canonical/approved design originals, accepted revisions and scope; working supplements and superseded evidence **clearly distinguished** |
| Triggering observation or design need | Actual feature UX/UI outcome, recurring patterns, material inconsistent treatments or **specific cross-document contradiction**; show affected surfaces/consumers |
| Available design proof | Relevant rendered visual references, chosen direction, prototypes, screenshots, real tests, accessibility evidence and source-only limitations; none inherently approves new reusable policy |
| Consumer and change impact | Actual downstream UX/UI/Engineering owners, production component uses if relevant, representative risk cases, technical constraints and reversibility |
| Legitimate Human decision | Who can adopt/change the project-wide rule, approval/delegation, what exact scope/revision is reviewed and any protected-branch/write authorization |

**A helpful index is not a rival standards authority**; when it contradicts the owning original, reconcile through actual project ownership. Engineering code and historical implementation are observation/evidence unless the project has expressly accepted their contract or precedent.

## 3. PROCESS — six possible responsibilities, not a required workflow

1. **Locate owner and effective branch.** Find the project-original rule, current approval/standing and scope; avoid treating pilot/worktree authority as operational `main`.
2. **Classify whether change is needed.** Reuse accepted coverage; clarify stale reference/standing; keep one-off UI/UX local; identify a genuinely repeated cross-feature decision; or examine a justified modification/supersession. Make a **no-change conclusion** valid.
3. **Verify cross-concern integrity.** Check Product truth, existing project patterns/brand/visual/asset constraints, feature UX/UI decision ownership and whether a candidate might silently alter page semantics, trust/evidence language or real action effects.
4. **Evaluate evidence, costs and consumers.** Name why a reusable rule adds value, what otherwise breaks, affected consumers, downstream risks, accessibility/responsive and brand impact, reversible options and what testing has actually been performed. Scrutiny increases with semantic/security/brand/blast-radius consequence.
5. **Obtain the legitimate decision when needed.** Ordinary delegated editorial/source clarification can remain small; novel project-wide or meaning-changing precedent, brand-defining asset and material supersession need the real owner/Human. Pin exact reviewed scope/revisions; a commit alone is not approval.
6. **Persist/reconcile/verify only if authorized.** Change the smallest **target-project owning source**, update its routing/stale competing references and relevant consumers, distinguish new/replaced/remaining OPEN decisions, perform source-level checks and record unverified runtime/render/consumer proof.

These six responsibilities are **analytical capabilities, not six mandatory gates, agents, forms or state-machine transitions**. The path may end at step 2 with **REUSE — NO CHANGE**. A genuine urgent ambiguity may require owner clarification before further binding design, without stopping independent safe work.

## 4. OUTPUT — bounded rule outcomes, not file count

| Logical result | What it may be |
| --- | --- |
| **No change / reuse** | Relevant accepted original source, applicability and exact effective revision; no new artifact or approval ceremony |
| **Clarification/reconciliation** | A corrected stale/open/superseded claim, restored authority boundary or project-owned index; preserve original approved substantive decisions and identify actual current owners |
| **Candidate reusable standard** | Scoped PROPOSED principle/pattern/visual/copy/asset decision, known competing alternatives, evidence and proposed owner; not effective by existence |
| **Accepted effective change** | Actual **project-owned** rule or explicit standard adoption with legitimate decision owner, exact reviewed revision/scope, supersession and actual consumer impact |
| **Consumer information** | Navigable pointers to project originals, what changed/which surfaces are affected, implementation freedoms, evidence limits and material unresolved owners |

These may be a single updated paragraph, a scoped project-owned approval record, existing documentation and links, or no file changes. **Do not require a separate project-standard output template, duplicate standard registry, UI prototype, one file per category or mandatory standard package.** Use a separate acceptance record only when needed to keep exact accepted source bytes intact.

## 5. Desired outcomes and sufficiency

A healthy project Design Standards concern should make rules **discoverable, unambiguous, scoped, stable enough to reuse, reversible where practical, minimally governed and reconstructable from project originals without chat memory**. A fresh authorized contributor should know the actual owning source, current/working/superseded status and who can change it.

| Real decision type | Smallest sufficient resolution |
| --- | --- |
| Existing accepted rule covers current feature | Link effective source and consume it; no new standard |
| Older direction says OPEN after later concrete approval | Reconcile source standing and owning references, **not** repeat design selection |
| One feature design looks useful elsewhere | Keep candidate scoped; examine repeated semantic need before promotion |
| Multiple feature/UI consumers require a new common rule | Review proposed owner, actual usage/evidence, affected consumers and authorized scope; promote exact accepted project-owned rule |
| Proposed change is semantic, trust-critical, brand-defining or breaking | Strengthen Human review, downstream impact containment and actual verification; do not wave through as local styling |
| Runtime/browser/user evidence is absent | Name the limit **UNVERIFIED / NOT CHECKED** and do not imply consumer outcome proof |

**Feature-specific acceptance ≠ project-wide standard acceptance.** An approved UI component library design may be a **candidate source** for project-wide standards; production React components are Engineering-owned. Approved visual direction is not automatically a production asset or a pixel-level engineering spec.

## 6. Illustrative standard-evolution issue (not a project precedent)

Suppose a project first approves **brand direction** but leaves exact typography and colors open. A later, separately approved **visual system** establishes those values. The earlier document may still accurately describe what was open *at the time*, yet mislead current consumers if it continues to claim those values are open **today**. The narrow remedy is to reconcile its current-standing note or pointers to the later effective owner without reopening brand direction.

Similarly, if guidance and evidence are mixed in one authority index, clarify which sources are **canonical**, **working supplements** and **reference-only proofs**. These are **hypothetical decision patterns**, not an assertion that a named project's solution or document inventory should be universalized, and not proof of usability or runtime consumer fit.

## 7. Consumer fit and completion

For an actual current consumer, provide **only** what their decision needs: project/branch and exact source, applicable binding design rule, which decision was adopted/clarified/superseded, original Product/UX/UI ownership preserved, proof/standing limits, design freedoms left to actual consumers, and remaining conflicts/owners. If a declared consumer contract exists, check it. Otherwise do not invent one.

Source-level correctness means actual owner links and standing agree. **It is not** evidence of user comprehension, screen fidelity, independent UX/UI tests, brand recognition, production CSS, real asset licensing, runtime availability or successful deployment.

**Final rule:** maintain the smallest truthful and effective project-owned Design Standard; if no standard needs changing, **do not manufacture one**.
