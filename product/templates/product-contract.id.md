# Template — Product Contract (Bahasa Indonesia)

> **Standing:** DRAFT FOR HUMAN REVIEW. Optional research authoring aid, not automatically binding target-project Product authority or Engineering input.
> **References:** [Product Definition](../product-definition.md), [Authority & Approval](../authority-and-approval.md), [Consumer Handoff](../consumer-handoff.md).
> **Boundary:** Defines consequential Product meaning, not screens, APIs, database models, named Space contracts, or execution permission.

## 0. Identitas, authority dan approval standing

| Item | Isian |
| --- | --- |
| Project / bounded Product outcome | `<...>` |
| Legitimate Human Product decision owner | `<...>` |
| Current effective Product sources/revisions | `<...>` |
| This artifact's immutable revision, if already recorded | `<...>` |
| Content standing | `DRAFT / PROPOSED / APPROVED only if external exact-revision record confirms` |
| Scope, exclusions and consumers by **functional responsibility** | `<...>` |
| Separate Product Approval Record | `<actual exact approved revision; NONE if pending>` |

**Approval must refer to the exact approved bytes.** Do not edit approved Contract bytes to insert an APPROVED label or SHA and then treat the previous approval as covering the modified content.

## 1. Outcome and Success Criteria

**Meaningful result:** `<actor, situation, legitimate action, domain change, why valuable, inspectable outcome>`

**Non-guarantees and scope limits:** `<...>`

| SC | Product success condition | Conditions that must hold jointly / what does not prove success | Authority source |
| --- | --- | --- | --- |
| SC-01 | `<...>` | `<...>` | `<...>` |

SC identifies legitimate Product success, not automatically a growth metric or actual runtime evidence.

## 2. Actor, Domain Roles & Authority Rules

**Relevant actor goals/context:** `<...>`

| REQ | Domain relationship, role meaning, eligibility | Attribution, acquisition/transition/loss, permitted actions | Forbidden inference and authority source |
| --- | --- | --- | --- |
| REQ-ROLE-01 | `<...>` | `<...>` | `<...>` |

Only define authority rules material to this outcome. Actor perspective is not identical to Domain Role; role meaning is not necessarily RBAC.

## 3. Consequential Content & Information Requirements

| REQ | Required information: supplied / collected / displayed / understood / inspectable | Source and status: asserted / verified / pending | Required timing/disclosure and prohibited claims |
| --- | --- | --- | --- |
| REQ-INFO-01 | `<...>` | `<...>` | `<...>` |

Product defines necessary domain information and consequential disclosure, not layout, visual hierarchy or non-consequential final UI copy. Material rules must trace to acceptance/invariants; they cannot hide in an optional appendix.

## 4. Bounded Product User Journey Anchor

| Moment | Legitimate actor understanding/action | Actual Product/domain consequence | Rejection, failure, partial, uncertain meaning |
| --- | --- | --- | --- |
| Entry | `<...>` | `<...>` | `<...>` |
| Pre-effect | `<...>` | `<...>` | `<...>` |
| Action | `<...>` | `<...>` | `<...>` |
| Result / later inspection | `<...>` | `<...>` | `<...>` |

Can reference a separate effective journey artifact for context, but no binding Product meaning may require reconstructing historical chat/research IDs. Do not specify UX screens/routes or technical sequencing.

## 5. Product Requirements, Business Rules & Invariants

| REQ | Accepted behavior / preconditions | Domain actor authority and consequential result | Invariant / prohibited state | Source and decision standing |
| --- | --- | --- | --- | --- |
| REQ-01 | `<...>` | `<...>` | `<...>` | `<exact approved/proposed source>` |

Material PROPOSED obligations cannot silently be treated as binding. Resolve with owner or narrow affected scope and reconcile SC/REQ/AC.

## 6. Acceptance Criteria

| AC | Related SC/REQ | Material case (positive / negative / partial / unknown) | Observable expected result | False-success / authority claim prevented |
| --- | --- | --- | --- | --- |
| AC-01 | SC-01 / REQ-01 | `<...>` | `<...>` | `<...>` |

Acceptance is a checkable Product claim, **not** evidence that software tests have run.

## 7. Dependencies, exclusions, delegated solution freedoms

| Area | Requirement / standing |
| --- | --- |
| Real prerequisites | `<available / missing / unverified with evidence>` |
| Related Product behaviors and external evidence | `<...>` |
| Included / excluded scope | `<...>` |
| Interaction & Experience Design freedom | `<...>` |
| Visual Interface & Content Design freedom | `<...>` |
| Engineering Solution Design / Development freedom | `<...>` |
| Effective non-Product sources | `<separately owned Design/technical/security standards and revisions>` |

A mock, diagram, seed, prior code path, or specification does not prove a real dependency is available.

## 8. Unresolved decisions and consumer sufficiency

| Material question | Affected SC/REQ/AC or claim | Legitimate owner | Blocked decision versus independent work |
| --- | --- | --- | --- |
| `<...>` | `<...>` | `<...>` | `<...>` |

| Check | Result and evidence |
| --- | --- |
| Directly understandable binding Product meaning | `<checked / gap / not checked>` |
| Actual Human approval at exact revision | `<approved record / NOT APPROVED>` |
| Generic receiving I/O contract fit, if applicable | `<checked / conditional / not applicable / unverified>` |
| Actual project-bound consumer fit | `<checked / conditional / blocked / unverified>` |
| Required original-source/project security checks | `<checked by receiver / pending / out of scope>` |

**Self-contained Product semantics never waive receiving responsibilities' applicable original-source inspection, technical/design/security inputs, or separate implementation authorization.**

## 9. Acceptance boundary

Only the legitimate project's separate exact-revision approval can establish binding Product meaning. No Product Contract alone approves Design, Engineering Solution, capability formation/invocation, canonical API adoption, protected writes, runtime completion or delivered actor value. Use an existing project format if it already satisfies these semantics.
