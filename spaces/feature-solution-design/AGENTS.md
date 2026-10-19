# AGENTS.md — Feature Solution Design (Research Candidate)

Read [SPACE.md](SPACE.md) first for definition status, owner, authority and allowed output; then choose scoped guidance by actual assignment.

## Routing

- External input/output: [Input](contracts/input.md), [Output](contracts/output.md).
- Structural I/O, producers and consumers: [Input–output chain](composition/input-output-chain.md), [Responsibilities](composition/responsibilities.md).
- Human-facing Space Coordinator: [Profile](agents/space-coordinator/profile.md), [Guidance](agents/space-coordinator/guidance.md), [Guardrails](agents/space-coordinator/guardrails.md), [Coordinator entry](agents/space-coordinator/kickoff-prompt.md).
- Logical order, handoffs and gate boundaries: [Interaction sequence](composition/interaction-sequence.md), [Human Approval Gates](composition/human-approval-gates.md).
- Artifact envelope and evidence: [Artifacts](artifacts/format-and-traceability.md), [State](invocation/state-and-handoff.md).
- Invocation/preflight: [Kickoff](invocation/kickoff-prompt.md), [Execution requirements](composition/execution-requirements.md), and [State](invocation/state-and-handoff.md). Harness-specific configuration and translation are external to this Space.
- For an individual Specialist, open only that Specialist's `profile.md`, `guidance.md`, `guardrails.md`, `knowledge.md`, `kickoff-prompt.md` when their concern actually applies. Their knowledge is locally owned; no global Best Practices index is required for this candidate.

## Hard rules

1. This tree is **PROPOSED / UNFORMED** until the authorized Human owner separately approves a pinned definition revision. Reading it grants no invocation.
2. The Space's external contract is technology-neutral; concrete assignments must honor target-project stack and architecture. No Kencleng C1 content becomes reusable Space truth.
3. Follow current project authority and approved acceptance directly; Agent-local knowledge never overrides applicable project/Space contracts, security boundaries, or permission gates.
4. Scope is **solution production**, not project Product Authority change, feature code, deployment, end-to-end product assurance or downstream execution.
5. Reviewer must receive original authority directly and review current outputs without relying on producer narrative. Reviewer does not modify producer-owned artifacts.
6. Failure, partial, contradiction, missing authorization, or unknown must be reported truthfully; never claim validated runtime or human approval.
7. Output and state must be reconstructable from pinned artifacts; chat memory is not authoritative. Prefer smallest task-relevant reads.
8. Coordinator is a Human-invoked Agent role: **supervised default**, **autonomous only on explicit Human request**, with non-waivable consequence-based Human gates. Balad is advisory-only and cannot invoke, request dispatch from, communicate with or coordinate this Space.
9. Space and Agent files must not assume a particular harness, model/effort enum, native subagent mechanics or sandbox configuration. Translate execution requirements externally and verify concrete readiness.
