# Product C1 — Independent Cold-Read Validation

> **Status:** TEST PROTOCOL / NOT PRODUCT AUTHORITY.
> **Owner:** Harscode Foundation Refactor evaluation.
> **Tested Harscode candidate:** `anhsbolic/harscode-workspace@643fde68ecbf7bc682bbef06d56e621f91433c53` (branch `refactor/harscode-foundation`).
> **Target-project evidence:** `anhsbolic/kencleng@91fad854301265357ba69e76182eb5c82ae71049` (branch `pilot/station5-c1-space-only`).
> **Mode:** Read-only, independent fresh-context session. No modifications to either repository.
> **Standing:** PREPARED; **NOT EXECUTED IN AN INDEPENDENT SESSION**.

## Purpose

Determine whether a reader without prior Harscode/Kencleng conversation can use the **working Product guidance** to reconstruct the current Product Authority, the C1 actor experience, its commitment and its downstream semantic handoff.

This is an **independent-consumption** test, not a source citation audit, product approval, engineering design, or runtime test. The candidate Product guidance is research-only; historical/archived guidance is not active authority.

## Instructions for the independent reader

Use the following message verbatim in a fresh session. Do **not** supply this session's history, a model answer, or additional C1 summaries.

### Reader prompt

```text
Independent read-only evaluation: Harscode Foundation Refactor — Product guidance.

You have no prior conversational context. Work only from authoritative files you can actually access; identify missing access instead of inferring facts. Do not modify files, open PRs, or invoke Engineering Spaces.

Sources:
- Proposed Harscode Product guidance: repository anhsbolic/harscode-workspace, exact revision 643fde68ecbf7bc682bbef06d56e621f91433c53. Begin at product/AGENTS.md; follow its scoped navigation. This is research-only guidance, not Harscode main policy.
- Target project: repository anhsbolic/kencleng, exact revision 91fad854301265357ba69e76182eb5c82ae71049. Locate the current authoritative and supporting product artifacts for commitment C1 ("Legitimate Organization representation") using the repository, not chat or recollection.

Evaluate whether the proposed Product guidance is sufficient for a fresh reader to answer:

1. What is the whole-product authority, what is the C1 commitment, and which sources actually bind downstream C1 product meaning? Distinguish approved, supporting, historical/superseded, and open materials, with specific file links and document standing.
2. Describe C1 from the initiating human actor's perspective, from entry through consequential action, success, later inspection, and material exceptions. State exactly what the success claim does and does not mean.
3. Identify relevant product dependencies and unknowns. Separate product gaps from Design/Engineering implementation freedom. Do not invent mechanisms or additional commitments to make the chain look complete.
4. Explain whether C1 is one product outcome or multiple independently deliverable outcomes, and whether that dictates the number of solution-design or engineering assignments.
5. State what a downstream Design/Engineering consumer must receive, where approval applies, and which assertions are still unproven.
6. Critique the Harscode Product guidance itself: name any concrete omission, ambiguity, excessive ceremony, misleading rule, or authority/routing defect that would cause a fresh consumer to make a wrong decision. If none is found, say why.

Report:
- An explicit PASS / PARTIAL / FAIL for fresh-context Product guidance consumption, supported by citations to precise repository paths/sections.
- Material issues only, each with a consequence and the smallest justified improvement.
- What you verified versus inferred versus could not verify.
- Whether you recommend the Product Foundation proceed to Design or remain blocked.

Do not treat a handoff, design, mock, previous implementation, or historical research branch as evidence that C1 was delivered.
```

## Reviewer scoring (after receiving independent output)

Do **not** give the reviewer a precomputed answer. Assess the returned output against the current owning files:

| Dimension | PASS evidence | Failure indicator |
| --- | --- | --- |
| Source/authority discipline | Identifies correct project ownership, exact source standing and current approved precedence | Uses archived guidance or superseded decisions as current Product Authority |
| Experience integrity | Actor-centered entry → consequential action → outcome → later inspection plus material negative paths | Treats C1 as only a UI screen, technical task, or transient success message |
| Semantic correctness | Success and non-success claims match approved behavior and scoped requirements | Invents verification, broader review, legal authority, conflict resolution, or mandatory recovery |
| Commitment/assignment separation | Product meaning does not force a one-to-one Space/task decomposition | Calls implementation milestones independent delivered product outcomes by fiat |
| Consumer readiness | Identifies binding obligations, dependencies, freedoms and gaps | Claims current implementation, accepted Rancang solution, or operational readiness without evidence |
| Guidance usability | Uses concise route to sources and surfaces material ambiguity if found | Depends on conversation memory, unfounded assumptions, or extensive archived text |

Record **PASS** only if all material criteria are met without correction or coaching. Use **PARTIAL** for bounded errors that can be corrected locally and **FAIL** for a materially false authority/product outcome. Access failure means **NOT TESTED / BLOCKED**, not FAIL for the guidance.

## Evidence recording

Once an independent response exists, record:
- Session date and tested exact source revisions.
- Whether the reader was truly independent of prior conversation/context and whether repository access succeeded.
- Response or durable link and exact source citations.
- Dimension-by-dimension evidence, material errors and verdict.
- Any authorized subsequent guidance change, versioned separately.

An unexecuted protocol, same-session source trace, automated link check or self-review cannot satisfy the independent fresh-context checkbox in [Refactor Checklist](../REFACTOR-CHECKLIST.md).
