# Product — Research Guidance

> **Status:** WORKING / RESEARCH-ONLY. Rebuilt for evaluation on `refactor/harscode-foundation`; not approved operational Harscode policy.
> **Owner:** Harscode Product guidance. Product decisions and truth for any actual product remain with its owning project.
> **Applies to:** Product discovery, Product Authority assessment, commitment selection, commitment-scoped experience clarification, and product-to-consumer handoff.
> **Precedence:** Current target-project approved authority first; this research guidance cannot amend it. Legacy material under `deprecated/` is evidence only.

## Current Kencleng research experiment (not general Product policy)

The [current Kencleng Product research route](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/README.md) uses Product Intent + Interconnected Journeys Level 2 for fresh outcome selection and Product elaboration. The [current selection/handoff checkpoint](https://github.com/anhsbolic/kencleng/blob/pilot/station5-c1-space-only/docs/product/interconnected-journeys/selection-and-handoff-research.md) rejects importing historical commitment-specific requirements into O1 or using a prior draft PRD that repackaged them. It records an approved **working research** Product Output Contract, not effective Harscode policy, a Product Space, or a Rancang invocation. Historical pilot artifacts remain only historical evidence in this experiment; do not auto-consume them as the source of current requirements.

## Purpose

Help a Human and AI move from a real human problem to a **meaningful, truthful product outcome** that downstream Design and Engineering can consume without inventing Product Truth.

Product experience is not a final presentation layer. It is a recurring test of what a person **knows, does, experiences, and can validly conclude**. Requirements and invariants protect that meaning; they do not substitute for it.

## Read by concern

| Current question | Guidance |
| --- | --- |
| Is the project's Product Authority clear, sufficient, and genuinely owned? | [Product foundation](foundation.md) |
| What experiences matter, which outcomes should be committed to, and how are exceptions handled? | [Experiences and commitments](experiences-and-commitments.md) |
| What must remain accessible and binding when Design or Engineering takes over? | [Product handoff](handoff.md) |
| Need only routing, boundaries, or stop rules? | [Product AGENTS](AGENTS.md) |

Read the smallest relevant section. No fixed PRD format, persona inventory, stage count, or Product approval ritual is imposed by this research guidance.

## Conceptual flow (not a mandatory sequence)

```text
Project-owned purpose, actors, truths and uncertainty
        ↓
Actor situations / representative experiences
        ↓
Meaningful product outcome candidates and dependency analysis
        ↓
Human-selected product commitment
        ↓
Commitment-scoped experience: success, exceptions, resulting state
        ↓
Approved behavior / semantic obligations / acceptance as needed
        ↓
Versioned product handoff to Design and/or Engineering
```

Discovery may reveal new Product Authority gaps. Concrete experience can change the candidate commitment before it is approved. A downstream implementation constraint may reopen only the affected owner decision, with new evidence. This is a model of **reasoning and authority**, not a required workflow engine or one-way waterfall.

## Hard separation

- **Product**: what an actor should meaningfully experience and what the product may truthfully claim.
- **Design**: how the approved meaning is expressed through interaction, content, UI, accessibility and visual language.
- **Engineering**: how the approved meaning is implemented and independently verified through executable systems.
- **Collaboration**: how Human and AI discuss, evaluate, decide and authorize across owners.
- **Harness**: runtime mechanics, not product semantics.

A commitment may be one indivisible product outcome while requiring multiple bounded engineering design/implementation assignments. Conversely, a single engineering assignment may support several product outcomes. **Do not introduce a Delivery Units policy here**; that concern is still under investigation.

## Use and readiness

- These files are **working proposals for evaluation**, not self-approved Product Authority.
- The target project's current source and approved commitments remain binding within their actual scope.
- Product handoff is not an implementation, a production release, or proof that a downstream consumer can execute.
- Any claim of successful independent cold-start consumption needs a separate fresh-reader test; a document review is not that test.

See [Foundation Refactor Architecture](../ARCHITECTURE.md) and [Refactor Checklist](../REFACTOR-CHECKLIST.md) for refactor standing.
