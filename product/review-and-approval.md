# Product Review & Approval

> Scope: Harscode Product guidance in the current branch. Product approval authority belongs to the target project's authorized Human; no change to operational main.

Phase: `PROD-APR`. Output kind: `PROD-APPROVAL` — Product Approval Record.

## Purpose

Confirm that an outcome's Product Contract has coherent behavior, success, negative paths and acceptance, that material decisions have been made by the correct owner, and that the approval is bound to an immutable revision. This is not a release or Engineering approval.

## Human Decision Gate

1. Consolidate only OPEN decisions material to the selected outcome. Record the real question, owner, consequence and affected contract parts. OPEN questions elsewhere are not automatically blockers.
2. Ask the authorized Human to decide; do not silently promote a recommendation into a rule.
3. Reconcile actor outcome, Success Criteria, behavior, invariants, Product requirements and Acceptance Criteria with accepted decisions.
4. Product checks source authority/precedence and whether the contract is self-contained. Record genuine gaps and unresolved contradictions.
5. Persist Human approval with exact file revision/blob, scope, date, owner and audit evidence. A verbal approval not yet persisted is a working decision, not durable canonical authority.

An approved contract is binding only for its declared project, outcome and revision. Meaningful subsequent semantic changes require a new exact-revision approval.

## Identifier migration

A user-authorized, semantics-preserving identifier or path migration may be performed separately from a new Product policy decision. Preserve the old approved blob, maintain complete old-to-new ID mappings, verify semantic fields are unchanged after normalizing identifiers, and pin the newly effective revision. Do not silently rewrite historical approvals.

## Exit and boundaries

Human Product decisions CLOSED and Product Contract APPROVED are distinct from consumer fitness, input I2/I3/I4, runtime verification or an Engineering assignment. An internal consistency check does not prove independent cold-read consumption.

Next: Product Handoff (`PROD-HND`).
