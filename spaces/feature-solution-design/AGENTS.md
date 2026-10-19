# AGENTS.md — Feature Solution Design (Research Candidate)

Read [SPACE.md](SPACE.md) first for definition status, owner, authority and allowed output; then choose scoped guidance by actual assignment.

## Routing

- External input/output: [Input](contracts/input.md), [Output](contracts/output.md).
- What produces what: [Path relations](composition/path-relations.md), [Responsibilities](composition/responsibilities.md).
- Artifact envelope and evidence: [Artifacts](artifacts/format-and-traceability.md), [State](invocation/state-and-handoff.md).
- Invocation/preflight: [Kickoff](invocation/kickoff-prompt.md); Codex translation: [Codex binding](harness/codex.md).
- For an individual Specialist, open only that Specialist's `profile.md`, `guidance.md`, `guardrails.md`, `knowledge.md`, `kickoff-prompt.md` when their concern actually applies. Their knowledge is locally owned; no global Best Practices index is required for this candidate.

## Hard rules

1. This tree is **PROPOSED / UNFORMED** until the authorized Human owner separately approves a pinned definition revision. Reading it grants no invocation.
2. The Space's external contract is technology-neutral; concrete assignments must honor target-project stack and architecture. No Kencleng C1 content becomes reusable Space truth.
3. Follow current project authority and approved acceptance directly; Agent-local knowledge never overrides applicable project/Space contracts, security boundaries, or permission gates.
4. Scope is **solution production**, not project Product Authority change, feature code, deployment, end-to-end product assurance or downstream execution.
5. Reviewer must receive original authority directly and review current outputs without relying on producer narrative. Reviewer does not modify production artifacts.
6. Failure, partial, contradiction, missing authorization, or unknown must be reported truthfully; never claim validated runtime or human approval.
7. Output and state must be reconstructable from pinned artifacts; chat memory is not authoritative. Prefer smallest task-relevant reads.
