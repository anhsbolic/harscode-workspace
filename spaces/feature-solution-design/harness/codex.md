# S1 Codex Harness Binding — Unverified Research Candidate

**Status:** Declarative mapping proposal, not confirmed native CLI behavior, configured agents, sandbox rights, model access or multi-agent dispatch.

## Responsibilities at invocation

The authorized operator/coordinator must ensure each Specialist assignment receives exactly: selected profile + scoped guidance/guardrails, relevant agent-owned knowledge (not all other Agents' knowledge), pinned I1–I4 references, current required intermediate outputs, and precise output destination/verification role.

**Agent Profile ≠ Codex configuration.** Actual prompts, model choice, tool access, isolated context and write rights must be verified in the installed Codex version for the first real use. Do not imply that writing `agents/*/profile.md` creates native Codex agent identities.

## Conservative first-use method

- Prefer bounded, explicitly addressed Codex sessions for producer roles; use the native sub-agent mechanism only if its existence and isolation are actually verified. Human/Balad handles external gating, Space coordinator handles internal handoffs.
- Requirements Analyst produces X1; Architect produces O1/O2; Experience Specialist produces O3; Reviewer separately receives original authority plus the current outputs and produces O4/O5. Tasks may iterate, but output pointers and revision checks must remain coherent.
- Reviewer should run in a fresh context without treating the producers' explanations as evidence. If isolation cannot be demonstrated, mark `REVIEW INDEPENDENCE UNVERIFIED` rather than claim independent assurance.
- Each producer may write only the approved solution-artifact scope. Reviewer is read-only for producer artifacts and may write only review/evidence files if separately authorized.
- No background jobs, daemon, scheduler, hidden process manager, automatic branch switching, unsafe sandbox flags or global registry is introduced by this definition.

## Model / effort suggestions

| Responsibility | Needed capability; effort guidance (nonbinding) |
| --- | --- |
| Requirements Analyst | High-fidelity source reasoning and traceability; medium for ordinary bounded work, consider high when authority contradictions are real |
| Solution Architect | Cross-boundary design and security/consistency tradeoffs; high when difficult coupled decisions, medium for straightforward scoped work |
| Experience Specialist | UX state and product semantics; medium ordinarily, high for consequential multi-path ambiguity |
| Solution Reviewer | Independent critical contract/source comparison; high for security/cross-interface complexity, medium for small bounded designs |

No model IDs or universal effort permissions are baked into S1. Read Human-owned `<workspace-root>/.harscode-local.yaml` `available_models`, follow [Balad Model Routing](../../../pairing/model-routing.md), confirm native runtime availability and use the actual approved option; missing/contradictory eligibility → `NOT READY`, no fallback by assumption.

## Readiness report

Before first invocation state actual observations (not guesses): definition SHA/formation approval, C1 project source SHA, model+effort eligibility and runtime capability, exact file/tool sandbox scope, specialist context separation method, original-reviewer source routing, artifact/state location and reconstructability, required protected approvals, and what cannot yet be verified.

Codex could execute a correct design yet fail strict conformance; conversely a complete profile is not proof of functioning dispatch. No C1 engineering implementation belongs to this Space.
