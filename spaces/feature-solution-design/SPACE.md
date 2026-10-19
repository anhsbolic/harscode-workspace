# Feature Solution Design — Reusable Space Candidate

> **Status:** PROPOSED / UNFORMED; research draft, no readiness or invocation evidence.
> **Owner role:** Human. The concrete owner and approval authority are identified in the applicable formation decision, not hardcoded into this reusable definition.
> **Capability identity:** `feature-solution-design`
> **Definition revision:** the Git commit containing this definition; pin exact SHA when approved. No semantic version number is claimed yet.
> **Formation basis:** Balad's accepted C1 capability-gap request; experimental [formation guidance](../../space-formation/README.md).
> **Scope:** Technology-neutral reusable solution design; each invocation is technology/architecture-aware through current project binding.

## Outcome and value

Transform a sufficiently approved, bounded software feature commitment into a **traceable, implementation-consumable solution contract** across material experience, interface, state, security and persistence boundaries. A future Go, NestJS, Next.js or other producer may consume it if generic and concrete I/O are compatible.

The Space is accountable for a **coherent solution**, not for creating features, making unsupported product decisions or implementing every local engineering detail.

## Authority, permissions, and exclusions

- The authorized **Human owner** controls formation, reusable-contract changes and material approvals. The Human authorized for the concrete project assignment controls its invocation approval. AI collaborators may help design or review, but do not acquire ownership or self-approval authority.
- **Balad is Human-facing advisory only** for authority, candidate capability and compatibility. It cannot invoke, request dispatch from, communicate with or coordinate the S1 Space Coordinator Agent. **Human directly invokes and reviews S1**; no implicit Pairing → Space execution channel.
- Target-project Human-approved product meaning, requirements, design authority and protected writes take precedence over solution preferences and Agent-local best practices.
- **Allowed in formation draft:** design, contract reasoning, documentation, solution review and bounded preflight planning.
- **Potential authorized invocation:** read specified project sources, analyze current baseline and write solution artifacts only to approved project-owned locations; shared OpenAPI/spec changes are **not** automatically authorized. No feature-code or privileged auth/role implementation writes.
- **Excluded:** re-opening settled product commitments without evidence; using previous C1 implementations as source of truth; coding/deploying production features; independent integrated-product assurance; selecting actual project write paths without authorization; claiming real runtime evidence before execution.

## External contracts

- [Generic input and conformance](contracts/input.md): accepted scoped authority, target revision, constraints and assignment permissions; reject missing/contradictory material inputs.
- [Generic output](contracts/output.md): material decisions, cross-boundary responsibilities/interfaces, state/experience semantics, downstream verification obligations, trace and review/evidence, unresolved items with accurate delivery verdict. When consumers require separately addressable contracts (e.g., shared FE/BE API interface), list them as typed payload artifacts with explicit authority/approval standing; S1 is not automatically permitted to modify project-owned OpenAPI.
- Each output distinguishes **produced/reviewed** from **Human accepted for downstream use**. Output may be high quality but not yet authorized as binding project contract.
- The Space may choose details within expressly delegated solution authority. It must escalate material product changes, security approvals and unresolved inter-consumer contract obligations.

## Physical composition

[Input–output chain](composition/input-output-chain.md) maps authoritative inputs → responsible Specialists → intermediate/final artifacts and consumers; [interaction sequence](composition/interaction-sequence.md) illustrates authorized kickoff, execution handoffs, review feedback and separate Human acceptance. [Responsibilities](composition/responsibilities.md) defines the **[Space Coordinator Agent](agents/space-coordinator/profile.md)** and four scoped Specialist roles: Requirements Analyst, Solution Architect, Experience Specialist and Solution Reviewer. The Coordinator owns internal task coordination, not Product Authority or independent review. All Agent definitions remain **declarative and UNVERIFIED** until real runtime evidence demonstrates execution and required isolation.

## Execution modes and Human gates

- **Supervised (default):** the Human interacts directly with S1 Coordinator, reviews material milestone artifacts and authorizes continuation at the selected supervision points. Routine supervision `continue` does **not** approve a material project decision.
- **Autonomous:** only when **explicitly selected by the Human for the concrete invocation**. Coordinator may handle internal authorized Specialist routing without optional review pauses, but may not ignore declared Human gates or expand runtime authority.
- [S1 Human Approval Gates](composition/human-approval-gates.md) distinguish formation, invocation, conditional owner decisions/protected actions and final downstream acceptance. **Consequential transitions**, not each Specialist handoff, trigger mandatory approval in **both modes**. All gate evidence and permitted resume scopes are revision-bound. Mode choice cannot waive a gate.
- Coordinator and Specialist capabilities are **harness-neutral**. Actual Codex/subagent dispatch, context independence and secure pause/resume are unverified and belong to Harscode-level harness translation and invocation binding, not Space policy.

## Artifacts, knowledge, execution requirements and state

- [Artifact format and traceability](artifacts/format-and-traceability.md) describes reusable artifact semantics, identifiers, provenance and contract checks, not a universal parser.
- [Delivery bundle](artifacts/delivery-bundle.md) owns the logical external handoff, including a revision-pinned index of **multiple typed, consumer-relevant artifacts**. [Shared minimum handoff semantics](../../space-formation/contract-and-readiness.md) govern cross-Space discoverability; no fixed file count or mandatory API document is implied.
- Specialist-local guidance, guardrails and knowledge and Coordinator-local profile/guidance/guardrails/kickoff are under [agents](composition/responsibilities.md); local guidance cannot create competing authoritative truth.
- [Kickoff and preflight](invocation/kickoff-prompt.md), [state/handoff](invocation/state-and-handoff.md), and [harness-neutral execution requirements](composition/execution-requirements.md) define capability needs and truthful readiness checks. Harness-native translations are owned outside the Space by Harscode `harness-optimization/`; project/runtime bindings supply actual tool, model, context and permission details. This Space does not create a scheduler or automatic Agent dispatcher. Coordinator responsibilities are declared, not proof of native Agent installation.

## Quality, failure and evolution

Output is potentially consumable only when every applicable source invariant is covered, cross-boundary decisions and interfaces are internally consistent, material uncertainties are resolved or explicitly block consumption, provenance is accurate, and reviewer findings are reconciled. The independent downstream assurance must consume original project acceptance authority directly.

Use **COMPLETE** for conforming delivery with explicitly declared limits; **PARTIAL** when only some required artifacts are produced; **BLOCKED** for missing authority/approval/preconditions; **FAILED** for unsuccessful production; **UNVERIFIED** when claimed checks were not run. No result state implies Human acceptance or runtime verification without evidence.

A future change to generic contracts or Agent knowledge requires review of actual affected consumers; pin active invocation definitions, do not silently mutate them. Any first real-use test requires **Human-direct** invocation after separate formation approval, declared mode and gates, and evidence that the selected runtime can satisfy the Space's requirements. A project's concrete owner/approver is resolved from its current authoritative binding.
