# Harscode Foundation Refactor — Authoring Rules

> **Status: TEMPORARY / REFACTOR ONLY.** These rules govern new guidance drafted on the isolated Foundation Refactor branch. They are not an operational replacement for Harscode `main`.

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

## Migration notes

- Legacy guidance is preserved under [deprecated/](deprecated/README.md) with original Git object identities.
- The original pinned Rancang definition remains authoritative only for its historical approved research scope; a moved or modified definition requires its own review.
- Do not duplicate the old `proposals/` mechanism by default. Use targeted review and Git revision evidence proportionate to consequence.

See [Architecture Blueprint](ARCHITECTURE.md) and [Refactor Checklist](REFACTOR-CHECKLIST.md).
