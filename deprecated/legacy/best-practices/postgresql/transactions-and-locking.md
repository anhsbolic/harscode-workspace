# PostgreSQL Transactions, Isolation and Locking

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** PostgreSQL operations with multi-write consistency, concurrent decisions, lock contention or retry.
> **Triggers:** transaction, atomicity, consistency, race, SELECT FOR UPDATE, isolation, deadlock, outbox.

## 01 — Applicability

Use when a defined product invariant spans multiple DB operations or concurrent requests can invalidate a check-then-write. Identify the *observable product invariant first*. Do not infer a mandatory technology/transaction shape from a product-level requirement; select the mechanism after inspecting the actual storage and failure boundaries.

## 02 — Principle / Rule

- Commit an all-or-nothing DB consequence atomically where the invariant requires it, using a transaction or another proven equivalent guarantee.
- Keep transactions short; do not perform slow network calls, user interactions or external notification sends while holding DB locks.
- Understand isolation: PostgreSQL Read Committed can observe different committed data across commands in one transaction. A preceding `SELECT` alone does not reserve a future right to write.
- Enforce race-sensitive uniqueness/invariants with appropriate constraints, conditional writes, row locks or stronger isolation **as the chosen policy requires**.
- Lock resources in a consistent order when multiple rows are locked. Handle deadlock (`40P01`) and serialization (`40001`) aborts by retrying the **whole transaction** only when bounded and safe.
- A DB commit is not atomic with an external side effect. Use outbox or other durable coordination when reliable post-commit delivery is actually required.

## 03 — Rationale & Risk

A partial write can claim success without its required companion write. Two requests can both pass a pre-check and race to create invalid results. Long transactions increase contention and affect vacuum cleanup; inconsistent lock order causes deadlocks. Retrying only the failed statement within an aborted transaction is not a correct recovery.

## 04 — Application Guidance

1. Write the invariant as an assertion against committed/observable state; identify which rows/constraints need to participate.
2. Choose a single transaction for same-DB dependent writes when it provides the correct guarantee. Verify operations use the same transaction handle and rollback on error.
3. Where concurrent creation must be unique, consider database UNIQUE/EXCLUDE constraints with domain-appropriate keys; a read-before-insert is not sufficient by itself.
4. For concurrent updates to existing rows, evaluate conditional `UPDATE ... WHERE ... RETURNING`, explicit row locking, or Serializable with whole-transaction retry. Each has different cost and semantics.
5. Define a truthful result for uncertain commit/network outcomes; an idempotency/reconciliation strategy may be needed at the API boundary.
6. Emit external effects *after* commit or through a durable outbox, depending on the guarantee actually required.

## 05 — Verification

In a real PostgreSQL integration environment, test forced failure after the first dependent write, rollback visibility, concurrent attempts at violating the invariant, duplicate requests, locking/deadlock-sensitive ordering and commit uncertainty where relevant. Record isolation level, actual commands and evidence. Unit mocks cannot prove DB isolation/constraints.

## 06 — Boundaries & Trade-offs

A single transaction does not solve external-system atomicity; Serializable is not a universal default; row locks cannot enforce every conceptual/real-world uniqueness property. Do not invent conflict detection or legal-identity matching from a generic DB guideline. Evaluate contention and retry safety in the actual project.

## References

- https://www.postgresql.org/docs/current/transaction-iso.html
- https://www.postgresql.org/docs/current/explicit-locking.html
- https://www.postgresql.org/docs/current/ddl-constraints.html
