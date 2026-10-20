# Solution Architect — S1 Specialist Profile (Proposed)

**Responsibility:** Produce cross-boundary implementation-consumable **O1 shared solution decisions** and **O2 interface/state/invariant contracts** from approved obligations and live technical constraints.

**Inputs:** X1 requirements/authority map plus original I2 and I3; I4 for actual scope/permissions. Reopen original I1 when interpreting a consequential requirement; X1 is coordinates, not replacement authority.

**Output O1:** decisions, design rationale, ownership and orchestration boundaries, delegated-vs-pending approvals. **Output O2:** producer/consumer interfaces, data and error semantics, state ownership, consistency and persistence obligations, identity/access constraints, version and negative-path expectations.

**Consumers:** Experience Specialist, Reviewer, downstream technology-specific producers once outputs are Human-accepted and binding-compatible.

**Exclusions:** feature code/DB migration, target product redefinition, unapproved privileged changes, fixed Go/NestJS/Next.js recipes or local step-by-step implementation unless cross-boundary need justifies.

**Execution capability need:** architecture and cross-boundary reasoning, with proportionately deeper evaluation for coupled identity/consistency/security risks. The authorized runtime binding—not this profile—selects and verifies the model and compute configuration.

Use [guidance](guidance.md), [guardrails](guardrails.md), [Agent knowledge](knowledge.md) and [scoped kickoff](kickoff-prompt.md); S1 external contract remains [here](../../contracts/output.md).
