# Template — UX Output & Consumer Handoff (English)

> **Standing:** DRAFT FOR HUMAN REVIEW, reusable **research authoring aid** only (A2, 2026-11-04). Not an approved target-project UX artifact, Design Standard, formed Space contract, Human decision or write authorization.
> **Contract references:** [UX Definition](../definition.md) · [UX Authority & Handoff](../authority-and-handoff.md).
> **Language equivalence:** English translation of the Human-approved Indonesian research authoring template at `1658b5d` (blob `82c7e670d386142993f6588d096cdc0bbb8c67ec`). The English translation itself is newly authored **DRAFT FOR HUMAN REVIEW**, not independently approved.
> **Use:** One bounded UX artifact (or an index of actual project-owned sources) for the **information and decisions needed by a real consumer**. Nine logical output types (O1–O9) are coverage prompts, **not nine mandatory files or nine obligatory sections**.

## How to use

- Provide **identity, sources/standing, scoped UX decisions, material interaction states, unresolved gaps, and consumer needs** to the level needed for the actual decision.
- Use **exact references to project-owned sources** when sufficient outputs already exist; do not duplicate authoritative Product, UX, or Project Standard meaning into a competing specification.
- For inapplicable outputs, write **N/A — brief reason**. For material unresolved outputs, write **OPEN — owner and affected decision**. Do not fill placeholders with assumptions and then claim READY.
- If a prototype, UX Flow, wireframe, or route map resides in a separate file, link the exact revisions and state its authority and evidence limits. **Lo-Fi is an optional form of proof**, not a prerequisite for UI or Engineering.
- **A completed template is not approved.** Record Human approval of the exact artifact revision separately so accepted bytes are not modified merely to insert a status or SHA.

## 0. Identity, scope & effective sources — required for binding consumption

| Field | Actual value / source |
| --- | --- |
| Project / bounded outcome / UX question | `<...>` |
| Intended functional consumer and decision | `<e.g. visual interface design deciding navigation/state expression>` |
| Legitimate UX decision owner | `<actual project authority / delegation source>` |
| Product authority and bounded scope | `<path + immutable revision + standing, or HYPOTHESIS / not binding>` |
| Applicable project Design Standards | `<effective paths + exact revisions / N/A with reason>` |
| Other material input and constraints | `<a11y, device, security/privacy, verified technical facts, research, etc.>` |
| This UX artifact / referenced output revisions | `<path + immutable revision when available>` |
| Decision standing | `EXPLORATORY / PROPOSED / ACCEPTED only with separate exact-revision evidence` |
| Material exclusions / non-claims | `<...>` |

The current effective status is established by **actual project-owned approval evidence**, not by editing this table. Where approval has not happened, keep proposed meaning explicitly provisional.

## O1 — Actor Scenario & UX Journey

**Bounded actor goal and entry context:** `<...>`

| UX moment / actor goal | Relevant information encountered and understood | Decision/action | Consequence and accepted Product source | Alternate / recovery |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<reference, not invented policy>` | `<...>` |

Actor scenario and UX Journey concern **interaction experience**, not new Product domain rules or legal/role standing.

## O2 — UX Flow

**Diagram/prototype link or concise flow representation:** `<exact path / revision / N/A>`

| Flow ID | Trigger / precondition | Interaction decision and branch | Exit / failure / unknown / recovery | Decision standing |
| --- | --- | --- | --- | --- |
| FLOW-01 | `<...>` | `<...>` | `<...>` | `<proposed/accepted ref>` |

Do not invent backend ordering, APIs or success semantics to make the flow look complete.

## O3 — Information Architecture (IA)

| IA ID | Person's current question / decision | Needed-now information / timing | Additional accessible detail and placement | Product/Design source |
| --- | --- | --- | --- | --- |
| IA-01 | `<...>` | `<...>` | `<...>` | `<...>` |

Distinguish mandatory pre-effect disclosures, information discoverable on demand, and nonessential repetition. UX selects priority/structure; Product owns consequential information meaning.

## O4 — Navigation Structure

| Surface / navigation node | Entry and destination / return | Purpose and information access | Relevant alternate/error states | Standing |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Scope:** `<web / native / service / other>`. Not every interaction requires page-to-page navigation.

## O5 — Webpage Map & Route Specification (conditional)

**Applicability:** `APPLICABLE / N/A — reason`

| Web path / page | Purpose and actor entry | Navigation to/from | Page vs in-page state | Accepted/proposed revision |
| --- | --- | --- | --- | --- |
| `<route if genuinely applicable>` | `<...>` | `<...>` | `<...>` | `<...>` |

**Web page paths are UX navigation decisions; not backend API endpoints or mandatory router/Next.js implementation details.** Do not invent paths for a non-web scope.

## O6 — Structural Lo-Fi Proofs (conditional)

**Applicability:** `APPLICABLE / N/A — reason`

| Wireframe / structural artifact | UX question tested | Covered surface/state | Actual inspection/evidence and exact ref | Limitations |
| --- | --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` | `<...>` |

A low-fidelity image or mock is not itself an accepted UX decision; its scope, source and standing matter.

## O7 — Interaction & UI State Requirements

| STATE ID | Actor action / situation | User-visible meaning and allowed action | Error / denied / partial / unknown handling and recovery | Accessibility / UX requirement | Product source / standing |
| --- | --- | --- | --- | --- | --- |
| STATE-01 | `<...>` | `<...>` | `<...>` | `<focus, keyboard, screen-reader, device, responsive priority>` | `<...>` |

Include only **material** states, such as empty, loading, validation, permission, failure, unknown result, recovery and legitimate success. A timeout is not evidence of confirmed success or confirmed failure. Do not invent Product or backend states.

## O8 — Interactive Prototype & UX Evaluation (conditional)

**Applicability:** `APPLICABLE / N/A — reason`

| Prototype / evaluation evidence | Real UX question | Actually inspected flows/states | Method and finding | Not proven |
| --- | --- | --- | --- | --- |
| `<path + revision, or NONE>` | `<...>` | `<...>` | `<walkthrough / heuristic / independent user check / a11y check>` | `<runtime / usability / accessibility / etc.>` |

A synthetic clickable demo may substantiate **interaction feasibility at that fidelity**; it cannot prove real user comprehension, API success, security, or implemented accessibility without performed evidence.

## O9 — UX Review & Decision References

| Decision ID / affected output | Proposed decision or question | Real Human disposition / standing | Evidence / trade-off | Immutable reviewed artifact or pending reference | Remaining scope |
| --- | --- | --- | --- | --- | --- |
| UX-DEC-01 | `<...>` | `<PROPOSED / HUMAN-ACCEPTED only if actual evidence>` | `<...>` | `<...>` | `<...>` |

**Approval evidence is external to approved artifact bytes.** Do not fill an APPROVED label or SHA inside an already accepted UX artifact and claim an earlier decision still covers the revised bytes. If acceptance predates persistence, preserve the immutable reviewed snapshot and check exact persisted equivalence.

## Consumer Handoff & Decision-Specific Sufficiency — required

| Consumer responsibility / intended decision | Required approved UX meaning and exact source | UX/other-concern delegated freedom | Material gap / owner | Compatibility / evidence standing |
| --- | --- | --- | --- | --- |
| `<visual interface / engineering solution / implementation / verification / standard proposal>` | `<...>` | `<...>` | `<...>` | `<SUFFICIENT / CONDITIONAL / BLOCKED / UNVERIFIED + reason>` |

**Generic receiving contract check:** `<actual declared contract result, or NOT APPLICABLE>`

**Project-bound consumer check:** `<actual scope, source/approval/security/standard checks, or NOT CHECKED>`

**What is not being claimed:** `<e.g. rendered fidelity, independent user test, implementation/runtime verification>`

**Next legitimate decision and owner:** `<...>`

Do not create a second authoritative Product/Design Standard master or hide mandatory obligations in unapproved prototype files. This UX output is a bounded information/decision vehicle, **not permission** to invoke a Space, modify protected files, approve UI, adopt a project-wide standard, deploy code, or claim a delivered actor outcome.
