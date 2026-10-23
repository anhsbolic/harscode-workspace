# Product — Phase and Output Catalog

> **Scope:** Harscode Product guidance, structured in branch `refactor/harscode-foundation`. **Not promoted to operational `main`.** Actual Product truth belongs to the target project's approved artifacts and Human owner.
> **Core rule:** Product owns meaningful, truthful actor outcomes. Design expresses their approved meaning; Engineering implements it. Phase labels support navigation and traceability, **not a mandatory state machine or six separate files**.

## Product phases (ordered for navigation)

| Order | Human-facing phase | Phase ID | Output kind ID | Main output | Owning concern |
| --- | --- | --- | --- | --- | --- |
| 1 | [Product Foundation](foundation.md) | `PROD-FND` | `PROD-INTENT` | Product Intent & Value Definition | Purpose, actor/business value, responsibilities, Product principles and truth |
| 2 | [Product Journey Mapping](journey-mapping.md) | `PROD-JRN` | `PROD-JOURNEYS` | Interconnected Product Journeys | Meaningful actor progression, dependencies and unknowns |
| 3 | [Outcome Selection](outcome-selection.md) | `PROD-SEL` | `PROD-SELECTION` | Selected Product Outcome | Human selection of a valuable, bounded outcome |
| 4 | [Outcome Definition](outcome-definition.md) | `PROD-DEF` | `PROD-CONTRACT` | Product Contract | Outcome, success, behavioral obligations, negative paths and acceptance |
| 5 | [Product Review & Approval](review-and-approval.md) | `PROD-APR` | `PROD-APPROVAL` | Approval Record | Human Decision Gate, exact-revision Product approval |
| 6 | [Product Handoff](handoff.md) | `PROD-HND` | `PROD-HANDOFF` | Approved Consumer Handoff | Consumer-facing contract, authority and scope without automatic invocation |

**Codes distinguish types, not runtime states.** Phase code and output type are globally consistent in Harscode. Each project owns a stable **outcome instance key** (example `ORG-01`); append it when tracking scoped artifacts (`PROD-CONTRACT-ORG-01`, `PROD-APPROVAL-ORG-01`). Within-document `SC`/`REQ`/`AC`/`PD` identifiers are project-local. Humans can use plain names in discussion.

Do not create all outputs when the actual problem needs fewer: Product Value Definition may live inside Product Intent; selection can be a durable decision pointer; handoff can point to the approved Product Contract and approval record. No separate stage invocation, registry, six-folder structure, one-to-one Engineering Space assignment, or mandatory completion order is implied.

## Authority boundaries

1. Start from **current target-project approved authority** and its revision. Older conversations, examples and other project artifacts are not Product truth.
2. **Product Foundation owns value promises.** Journey Mapping connects how value is experienced; Outcome Selection chooses one; Outcome Definition makes scoped semantics and acceptance binding after Human approval. Product Design determines interaction/content/visual expression under those meanings and returns material Product-value gaps to the owner.
3. Product reconciles upstream Product sources and decisions **before approving** a self-contained contract. Agent tracking codes never hide additional requirements from downstream readers.
4. **Product approval is not Engineering approval.** Rancang input `I1` may consume an approved Product Contract, but `I2/I3/I4`, actual code/security evidence, consumer-fit and authorization remain separate.
5. Current formed Rancang v3 still has an upstream source-inspection requirement. The desired Product-side self-contained handoff does **not** amend Rancang on its own; address that under Rancang authority later.

## Templates and guidance

- [Product Contract template — Bahasa Indonesia](templates/product-contract.id.md)
- [Product Contract template — English](templates/product-contract.en.md)
- [Agent routing](AGENTS.md)

The template is an authoring option. Actual project Product rules, approval, language and file organization are owned by each target project.

## Current demonstration and evidence limits

[Kencleng Product O1](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/outcomes/org-01/product-contract.md) has an Anhar-approved Product Contract on the Kencleng branch. It supports a concrete authored-output example, **not** universal evidence that the six-phase guidance is fully verified by independent downstream consumption. Historical experiments remain Git history; do not copy past project decisions as generic Harscode policy.

**Completion:** Product can finish as durable exact-revision approved semantics even while technical dependencies remain unverified. Reopen settled Product decisions only when materially new evidence appears.
