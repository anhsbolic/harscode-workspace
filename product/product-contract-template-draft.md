# Product Contract — Reusable I1 Template v0.1 (Draft)

> **Standing:** RESEARCH PROPOSAL / NOT APPROVED AS OPERATIONAL HARSCODE POLICY. This is a reusable **Product output authoring template**, **not** a new mandatory Rancang contract, Product Space, or runtime step.
> **Owning concern:** Harscode Product guidance. **Actual Product semantics, approved revisions, and local document conventions belong to the target project and its authorized Human.**
> **Consumer alignment:** Rancang `I1` at [formed v3 definition `4b49d0dd0db74cf34a927cadc938ae724676a75a`](https://github.com/anhsbolic/harscode-workspace/blob/4b49d0dd0db74cf34a927cadc938ae724676a75a/engineering/spaces/feature-solution-design/contracts.md) — approved for research formation, **not runtime-verified**. Rancang `I2` (Design/architecture/security), `I3` (repository/code/environment), and `I4` (Human-direct assignment/permissions) remain separate.
> **Research context:** Adapted from a Kencleng I1 template experiment. Kencleng-specific roles, entity semantics and acceptance remain **project-owned**, not generic Harscode requirements.
> **Language counterpart:** [Bahasa Indonesia — Product Contract Template v0.1](product-contract-template-id-draft.md). Both files use the same logical I1 sections; use one language per Product Contract, not duplicate binding project artifacts.
> **Design choice:** A consistent **logical content structure**, not a mandatory PRD extension, file count, tooling workflow or one-outcome-to-one-Space mapping. Use project-authoritative templates when they already meet the consumer contract.

## Artifact identity and authority

| Field | Required meaning |
| --- | --- |
| Product/project + bounded outcome | `<project, identifier, outcome>` |
| Authorized Product owner | `<Human/authority>` |
| Document standing | `DRAFT / PROPOSED / APPROVED`, based on actual evidence |
| Exact artifact revision | `<path + commit/blob SHA>` once the revision actually exists |
| Approval and scope | `<decision, approver, affected outcome, exact revision, date/source>`; `NOT APPROVED` until true |
| Owning sources and precedence | `<current Product source anchors + revisions; what is binding vs research/evidence>` |
| Applicability | `<project, scope, conditions, exclusions>` |
| Intended consumers | `<e.g. Rancang I1, Design owner; consumer-specific claims and limits>` |

An artifact does **not** become binding because it follows this template. A valid I1 requires **actual approved bounded Product meaning, behavior, acceptance and source revisions**, plus a real consumer compatibility check when used.

## 1. Product Outcome and Success Criteria

Describe **who**, **in what relevant situation**, **may do what consequential action**, **what changes in Product truth**, and **why that result matters**. State what this outcome does **not** automatically deliver.

**Outcome statement:** `<When ..., actor ... can ..., so that ... becomes actually true and meaningfully inspectable ...>`

**Success Criteria (SC):** Define the smallest set of **observable, outcome-level conditions** that jointly allow the Product owner to call this particular outcome successful. These must be *Product semantics*, not an assumed implementation recipe or growth metric.

| ID | Outcome-level condition for legitimate success | Material non-guarantee or boundary | Supporting source/decision |
| --- | --- | --- | --- |
| `SC-01` | `<what must actually be true>` | `<what this does not prove>` | `<exact source/revision, APPROVED or PROPOSED>` |

When outcome success requires several conditions **together**, say so explicitly. A condition that is material but merely proposed **blocks approval of that success claim** until the authorized owner decides. Metric/KPI targets are distinct from Product outcome success unless explicitly owned and relevant.

## 2. Actor Experience and Consequential Meaning

Capture only meaningful moments; **do not prescribe UI screens, authentication timing, API sequences, or interaction technology**.

| Moment | What the actor needs to do, know or validly infer | Product consequence / non-guarantee |
| --- | --- | --- |
| Entry | `<starting situation, claims, relevant uncertainties>` | `<actual starting truth>` |
| Before material effect | `<understand consequences, authority, limits>` | `<what is and is not yet in effect>` |
| Action | `<permitted consequential action and actor>` | `<legitimate result if conditions hold>` |
| Success and later inspection | `<what actor can understand and inspect>` | `<actual resulting state and durable meaning>` |
| Material denied/failed/partial/unknown paths | `<what differs from success>` | `<what must not be claimed>` |

Omit non-applicable rows with a reason; an illustrative experience does not create binding Product truth.

## 3. Approved Product Behaviors, Authority, and Invariants

| ID | Material behavior / semantic obligation | Actor authority and preconditions | Invariant / prohibited inference | Source + standing |
| --- | --- | --- | --- | --- |
| `REQ-01` | `<what Product must do/mean>` | `<real actor, authority, state>` | `<what cannot be falsely implied>` | `<exact source, approved/proposed>` |

A binding Product Contract must not silently include material **PROPOSED** rules. Resolve the owning Product decision or narrow scope and update linked success/acceptance accordingly. Design and Engineering remain free to choose authorized implementation mechanisms.

## 4. Acceptance Criteria and Boundary Cases

**Acceptance Criteria (AC)** evaluate whether the intended behavior actually satisfies Product rules and **Success Criteria**. Success Criteria define *when the outcome is successful*; AC define *what observations would establish or falsify those claims*.

| ID | Requirement + Success Criteria traced | Scenario / material negative or unknown path | Observable pass/expected result | Invalid claim to prevent |
| --- | --- | --- | --- | --- |
| `AC-01` | `REQ-01 / SC-01` | `<positive/failed/denied/partial/unknown>` | `<what Product should demonstrably mean>` | `<misleading success/authority/verification>` |

Include only material cases. **Defined acceptance** is not evidence that software tests were executed or that delivery succeeded.

## 5. Dependencies, Scope, and Delegated Solution Freedom

| Concern | Required answer |
| --- | --- |
| Genuine prerequisites | `<necessary Product behavior; actually available / not available / unverified>` |
| External or cross-boundary signals | `<what evidence or other owner is material; observed standing>` |
| Included outcomes | `<what this bounded contract covers>` |
| Explicit exclusions | `<what is not promised or cannot be inferred>` |
| Delegated Design freedom | `<interaction, content and visual decisions allowed within accepted Product meaning>` |
| Delegated Engineering freedom | `<architecture, state, interface, persistence, transactions, test mechanisms>` |
| Known applicable constraints | `<owning I2/I3 references if relevant, but do not pretend I1 approves or supplies them>` |

A spec, mock, diagram, previous implementation or seeded state **does not** prove a required capability is delivered.

## 6. Open Decisions & Blockers

| Question and affected claim | Decision owner | Status | Blocking consequence / next legitimate decision |
| --- | --- | --- | --- |
| `<specific unanswered Product question>` | `<authorized owner>` | `OPEN, PROPOSED or PARKED` | `<which outcome/SC/REQ/AC cannot be approved, or why not blocking>` |

`OPEN` **does not inherently mean urgent**. Only unanswered questions material to *this contract* and its truthful outcome must be resolved before its exact I1 revision becomes binding. Do not import answers from historical packages by default. **Potential Conflicts**, where relevant, is a category of material conditions to describe precisely for the scoped outcome, not a universal conflict detection obligation.

## 7. Consumer Readiness and Handoff Boundary

| Readiness question | Actual evidence or standing |
| --- | --- |
| Approved Product meaning on an exact source revision? | `<APPROVED / PROPOSED / BLOCKED; real evidence>` |
| Outcome, SC, experience, behavior, invariants and AC internally consistent? | `<reconciliation carried out, scope and limitations>` |
| No hidden blocking Product decisions? | `<finding or owned blocker>` |
| Prerequisite and external signal availability honestly stated? | `<observed / missing / unverified>` |
| Generic Rancang I1 contract fit? | `<checked / conditional / unverified; reference>` |
| Project-bound consumer fit for intended assignment? | `<checked / conditional / blocked / unverified; specific evidence>` |

**Handoff result:** `<DRAFT — NOT READY / PRODUCT-APPROVED BUT CONSUMER FIT UNVERIFIED / APPROVED I1 FOR PINNED SCOPE / BLOCKED>` based only on actual decisions and evidence.

This artifact supplies **Product-owned I1 meaning only**. It does not supply Rancang `I2`, `I3`, or `I4`; does not form or invoke a Space; and does not authorize Engineering. Where the target project's accepted input standards differ, reconcile with actual consumer contracts and owners rather than imposing a second master document.

## 8. Additional Material Information (Conditional)

Use **only** for information important to correct Product interpretation or consumer use that genuinely does **not** fit sections 1–7.

For each item state: **what matters**, **why the standard sections do not capture it**, **supporting source and standing**, **risk of misinterpretation**, and **owner/next action** when necessary.

If none exists, write `No additional material information.`

**Not an escape hatch:** Binding requirements, critical invariants, Success Criteria, acceptance, security boundaries, material blockers and unresolved owner decisions **must stay in their owning sections**. No authority is created by including an extra note.

---

## Upstream reference note for downstream consumers

**Append the following note (or semantically equivalent text) to each Product Contract:**

> **Upstream references:** Source codes and links in this Product Contract are maintained by Product for provenance, decisions and upstream audit. Downstream consumers, including Rancang, **do not need to dereference or revalidate upstream Product research sources, nor interpret upstream reference IDs to discover additional requirements**. All binding Product semantics for this outcome must be contained in the approved exact-revision Product Contract. `SC`/`REQ`/`AC` identifiers may be used for **internal traceability within this contract**. Checks of actual approval and `I1` revision, internal contract consistency, `I2/I3`, and technical/security constraints remain applicable. Material contradictions return to the owning authority rather than being resolved by reconstructing requirements from upstream research.

**Adoption boundary:** Formed Rancang v3 **currently** mandates original-source inspection. This note expresses the **target handoff model**, not an effective waiver of its formed definition. Removing Rancang upstream Product source re-check requires a separately reviewed, exact-revision formation amendment.

## Applicability and evaluation

This draft is a **candidate reusable authoring format**, not a new universal completion gate. Evaluate against a real project-produced contract (initial pilot: Kencleng O1) and a **separate fresh-reader / Rancang I1 consumer fit test** before proposing operational adoption. If there is no meaningful benefit over the project's own format, keep it as optional guidance. Human approval of this template, if given, is distinct from approval of any Product Contract written with it and from Rancang's formation or invocation.
