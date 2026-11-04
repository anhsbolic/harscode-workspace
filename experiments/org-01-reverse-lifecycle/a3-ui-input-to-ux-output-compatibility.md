# A3 — UI Input → UX Output and Owning-Source Compatibility

> **Standing:** A3 CONSUMER CONTRACT PROPOSAL / HUMAN REVIEW PENDING (2026-11-04). Not approved design/ui/ guidance or target-project Design policy.
> **Sources:** [Experimental UI 13 inputs](ui-design-hifi.md), [A3 source audit](a3-ui-and-project-standard-deep-audit-and-target-design.md), and revised [UX Definition](../../design/ux/definition.md) at the currently authored research revision; A2 scope correction was approved in direction by Anhar and implemented for exact-content review.
> **Verification:** Source-level interpretation only. No actual UI consumer run, browser rendering, independent user evaluation, or project-bound approval is claimed.

## Contract interpretation

UI depends on **actual accepted information**, not a named prior UX Space or compulsory waterfall. For new/material UX experience work, **O2 actual UX Flow Diagram and O6 representative Lo-Fi Wireframes are required by default**, together with applicable O1/O3/O4/O7 and web O5. Existing accepted exact-revision equivalents fulfill the obligation without duplication; exceptions need the actual affected O-ID/scope, evidence, UX owner/delegation, and consumer effect. A missing renderer is a NOT RENDERED evidence gap, not an output waiver.

**REQUIRED** means binding material information must be available for the intended UI decision. **CONDITIONALLY REQUIRED** means mandatory when the described condition is true. **SUPPORTING** means useful evidence, not universally a blocking prerequisite. These are classifications of *information availability*, not of mandatory separate files or UI/UX lifecycle phases.

## Full 13-input matrix

| UI experiment input | What the UI consumer actually requires | Owning source / UX logical output where applicable | Requiredness & missing-input disposition |
| --- | --- | --- | --- |
| **I01 UX Flow Diagram** | Actual material interactions, branches, entry/exit, denial, unknown/recovery | **UX O2**, with O1/O7 context; accepted exact revision or newly authored Mermaid/equivalent proof | **REQUIRED BY DEFAULT** for new/material UX. Missing or unjustified omission → UX owner; affected final UI stays blocked |
| **I02 Lo-Fi Wireframes** | Representative structure, content priority, actions, screen/state coverage for material screen UX | **UX O6**, grounded in O3 IA, O4 navigation and O7 states; accepted equivalent or structural HTML/CSS | **REQUIRED BY DEFAULT** for new/material screen UX. No concrete proof/accepted equivalent or evidenced non-applicability → UX gap |
| **I03 Webpage Map & Route Specification** | Web page paths/purposes, entries/exits, navigation and page-vs-in-page-state meaning | **UX O5/O4** plus applicable project Product constraints; not backend API paths | **CONDITIONALLY REQUIRED** whenever material web routing applies; otherwise reasoned N/A. Missing paths → UX owner |
| **I04 Product Requirements & Business Rules** | Accepted actors, consequences, eligibility, conditions, success/failure and disclosure rules | **Project Product authority**; UX O7 expresses their user-facing consequences without redefining them | **REQUIRED when binding**. Missing rules → Product owner, never UI or UX invention |
| **I05 Screen Content & Information** | Required fields/disclosures/provenance and timing, screen IA/priority and available wording | **Product consequential information** + **UX O3/O1/O6** for priority/placement; UI owns authorized final expression | **REQUIRED for affected screens**. Missing meaning → Product; missing layout/priority → UX; ordinary wording within UI delegation |
| **I06 UI States & Interaction Requirements** | Applicable state transitions, validation, waiting, denial, incomplete/error/unknown and recovery treatments | **UX O7** + Product domain meaning + verified Engineering interface facts when material | **REQUIRED for material states**. Missing user-facing behavior → UX; domain claim → Product; technical fact → Engineering |
| **I07 Brand & Visual Guidelines** | Applicable accepted visual/brand language and scope of styling freedom | Actual **target-project Design Standards** or legitimate Human-delegated bounded UI decision; **not UX O1–O9** | **CONDITIONALLY REQUIRED** when standards exist/apply. New brand-defining direction needs owner decision; do not invent canonical style |
| **I08 Responsive & Accessibility Requirements** | Applicable devices, assistive interaction, focus/reading order and information priority | Actual project accessibility standards + **UX O3/O6/O7** + UI responsive visual responsibility | **REQUIRED for applicable UI scope**. Missing structural/a11y UX decisions → UX owner; no implied testing pass |
| **I09 Design Quality Criteria / Anti-AI Slop Guidelines** | Evaluability of clarity, hierarchy, typography, purpose of visual/copy and information density | Applicable **project Design Standards**, authorized review criteria and UI craft judgment | **REQUIRED quality concern**, not mandatory Anti-AI-Slop policy file or aesthetic score gate; findings must be grounded |
| **I10 Existing Design System & UI Component Library** | Effective reusable patterns/tokens/components/variants if they constrain new UI | **Project Design Standard / actually accepted UI library**, with its own approval standing; existing code is evidence only | **CONDITIONALLY REQUIRED if available/applicable**. Ordinary nonstandard UI choices may be delegated; shared new precedent goes to standard owner |
| **I11 Web Assets** | Assets, icon/logo/typography provenance and license when actually needed | Approved **project asset/Design authority**; UI may propose scoped candidates | **CONDITIONALLY REQUIRED for needed assets**. Nonessential asset absence need not block independent UI; no invented brand/provenance |
| **I12 Visual References / Moodboard** | Sufficiently inspected style/direction evidence for a material visual decision | **Project visual-reference evidence** or authorized exploratory source; not a default UX output | **SUPPORTING by default**; becomes **CONDITIONALLY REQUIRED** if accepted project direction or decision depends on inspected visuals. No claimed pixel fidelity without pixel review |
| **I13 Usability Research / User Feedback** | Available credible feedback about comprehension, navigation and errors | Actual research evidence; UX evaluation findings only when genuinely performed | **SUPPORTING by default**; **REQUIRED if a binding claim/decision explicitly depends on specific research**. Absence is NOT proof of usability |

## Proposed UI Input Sufficiency Check

Before **binding/final acceptance of a material UI decision**, the receiving UI responsibility must establish:

1. **Actual scope and sources:** Is this new/material experience UX or bounded UI work with sufficient accepted UX already? Which I01–I13 meanings are material, and what effective Product/UX/Design Standard source/revision owns each?
2. **UX baseline completeness:** Inspect O2 **flow diagram** and O6 **representative structural Lo-Fi** by default when new/material UX; use exact accepted equivalents or a reasoned, owner-supported exception. Inspect applicable O1/O3/O4/O7 and O5 if web routing is materially in scope.
3. **Truth and conflicts:** No invented Product consequences, webpage paths, unauthorized actions or status certainty. Distinguish UX-owned navigation/interaction from Product domain truth, Design Standards and Engineering implementation facts.
4. **Proof standing:** Is representation merely source text, rendered/visually checked, simulated, user-tested or not checked? Browser/source availability cannot imply usability or accessibility proof.
5. **Decision-specific disposition:** **SUFFICIENT** with exact sources; **CONDITIONAL/PROPOSED** for independent bounded visual exploration; **BLOCKED** for dependent final UI acceptance when material UX/Product/standard authority is missing; **UNVERIFIED** for unperformed checks. Record exact missing information and legitimate owner.

**Consumer gap rule:** UI can do independent authorized visual exploration, but it cannot silently fill missing O2/O6 or other accepted UX meanings, and cannot finalize affected Hi-Fi UI decisions on guesswork. The gap returns to the actual UX responsibility without mandatory re-running a particular agent/Space. No project-standard promotion, Engineering contract change or Product approval is implied.

## Decision standing and limits

This matrix is **A3 proposed UI input guidance**, whereas the **required O2/O6 UX producer baseline** is a scoped research amendment authorized in direction by Anhar. Exact amended UX bytes remain to be reviewed/validated. No real UI/UX consumer test has been performed. The current A3 audit's earlier optional O6 wording represents its original snapshot; this matrix is the proposed corrective interpretation.
