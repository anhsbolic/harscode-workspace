# Template — Product Review & Approval Record (Bahasa Indonesia)

> **Standing:** DRAFT FOR HUMAN REVIEW. Optional research authoring aid. A completed-looking template is not approval.
> **References:** [Authority & Approval](../authority-and-approval.md) and [Product Definition](../product-definition.md).

## 1. Legitimate decision and scope

| Item | Record |
| --- | --- |
| Project / bounded Product concern | `<...>` |
| Exact question and consequential decision | `<...>` |
| Actual authorized Human approver | `<...>` |
| Evidence of Human decision (date/reference) | `<...>` |
| Decision | `APPROVE / REJECT / REVISE / DEFER` |
| Accepted scope, conditions and exclusions | `<...>` |

Record only a decision **actually made** by the legitimate Human owner. Do not infer approval from a template, Agent review or prior conversation about different bytes.

## 2. Exact reviewed artifacts

| Artifact / concern | Exact reviewed immutable path + blob/commit | Approved meaning/scope |
| --- | --- | --- |
| Product Contract | `<exact accepted revision>` | `<...>` |
| Supporting Product Definition (if material to decision) | `<exact accepted revision>` | `<...>` |

If the final Git revision was not yet available at the Human decision moment, identify an immutable reviewed content snapshot and **verify byte/semantic equivalence** before treating persisted content as approved. Never mutate accepted Contract bytes just to write this record or approval status.

## 3. Decisions and rationale

| Material question | Disposition | Accepted meaning / exclusions | Evidence, trade-off, risk |
| --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` |

The binding Product Contract contains accepted SC/REQ/AC; this record is **not a second normative specification**.

## 4. Unresolved questions and evidence limits

| Issue | Affected claim / receiving responsibility | Legitimate owner | Blocked edge or why non-blocking |
| --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` |

Distinguish Human approval from empirical user validation, UI/Engineering acceptance and runtime proof.

## 5. Effective standing and supersession

- Previous effective Product authority, if any: `<...>`
- Newly effective accepted artifact/revision: `<...>`
- Preserved historical approval and superseded scope: `<...>`
- Actual impacted consumers and revalidation/approval needs: `<...>`
- This approval record's location and revision: `<...>`
- References and exact approved bytes checked: `<actual check or NOT CHECKED>`

Semantically changed artifacts require legitimate new approval. A path/identifier migration needs authorized, recorded source equivalence and new effective pointers.

## 6. Explicit non-authorizations

This record does not authorize capability formation, Space invocation, protected writes, Engineering/Design approvals, canonical technical interface adoption, deployment, or a claim that Product value has been delivered.

**Final check:** Can a fresh reader verify exactly who approved what Product meaning, on which immutable bytes, and for what scope, without conversational recall?
