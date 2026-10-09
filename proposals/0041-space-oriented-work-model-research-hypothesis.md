# Space-Oriented Work Model — Research Hypothesis

**Status:** Research Hypothesis — Deferred
**Date:** 2026-10-09
**Revisit trigger:** After Kencleng C1 reaches end-to-end engineering delivery / verification evidence
**Authority:** Non-operational research note. This file does not change Harscode workflow, orchestration semantics, stage definitions, or target-project authority.
**Context:** Harscode is being developed through real end-to-end Kencleng usage as a laboratory for CRTV.

## Hypothesis

Harscode work may be better understood, at least in part, as a set of composable **Spaces** rather than primarily as one linear chain of phases/stages.

A Space is tentatively imagined as a bounded working environment that:

- accepts a specific class of input through an explicit input contract;
- owns a specific production responsibility / intended outcome;
- contains one or more agents with suitable Profiles and Specializations;
- may include Human collaboration or authority gates when materially required;
- may perform work internally in sequential, parallel, iterative, or other task-specific topology;
- produces a durable output through an explicit output contract.

Conceptually:

```text
bounded input
    ↓
┌────────────────────────────┐
│            SPACE           │
│                            │
│  Agent A      Agent B      │
│       Agent C              │
│                            │
│  profiles / specializations│
│  authority / Human gates   │
│  internal work topology    │
└────────────────────────────┘
    ↓
bounded durable output
```

The important contract is the Space boundary:

```text
accepted input
→ Space transformation
→ expected outcome / durable output
```

The internal execution mechanism is secondary.

## Standalone usefulness

A Space should be conceptually usable on its own.

If a Human has a problem that matches one Space's responsibility, the Human should be able to provide input satisfying that Space's input contract and receive the intended output without having to execute an entire Harscode pipeline.

This implies that composability should come from input/output contracts rather than from requiring one global workflow engine.

## Composition hypothesis

Spaces may compose when the output contract of one Space satisfies the input contract of another:

```text
Space A output
        ↓
Space B accepted input
```

Composition need not be strictly linear.

Possible topology may include:

```text
                  ┌→ Space B1 ─┐
Space A ──────────┤             ├→ Space C
                  └→ Space B2 ─┘
```

or other evidence-driven parallel / convergent relationships.

The topology should follow real dependency and production semantics, not stage numbering.

## Space is not a workflow engine

This hypothesis explicitly does **not** mean Harscode should become a workflow engine.

A Space should not require a central runtime/state machine merely to exist.

Its semantic value should remain understandable from:

- purpose / intended outcome;
- input contract;
- output contract;
- applicable authority;
- capabilities / Profiles / Specializations required;
- material Human gates;
- internal work that is necessary to produce the output.

Whether a future Space is implemented as a directory, agent team, collection of Runs, session container, orchestration construct, UI surface, or another mechanism is intentionally undecided.

Implementation mechanism must not become the semantic definition.

## Stage is not assumed to equal Space

Do not assume:

```text
Stage 1 = Space 1
Stage 2 = Space 2
...
```

The current Stage 1–7 pre-engineering model is useful evidence, not a required one-to-one mapping.

A Stage may represent a semantic maturity / transformation boundary, while a Space may represent the bounded production environment that performs work around such a boundary.

Future evidence may show:

- one Stage ≈ one Space;
- several Stages belong in one Space;
- one Stage requires multiple parallel Spaces;
- one Space contributes evidence to multiple maturity boundaries.

Do not decide this before observing complete real work.

## Relationship to agents

Agent is not assumed to be the primary unit of workflow.

Tentatively:

```text
Space
├── production responsibility
├── input/output contracts
├── applicable authority
└── agents
    ├── Profiles
    └── Specializations
```

Agents are capabilities operating inside the Space.

A Space may need one agent, several agents, or Human + agent collaboration depending on the actual transformation.

## Relationship to durable state

Correctness should not depend on one agent carrying conversational memory between Spaces.

A healthy composition would prefer:

```text
Space A
→ durable output
→ Space B reconstructs from that output + current authority
```

rather than:

```text
Agent remembers prior conversation
→ carries hidden context into next concern
```

This aligns with Harscode's existing preference for durable, reconstructable state.

## Relationship to Control Tower

The existing pre-engineering Control Tower / stage visualization suggests a potentially useful future view:

- which bounded concerns are currently being transformed;
- which Space, if any, owns that transformation;
- which required outputs already exist;
- which inputs are not yet sufficient;
- which concerns may progress independently / in parallel;
- where outputs converge into another Space.

This remains a visualization/research idea only.

The Control Tower must not become the semantic owner of Space state merely because it visualizes it.

## Why this is deferred

The current C1 experiment has already exposed a concrete engineering-boundary problem:

```text
Engineering Entry Ready
≠
Planning Ready
≠
Build Ready
```

There is enough evidence to test a bounded Solution Shaping mechanism before C1 proceeds to an execution-grade Techplan.

There is **not yet enough evidence** to justify restructuring Harscode around Spaces.

Changing the overall model now would modify too many variables during the same CRTV episode and make it harder to tell which mechanism actually improves delivery.

Therefore:

```text
Space
= active research hypothesis

C1 Solution Shaping
= current bounded experiment backed by observed evidence
```

## Revisit after C1

After C1 reaches end-to-end engineering delivery / verification evidence, use the complete C1 history as a specimen and ask:

1. Where did stable input → transformation → output boundaries actually appear?
2. Which current Stages / phases correspond to real reusable production responsibilities?
3. Which apparent stages are only maturity markers rather than distinct Spaces?
4. Did Exploration + Solution Shaping behave like one Space or multiple Spaces?
5. Is Techplan synthesis a distinct Planning Space?
6. Are Code Review and Testing meaningfully independent Spaces?
7. Which Spaces could be invoked standalone by a Human with only a valid input contract?
8. Where did parallel work naturally occur?
9. Which Profiles / Specializations were actually needed inside each bounded transformation?
10. What durable output was sufficient for a fresh next Space without conversational carryover?
11. Can Space composition remain simple and semantic without creating a workflow engine?
12. Does a Space model materially improve correctness, reuse, optionality, and Human usability over the current phase/stage model?

Only after this review should Harscode decide whether Space should become:

- a conceptual model only;
- a reusable guidance abstraction;
- an orchestration concept;
- a runtime/tooling concept;
- or no formal construct at all.

## Current decision

Do not operationalize the Space model during current C1 execution.

Finish C1 end-to-end first, using the smallest evidence-backed workflow refinement needed to reach Planning Ready and Build Ready.

Then revisit this hypothesis against complete real execution evidence.
