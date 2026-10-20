# Harscode Foundation Refactor — Authoring Rules

> **Status: WORKING / RESEARCH-ONLY.** These rules govern changes on the Foundation Refactor branch and do not replace Harscode operational `main`.

## Quality rules

1. **One owner per concern.** Write reusable guidance in the domain that owns the decision. Keep project-specific truth in the target project.
2. **Accuracy before brevity.** Preserve input and output meaning, preconditions, scope, refusal/stop conditions, negative paths, approval boundaries, security safeguards and required verification.
3. **Small active surface.** Prefer a clear local entrypoint and conditional deeper references to repeated rules or a centralized knowledge catalogue.
4. **Experience-led Product.** Explain actor situation, experience and truthful outcome before requirement lists. Preserve binding requirements and invariants without converting them into invented UI or engineering mechanics.
5. **Specialist-local knowledge.** Curate relevant technical knowledge into the consuming Engineering Specialist. Intentional redundancy may be acceptable; prevent critical safety-rule divergence.
6. **Explicit standing.** Mark each artifact `WORKING`, `NOT READY`, `APPROVED` or other context-appropriate status, with owner, source and revision; do not infer approval from file placement.
7. **Reconstructable state.** A fresh session must locate current authority and decisions from durable sources; archived copies and chat history are not authority.
8. **Selective migration.** Review and rewrite as needed. Do not mass-copy historical prose merely to fill a new directory.
9. **Evidence and reversibility.** Verify exact diffs, link changes, permissions, and consumers. Real execution/consumption is necessary before runtime-quality claims.
10. **Human authority.** Request explicit Human approval for material semantic/contract changes and protected writes. Do not expand a granted refactor scope silently.

## Change control

- **Ordinary reversible wording/routing corrections:** inspect current owner, modify the smallest affected area, verify the diff and links; no separate proposal file required by default.
- **Material Product/Design meaning or project contract:** the target-project Human owner decides and approves the exact revision; reusable Harscode guidance cannot amend it.
- **Space definition, scope, Human gate or critical security rule:** require Human review of the affected definition/revision before a new approval claim. Previously pinned approvals do not move with files.
- **Runtime activation, protected repository writes and downstream acceptance:** require their distinct, scoped Human authorization and actual runner evidence.
- **Research-to-operational promotion:** separate decision only after integrated semantic review, fresh-context consumption and relevant execution evidence. A Git merge or neat documentation tree alone does not establish operational correctness.

Record durable decisions with the *owning artifact*, not a global mandatory proposal register. A PR can supply the review/diff trail where available. Do not create per-domain proposal systems without a concrete recurring need.

## Migration notes

- Legacy guidance is preserved under [deprecated/](deprecated/README.md) with original Git object identities.
- The original pinned Rancang definition remains authoritative only for its historical approved research scope; a moved or modified definition requires its own review.
- Do not duplicate the old `proposals/` mechanism by default. Use targeted review and Git revision evidence proportionate to consequence.

See [Architecture Blueprint](ARCHITECTURE.md) and [Refactor Checklist](REFACTOR-CHECKLIST.md).
