# 0035 — Promote workflow-v2 to operational default

**Status:** Accepted - Anhar
**Date:** 2026-09-16
**Protection Tier:** general
**Triggered by:** completion of two real Continuous Real-Task Validation runs with positive correctness/outcome evidence, including a second materially different Kencleng frontend task after the Validation #1 refinements.
**Target area:** promotion of the validated `workflow-v2` line to Harscode `main`; no new runtime workflow mechanism is introduced by this proposal.

## Decision

Promote the validated workflow-v2 line to Harscode `main` as the current **Operational Default**.

This decision accepts the workflow architecture implemented under proposal 0031 and the accepted evidence-backed refinements in proposals 0032–0034. It does **not** declare the workflow fully mature, universally optimal, or permanently stable.

## Evidence

### Validation #1

Validation #1 exercised a broader implementation with Build/Review/Testing patch loops and showed that independent verification still found real defects while durable artifacts preserved reconstructability across phase boundaries.

It also exposed concrete friction that drove proposals 0033 and 0034: provenance/operator handoff gaps, late optional-plan routing, and repeated verification without enough economics/ownership guidance.

### Validation #2

Validation #2 used the refined candidate `workflow-v2@4199c6db1b26ef1920ba670f222aff0c6d0f9e59` on Kencleng's clean Frontend Experience Foundation task.

Observed lifecycle:

```text
Exploration + Techplan in one healthy continued thread
→ fresh material-UI Build
→ fresh independent Code Review
→ fresh independent Testing
→ human rendered acceptance
→ delivery
```

Observed quality outcome:

```text
Rescue prompts: 0
Clarifications: 0
Human redirections caused by agent misunderstanding: 0
Code Review findings: 0
Testing code defects: 0
Patch loops: 0
Human rendered acceptance: PASS
Delivery: PASS
```

Independent Techplan review and decomposition were both skipped by their routing/gates. Later independent Review and Testing did not expose a material decision that those skips had lost.

Secondary operator-recorded non-cached totals were directional rather than a universal cost baseline:

```text
Exploration + Techplan: 48,272
Build:                  136,757
Code Review:             75,894
Testing:                 78,172
Run total:              339,095
```

Cached input was tracked separately and is not treated as economically equivalent to non-cached input.

Kencleng evidence is preserved under:

`frontend/.local-agents/works/00-foundations/01-frontend-experience-foundation/`

The delivered task merged through Kencleng PR #24 as `main@71093b687cd7135495bc6ed62d520a621f96f586`.

## Why promotion is justified

The evidence now supports the narrower question required for promotion:

> Is workflow-v2 credible enough to become the current default without lowering the established correctness/outcome floor?

The answer is yes.

Across the two runs, the evidence supports:

- progressive disclosure instead of broad mandatory loading;
- durable state over chat memory;
- continuation-fitness routing instead of one-session-per-phase ritual;
- fresh independence for Code Review and Testing;
- Build ownership of production patches;
- optional Techplan review/decomposition rather than mandatory ceremony;
- proportional planning that resolves material decisions before Build without pre-solving cheap mechanics;
- verification rationale/ownership rather than tool-name ritual;
- human product/rendered acceptance remaining distinct from automated verification.

## What remains unproven

Promotion to `main` is not the same as broad maturity. Real future work should continue to exercise and benchmark paths not yet covered sufficiently, including:

- Complex Techplan independent review;
- decomposition into multiple execution tasks;
- repeated Review → Build/Patch and Testing → Build/Patch cycles under the refined ownership rules;
- API/data-contract work;
- auth/security-sensitive work;
- cross-service, migration, destructive, or major state-ownership changes.

Do not manufacture synthetic tasks merely to fill this list when normal project development will provide real evidence.

## Post-merge expectation

Continue **Continuous Real-Task Validation** after promotion.

For each meaningful run, preserve enough evidence to judge both:

```text
efficiency
→ context/session usage, repeated loading, repeated verification, rescue prompts

correctness/outcome
→ authority adherence, human redirection, Review/Testing findings, patch loops, final acceptance
```

Do not tune the workflow after every run. Promote an observation into a workflow change when repeated real-task evidence shows a stable correctness gap, routing ambiguity, or unnecessary recurring cost.

The current maturity interpretation is:

```text
Level 0 — Experimental
Level 1 — Validated Candidate
Level 2 — Operational Default      ← accepted now
Level 3 — Broadly Validated
Level 4 — Mature / Stable
```

## Integration note

Before promotion, current Harscode `main@abfa66ae3c049f01bb41666b7b64ab6f463726e3` added accepted upstream `product-design/` guidance as proposal 0030. `workflow-v2` was reconciled with that commit rather than overwriting it.

Because the isolated branch had temporarily used proposal numbers 0030–0033, its workflow proposals were mechanically renumbered to final 0031–0034. Historical audits may still cite the experimental numbering; `proposals/README.md` records the mapping.

No speculative runtime workflow redesign is part of this integration step.

---

*Accepted by Anhar after Validation #2. Merge the reconciled workflow-v2 line to `main`, then continue longitudinal benchmarking during normal Kencleng development.*
