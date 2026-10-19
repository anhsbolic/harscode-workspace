# S1 Specialist Composition — Proposed

Four **bounded specialist responsibilities** are proposed for first real-use calibration; they are not guarantees of four configured runtime Agents, fixed model IDs, or a universal staffing minimum. Agent package changes should follow evidence. The Space coordinator composes/checks their outputs, but is not a fifth automatically-created Agent.

| Specialist / package | Consumes | Produces and owns | Does not own |
| --- | --- | --- | --- |
| [Requirements Analyst](../agents/requirements-analyst/profile.md) | Original authority + constraints + binding | X1 source and obligation map, unresolved/approval classification | Re-approval/product invention, solution architecture |
| [Solution Architect](../agents/solution-architect/profile.md) | X1, architecture/baseline, technical permission | O1 shared decisions; O2 interface/data/invariant contracts | Feature implementation, legal/product authority, detailed local coding plans |
| [Experience Specialist](../agents/experience-specialist/profile.md) | X1, O1/O2 and design authority | O3 experience/interaction/state solution | Inventing product meaning, replacing backend permission checks, final UI implementation |
| [Solution Reviewer](../agents/solution-reviewer/profile.md) | **Original I1/I2/I4** directly + X1/O1/O2/O3 | O4 verification obligations; O5 coverage, contract consistency, findings | Mutating producer output, claiming independent runtime assurance |

Each package owns scoped `profile.md`, `guidance.md`, `guardrails.md`, `knowledge.md` and `kickoff-prompt.md`. This is deliberate separation: routing/capability, working technique, non-negotiable stop conditions, local reference knowledge, and executable assignment entrypoint can evolve differently.

**Composition is functional, not ornamental.** If one Specialist/session can safely deliver multiple non-independent tasks, combine at invocation with an explicit assignment. Internal Review independence cannot be waived invisibly simply because the same operator/model is available; state what actually differed in context/persona and what is unproven.

## Authority and knowledge discipline

- **Space contract** governs required outputs and truthful failure. **Current project authority** governs product semantics and protected access.
- **Agent-owned knowledge** guides technique, not authority; it may duplicate another package to keep context local. Search this package's knowledge by relevant trigger; no mandatory global `best-practices/index.md` scan.
- Cross-Agent invariants are transmitted through I1/I2, scoped task requests, X1, explicit O1–O4 relations, reviewer checking and consumer conformance—not a new global invariant registry.
- Material conflict: do not pick whichever Agent seems more convincing; identify the owning input/decision and escalate when not delegated.
- Specialist profiles describe required reasoning capabilities, risk sensitivity and review independence, **not** a selected model or harness-specific effort setting. Actual model, effort/compute level, access and permission choices belong to the project/runtime binding under applicable Human policy; see [execution requirements](execution-requirements.md).

## Space coordinator responsibility

Validate original input package against [generic input](../contracts/input.md); pin revision; establish versioned writing/evidence paths and approved Specialist assignments; ensure outputs are actually delivered and handoffs conformed; request scoped correction; return the final [bundle](../artifacts/delivery-bundle.md). No software scheduler, automatic promotion or shell dispatch is implied.
