# Reusable Space Formation — Reasoning and Iteration Guidance

> Applies to **Anhar + ChatGPT** for experimental Station 5 Space design. Do not use this file to authorize Balad to create definitions or Specific Agents. Read [contract-and-readiness.md](contract-and-readiness.md) for the technical contract floor.

## Start with a Formation Request, not a Space template

Balad's project-facing responsibility is to supply the **minimum sufficient capability-gap report**:

| Formation Request field | Meaning |
| --- | --- |
| **Project objective and authority** | Current target project/branch/version, accepted commitment, applicable constraints and acceptance owner |
| **Chain position** | Required logical outcome, its upstream inputs, downstream consumer(s), joins/parallel dependencies and final acceptance path |
| **Needed capability and expected generic IN → OUT** | Capability in reusable terms, plus the *specific* bound output needed for this project |
| **Discovery evidence** | Existing Space definitions actually checked; evidence for reuse/adapt/no-fit; unknown local sources acknowledged |
| **Handoff gap and consequence** | Which producer OUT → consumer IN is missing/mismatched, at generic and project-bound layers |
| **Constraints and unknowns** | Security/permissions, runtime/tool limitations, independent assurance, conditional downstream decisions; request to Human if necessary |

Not every report needs a formal file. A concise table and graph can be enough. Balad **reports** the gap; it does not create a Space definition, edit profiles or claim formation approval. If the project authority is unavailable or the chain is materially incoherent, request missing evidence before generalization.

## Adaptive formation reasoning

**1. Verify the need and existing capability.** Read the current owning project sources proportionate to risk, not historical implementations as default design authority. Check actual accessible reusable Space definitions and their **generic external contracts**, readiness status and known limitations. Distinguish "no suitable Space found" from "no Space exists anywhere". Prefer reuse, then a justified adaptation, then new formation; a missing project decision is not automatically a missing reusable Space.

**2. Challenge the proposed boundary.** Ask what independently useful, repeatable production responsibility a Space owns, who consumes its outcome, and why a standalone boundary is worth its coordination cost. Compare a small number of materially different groupings only when necessary. Avoid both giant do-everything Spaces and one-Space-per-stage/Agent/file. A capability can specialize in technology or output class while remaining agnostic to project feature content.

**3. Generalize without losing real constraints.** Separate:
- **Generic capability invariant:** accepted input types and provenance, production responsibility, output shape/quality, conformance evidence, failure/refusal semantics, assurance and authority.
- **Project invocation binding:** current approved requirement content, repository revision, requested feature/API/UX behavior, write scope, environment and acceptance evidence for this assignment.

Use the current project as a **concrete test case**, not the embedded definition of the reusable Space. Reject attractive abstractions lacking a present, testable benefit. Conversely, do not weaken strict contract semantics just to accommodate every possible project.

**4. Design the Space definition.** Apply the contract floor in [contract-and-readiness.md](contract-and-readiness.md), define the smallest credible Specialist capabilities and ownership of internal work, and bind only task-relevant knowledge/constraints. A Specific Agent profile is declarative until its Codex routing, tools, context, sandbox and actual capability are tested. For model choices, consult [pairing/model-routing.md](../pairing/model-routing.md) and Human-owned inventory/effort gates; do not populate or silently change that inventory.

**5. Review readiness before formation approval.** Show Anhar the proposed reusable I/O, boundaries, downstream generic-port fit, C1 or other project binding example, failure conditions, Agent composition rationale, actual versus unverified mechanics, and smallest viable validation experiment. Distinguish true security and independent-assurance blockers from harmless design freedom. Ask for **one scoped formation decision**; formation and invocation are distinct permissions.

**6. Persist an approved definition at its owning research location.** Preserve inspectable source, references and version/revision, but do not assume a fixed Space registry, generator, directory convention or `harscode-state` implementation. The physical storage model remains replaceable. A formation commit can establish a definition; it cannot by itself establish operability.

**7. Learn from actual use.** Record whether real input passed conformance, internal production was bounded, outputs satisfied the strict generic and concrete-bound contract, consumers accepted them, and required assurance was credible. When a Space/Agent discovers a reusable improvement, report:
- observed failure/friction with evidence, affected contract/Agent/knowledge;
- proposed change, expected benefit and compatibility impact on current/future consumers;
- whether a non-breaking addition, new version, scoped override, or different capability is warranted.

Route improvement proposals through Balad to Anhar + ChatGPT; only the owning Human approves reusable definition changes. Do not retroactively change an active invocation's pinned contract or disguise project-specific exceptions as generic improvements.

## Important decision boundaries

- **Product/domain truth:** owned by the target project/Human, never silently invented by a new Space or Harscode guidance.
- **Pairing composition:** Balad still maps whole-goal outcome dependencies and identifies missing capability, but **formation design belongs here**.
- **Formation:** creates/revises a reusable declarative capability after Human approval; does not dispatch engineering production.
- **Invocation:** separately scoped, after input conformance, actual harness readiness and required security approvals.
- **Acceptance:** executing Space reports truthful evidence; the authorized project/Human owner accepts or rejects the outcome.

## Stop when sufficient

For the first C1 test, form **only the next credible capability** if the report warrants one. Keep later Space counts and interfaces provisional. Do not create extra policy files or automation just to reflect the sections above.
