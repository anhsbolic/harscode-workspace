# AGENTS.md — orchestration/

This is the HOT router for Harscode orchestration. Read this when work is coordinated as Work Units/Runs or when current delivery state, blockers, decisions, or routing must be understood.

## Hard rules

- Orchestration coordinates approved work; it does not create product, design, security, or project-domain authority.
- Work Unit identity is logical and independent from repository path, issue, session, harness, or workflow phase.
- Run is one workflow execution occurrence. Participant is the assignee; Session is only execution context.
- When authority is missing or conflicting, escalate through the applicable Decision path instead of inventing an answer.
- Re-entry into a workflow phase creates a new Run and requires a meaningful delta.
- Current state must be reconstructable from durable orchestration records; filesystem ordering is never workflow chronology.
- Load only the smallest applicable knowledge for the current role, specialization, task scope, and workflow phase.

## Routing

- Protocol semantics and object boundaries → `protocol-v0.1.md`
- Run/session/workspace invocation contract → `run-contract.md`
- Role-specialization guidance routing → `specializations/README.md`
- Engineering workflow execution → `../workflow/AGENTS.md`
- Portable engineering guidance → `../best-practices/AGENTS.md`

Project-specific product truth, Work Unit definitions, Control Surface state, and Harscode Spaces belong in the target project, not this workspace.
