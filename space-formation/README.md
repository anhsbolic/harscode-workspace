# Space Formation — Reusable Capability Development (Station 5 Research)

> **Status:** EXPERIMENTAL on `research/harscode-purpose-llm-fit`; not operational `main` policy, a formed Space catalog, or evidence of runtime fitness.
> **Collaboration owner:** Anhar (approval and final decisions) + ChatGPT (reasoning, challenge, definition drafting and iteration).
> **Source discipline:** current Harscode research authority, target-project owning artifacts, and real execution evidence. Project-specific truth stays with the target project.

## Purpose

Develop **reusable, bounded Space capabilities** from real project needs while protecting strict external input/output contracts, verified handoffs, Human authority and execution boundaries.

A Space is a coherent bounded **production capability**, not a workflow phase, file layout, Agent persona or feature-specific recipe. "Generic" means reusable across suitable assignments **within a defined capability class**, not universal. A REST API production capability may be technology-specific; its reusable contract cannot encode Kencleng's C1 endpoint choices.

Formation quality is a **design claim** until actual harness and project use verify it. Do not equate a detailed profile with a functioning runtime.

## Responsibility boundary

| Responsibility | Owner |
| --- | --- |
| Project authority intake, end-to-end outcome/I/O chain, existing capability discovery, generic-vs-bound fit and gap reporting | **Balad / Pairing** in the project-facing session |
| Evaluate the formation request, challenge generalization, design/iterate reusable Space definition and contract | **Anhar + ChatGPT**, applying this guidance |
| Formation approval and consequential contract changes | **Anhar** |
| Validate selected runtime mechanics, input conformance, bounded execution and real delivery evidence | **Authorized Space / relevant execution actor**, with Balad coordinating external handoffs |
| Accept or reject the project outcome and any material product meaning | **Project-owning Human / authority**, Anhar for the current C1 pilot |

Balad **does not form/edit declarative Spaces or configure Specific Agents** under this Station 5 working boundary. It may explain needed capability and send a **Formation Request**. The Human may change this allocation in a later explicit decision, not through implied formation approval.

## Guidance routing

- [AGENTS.md](AGENTS.md) — concise authoring/authority rules.
- [formation-guidance.md](formation-guidance.md) — how to analyze a real gap, decide capability boundaries, generalize and iteratively form a Space.
- [contract-and-readiness.md](contract-and-readiness.md) — strict generic I/O, concrete assignment binding, inter-Space compatibility, readiness and evidence.
- [Proposed reusable Space packages](../spaces/README.md) — inspectable candidate definitions; formation requires Anhar's separate approval. Space definitions own **harness-neutral** execution requirements; Harscode-level `harness-optimization/` translates them to a selected runtime after applicable proposal approval.

Project-specific assignments, B1–B7 or other project semantics belong to the **invocation binding / target project**, not this guidance or reusable Space definition. Space definitions, if approved, need their own owning research location and reconstructable version; no permanent catalog or physical layout is presumed.

## Working cycle (adaptive, not an execution pipeline)

```text
Real project need + Balad's I/O-chain / capability-gap report
  → review effective sources and actual existing Space definitions
  → decide reuse / adapt / propose new formation
  → generalize a bounded, strict Space contract and Agent capabilities
  → Human reviews/approves the formation definition
  → separately authorized harness/runtime readiness check and invocation
  → observed outcome, consumer handoff, failures and improvement proposals
  → Human-reviewed revision of reusable Space as warranted
```

Do not demand formation every time a project has a gap: a Human decision, bounded local implementation or reuse may be better. Do not require all downstream Spaces to be formed before the first test.

## State and governance

Keep the distinction **research proposal → approved declarative definition → readiness-checked capability → execution-validated use**. These are reporting claims, not a new state machine. Formation approval does **not** approve invocation, protected engineering writes, contract changes in a running assignment or promotion to `main`.

When this experimental area changes materially, document the rationale and Human decision in its owning research context. Operational promotion would require the applicable Harscode authoring/proposal governance, separate from this pilot.
