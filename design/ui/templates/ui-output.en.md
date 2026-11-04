# Template — UI Output & Consumer Handoff (English)

> **Standing:** A3 RESEARCH AUTHORING TEMPLATE / DRAFT FOR ANHAR REVIEW (2026-11-04). Not approved target-project UI Design, project-wide Design Standard, runtime/visual verification, a formed Space, or tool/write authorization.
> **Contract:** [UI Definition](../definition.md) · [UI Authority & Consumer Handoff](../authority-and-handoff.md). Other language: [Indonesian](ui-output.id.md).
> **Use:** One bounded UI output record, or a navigable index to existing project-owned artifacts. Nine logical outputs **O1–O9 do not mean nine mandatory files**. This template **does not replace actual visual artifacts** for new/material design.

## How to use

- First perform the **UI Input Sufficiency Check** on **I01–I13** as defined in [UI Definition](../definition.md#3-ui-input-sufficiency-check). Refer to real owning sources; do not recreate Product/UX/Project Design Standards as competing authority.
- For new/material visual UI, **O1 visual screen proof is required by default**; include affected **O3 responsive, O4 material states, O5 visual/component styles and O7 final UI copy**. Reuse exact accepted artifacts if sufficient; exceptions require scope, evidence, legitimate decision owner/delegation and consumer impact.
- O2 prototype is required **when material interaction cannot be adequately evaluated through static proof**; O6 reusable library and O8 assets depend on real need, not a file-count target.
- If an artifact lives in HTML/CSS, images, a prototype, existing Figma or other media, state its **path, exact revision, decision scope, visual inspection standing and evidence limits**. HTML in Git is not proof of browser rendering.
- Distinguish **NOT CHECKED**, **CHECKED (actual evidence)** and **HUMAN ACCEPTED exact revision**. Review and approval records may be separate so accepted bytes need not change merely to add a hash/status.
- Use `N/A — reason and scope` for genuinely inapplicable outputs, `OPEN — owner and consumer impact` for material gaps; never fill placeholders with guesses and claim READY.

## Web visual format — baseline v1

For **new/material web Hi-Fi**, use **static HTML + CSS by default**: **one `.html` per actual accepted UX webpage**, not one file per UI state. Keep default/loading/error/unknown, dialogs and other variants **within their owning page**. Use **relative preview links** between actual webpages, not JavaScript to swap entire distinct pages inside a single HTML. Preview filenames need not match production URLs. Share CSS when useful; use **minimal JS** only for necessary local interaction simulation, never real auth/API/data effects.

**Accepted existing equivalents, legitimately better project/tool constraints or non-web UI** can justify an evidence-backed exception. Record affected scope, actual constraint, exact artifact/evidence, legitimate Design owner/delegation and consumer impact; agent preference alone is insufficient. No universal folder/filename is mandated. See [UI Definition §7](../definition.md#7-visual-artifact-formats-verification-and-limits).

**Proof limit:** Git-hosted HTML/source is not browser verification. Record the actual page/state/viewport preview method only when performed; otherwise use `NOT VISUALLY VERIFIED` without claiming visual acceptance.

## 0. Identity, scope, input sufficiency & standing

| Field | Actual value / exact source |
| --- | --- |
| Project / bounded UI outcome / actor / intended decision | `<...>` |
| Actual UI decision owner / delegation evidence | `<actual target-project owner and reference>` |
| Intended functional consumer and decision | `<Engineering / verification / other, exact decision>` |
| Current project repo, branch and inspected baseline | `<path + immutable revision>` |
| Effective Product sources / accepted scope | `<project-owned paths + revisions + standing>` |
| Effective UX sources: O2 Flow & O6 Lo-Fi baseline | `<accepted paths/revisions, or legitimate evidenced exception>` |
| Applicable UX O1/O3/O4/O7 and web O5 | `<actual accepted source/revision or gap owner>` |
| Effective Brand/Visual/Component/Asset standards | `<project-owned paths/revisions and applicability; N/A if absent>` |
| Other material I01–I13 input decisions and gaps | `<applicable input IDs + source/owner; link source checks>` |
| UI candidate artifact(s) and source revision(s) | `<exact revision(s) when persisted; prior source if proposed>` |
| Web visual format and exception standing | `<HTML-per-actual-UX-webpage default / accepted exact equivalent / non-web / evidenced alternative + owner, scope, consumer impact>` |
| Binding UI input sufficiency | `SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED + per-decision reason` |
| UI content standing | `PROPOSED / ACCEPTED only with separate actual exact-revision evidence` |
| Exclusions, open decisions, risks | `<...>` |

**No silent UX substitution:** For new/material UX, UX O2 flow and O6 structural Lo-Fi are required by default. Send specific gaps to the UX owner. UI may explore independently but cannot claim acceptance of a visual decision dependent on unaccepted UX.

## Page-to-file preview mapping — required for new/material web Hi-Fi

| Accepted UX webpage / route + exact source | Preview HTML file + exact revision | Local relative navigation destination(s) | In-page state variants included | Render evidence / exception / open gap |
| --- | --- | --- | --- | --- |
| `<UX O5/O4 page and accepted revision>` | `<entry.html or equivalent + exact revision>` | `<relative hrefs corresponding to UX navigation>` | `<default/loading/validation/unknown etc. within this page>` | `<CHECKED with actual evidence / NOT VISUALLY VERIFIED / owner-backed exception>` |

**Page vs state:** Do not turn UI states into new webpages or simulate distinct entire webpages inside one HTML. This map only indexes visual proof; it grants no route authority. If already accepted in another medium, link exact accepted evidence and document the exception.

## 1. Visual evidence register — required for new/material UI

| Evidence ID | Linked source + exact revision | UI question / covered O-ID(s) | Screens / states / viewports actually included | Render/inspection standing and method | What this does NOT prove |
| --- | --- | --- | --- | --- | --- |
| VIS-01 | `<HTML/image/etc path + revision>` | `<O1/O3/O4/O5/O7 + question>` | `<...>` | `NOT VISUALLY VERIFIED / CHECKED + actual observation ref` | `<user test, API, accessibility, etc.>` |

**Required visual review boundary:** For new/material UI, prose or tables without inspectable O1 visual evidence are insufficient for the final visual decision. Renderer unavailable means **NOT VISUALLY VERIFIED** and an affected acceptance gap; never fabricate a rendering claim. Existing accepted visual proofs may be referenced if they truly cover the affected scope.

## O1 — Hi-Fi Screen Designs (default required for new/material UI)

| Screen/surface ID | Actor goal and accepted UX anchor | Visual composition, main content/actions and hierarchy | Visual evidence ref | Scope / accepted/proposed standing |
| --- | --- | --- | --- | --- |
| UI-SCREEN-01 | `<UX flow/IA/state source>` | `<...>` | `<VIS-01 + exact revision>` | `<...>` |

**Sufficiency:** `<new inspectable proof / already accepted equivalent + exact revision / evidenced no-impact exception>`. For a meaningful new visual decision, **do not merely describe the layout**.

## O2 — Interactive Prototype (conditional)

**Trigger:** `<interaction cannot be responsibly reviewed through static proof? YES / NO + concrete reasoning>`

| Prototype/ref | Actual simulated interactions and states | Source/evidence and inspection | Not proven / prohibited real effects |
| --- | --- | --- | --- |
| `<... / N/A>` | `<...>` | `<...>` | `<no real auth/API/data effects, etc.>` |

A clickable simulation does not prove Product behavior, acceptance, real users or integration. Minimal JS only if justified and authorized.

## O3 — Responsive Designs (affected scope required)

| Screen / state | Representative viewport / device context | Information priority, layout/reading order and overflow behavior | Visual evidence + actual inspection | Open limitations |
| --- | --- | --- | --- | --- |
| `<...>` | `<e.g. narrow/wide actual reviewed contexts>` | `<...>` | `<VIS-ID or NOT CHECKED>` | `<...>` |

No universally mandated breakpoint numbers; cover material affected behavior with evidence.

## O4 — UI Interaction States (material states required)

| UI state / trigger | Accepted UX/Product meaning and source | Visible copy/affordance/feedback, focus/recovery | State visual evidence | Actual inspection / exception |
| --- | --- | --- | --- | --- |
| `<loading / validation / denied / unknown / recovery / success, as applicable>` | `<...>` | `<...>` | `<VIS-ID>` | `<...>` |

Do not collapse pending, unknown, failed, success or verified when Product truth distinguishes them. Do not invent state transitions or backend results.

## O5 — UI Components & Styles (affected scope required)

| UI component / element | Existing approved precedent or scoped new candidate | Variant, typography/color/spacing/interaction appearance | Visual evidence / implementation freedom | Reusable standard status |
| --- | --- | --- | --- | --- |
| `<...>` | `<effective source / PROPOSED>` | `<...>` | `<...>` | `<feature candidate / existing standard>` |

Frontend component APIs/CSS/frameworks belong to Engineering. A local new variant does **not automatically** become a reusable project standard.

## O6 — Reusable UI Component Library (conditional)

**Reuse trigger:** `<repeated use evidenced across real project needs? YES / NO + concrete reason>`

| Candidate library/component | Actual repeated-use need | Owner/project-standard decision required | Scope, affected consumers & source standing |
| --- | --- | --- | --- |
| `<... / N/A>` | `<...>` | `<not automatically approved>` | `<...>` |

If not needed, do not build a large library or promote global tokens/styles without owner approval.

## O7 — Final UI Copywriting (affected scope required)

| Screen/state/element | Final candidate UI text, language and placement | Accepted Product/Legal terms, copy source and standing | Visual evidence / unresolved review |
| --- | --- | --- | --- |
| `<...>` | `<actual user-facing copy>` | `<...>` | `<...>` |

Consequential wording/legal disclosures remain owned by Product/Legal. Not all copy changes require new approval when legitimately delegated.

## O8 — Final Visual Assets (conditional)

| Asset/ref & intended purpose | Provenance/license/availability | Exact project source + standing | Actually inspected / fit & limitations | Required approval or remaining gap |
| --- | --- | --- | --- | --- |
| `<... / N/A>` | `<...>` | `<...>` | `<...>` | `<...>` |

Visual references, generated candidates, icons and brand assets are not automatically production-ready or approved. Never claim to have viewed pixels from a filename alone.

## O9 — Design Review & Acceptance References

| Decision ID / affected O-ID | Actual question, trade-off & review finding | Human decision/owner or OPEN | Exact reviewed UI artifact revision | Evidence gaps / exclusions |
| --- | --- | --- | --- | --- |
| UI-DEC-01 | `<...>` | `<PROPOSED / accepted with separate evidence>` | `<...>` | `<...>` |

**Approval record external to approved bytes.** A commit, filled template, rendered prototype or reviewer suggestion is not a substitute for actual legitimate Human acceptance.

## Consumer Handoff & Decision-Specific Completion — required

| Consumer / intended decision | Exact accepted project-owned UI evidence + Product/UX/Standard origins | UI constraints and delegated implementation freedom | Compatibility/verification status | Material gap / owner |
| --- | --- | --- | --- | --- |
| `<e.g. Engineering implementation of this screen set>` | `<exact refs/revisions>` | `<...>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED>` | `<...>` |

**Generic consumer Input Contract check:** `<actual applicable formed contract test, or NOT APPLICABLE>`

**Project-bound consumer check:** `<real project authority/security/accessibility/copy/asset/readiness and scoped acceptance, or NOT CHECKED>`

**Performed checks vs not performed:** `<actual inspected screens/viewports/states, source-only limitations, accessibility/user/API/runtime NOT CHECKED>`

**Next legitimate decision and owner:** `<...>`

**Nonclaims:** UI acceptance does **not** approve Product/UX changes, reusable project standards, API/security contracts, frontend implementation, deployment, runtime behavior, accessibility certification, asset licensing, or release. This template carries information, **not execution or write authorization**.
