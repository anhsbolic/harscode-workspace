# Feature Solution Design — Reusable Space Candidate

> **Status:** PROPOSED / UNFORMED; research draft, no readiness or invocation evidence.
> **Owner:** Anhar
> **Capability identity:** `feature-solution-design`
> **Definition revision:** the Git commit containing this definition; pin exact SHA when approved. No semantic version number is claimed yet.
> **Formation basis:** Balad's accepted C1 capability-gap request; experimental [formation guidance](../../space-formation/README.md).
> **Scope:** Technology-neutral reusable solution design; each invocation is technology/architecture-aware through current project binding.

## Outcome and value

Transform a sufficiently approved, bounded software feature commitment into a **traceable, implementation-consumable solution contract** across material experience, interface, state, security and persistence boundaries. A future Go, NestJS, Next.js or other producer may consume it if generic and concrete I/O are compatible.

The Space is accountable for a **coherent solution**, not for creating features, making unsupported product decisions or implementing every local engineering detail.

## Authority, permissions, and exclusions

- Anhar owns formation, reusable-contract changes, material approvals and first invocation decision. ChatGPT may collaborate on design, not own the Space.
- Balad identifies/pins project authority and coordinates external handoff; no autonomous Space definition authoring by Balad.
- Target-project Human-approved product meaning, requirements, design authority and protected writes take precedence over solution preferences and Agent-local best practices.
- **Allowed in formation draft:** design, contract reasoning, documentation, solution review and bounded preflight planning.
- **Potential authorized invocation:** read specified project sources, analyze current baseline and write solution artifacts only to approved project-owned locations; shared OpenAPI/spec changes are **not** automatically authorized. No feature-code or privileged auth/role implementation writes.
- **Excluded:** re-opening settled product commitments without evidence; using previous C1 implementations as source of truth; coding/deploying production features; independent integrated-product assurance; selecting actual project write paths without authorization; claiming real runtime evidence before execution.

## External contracts

- [Generic input and conformance](contracts/input.md): accepted scoped authority, target revision, constraints and assignment permissions; reject missing/contradictory material inputs.
- [Generic output](contracts/output.md): material decisions, cross-boundary responsibilities/interfaces, state/experience semantics, downstream verification obligations, trace and review/evidence, unresolved items with accurate delivery verdict.
- Each output distinguishes **produced/reviewed** from **Human accepted for downstream use**. Output may be high quality but not yet authorized as binding project contract.
- The Space may choose details within expressly delegated solution authority. It must escalate material product changes, security approvals and unresolved inter-consumer contract obligations.

## Physical composition

[Path relation graph](composition/path-relations.md) maps input → responsible Specialist → intermediate output → reviewer/consumer. [Responsibilities](composition/responsibilities.md) defines the proposed four scoped Specialist packages: Requirements Analyst, Solution Architect, Experience Specialist and Solution Reviewer. These are draft capability responsibilities, **not proof that four independently runnable Codex Agents exist**. The Space coordinator is an internal responsibility, not an assumed service/Agent.

## Artifacts, knowledge, harness and state

- [Artifact format and traceability](artifacts/format-and-traceability.md) describes reusable artifact semantics, identifiers, provenance and contract checks, not a universal parser.
- [Delivery bundle](artifacts/delivery-bundle.md) is the format for durable, consumer-oriented final output.
- Specialist-local guidance, guardrails and knowledge are under [agents](composition/responsibilities.md); agent knowledge may duplicate another Agent, but cannot create competing authoritative truth.
- [Kickoff and preflight](invocation/kickoff-prompt.md), [state/handoff](invocation/state-and-handoff.md), [Codex harness binding](harness/codex.md) are scoped instructions. They do not create a scheduler, native multi-agent runtime, or unrestricted model routing.

## Quality, failure and evolution

Output is potentially consumable only when every applicable source invariant is covered, cross-boundary decisions and interfaces are internally consistent, material uncertainties are resolved or explicitly block consumption, provenance is accurate, and reviewer findings are reconciled. The independent downstream assurance must consume original project acceptance authority directly.

Use **COMPLETE** for conforming delivery with explicitly declared limits; **PARTIAL** when only some required artifacts are produced; **BLOCKED** for missing authority/approval/preconditions; **FAILED** for unsuccessful production; **UNVERIFIED** when claimed checks were not run. No result state implies Human acceptance or runtime verification without evidence.

A future change to generic contracts or Agent knowledge requires review of actual affected consumers; pin active invocation definitions, do not silently mutate them. First C1 test is a separate Anhar-authorized experiment after formation approval and actual Codex readiness evidence.
