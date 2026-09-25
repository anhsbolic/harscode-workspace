# AGENTS.md — orchestration/

This is the HOT router for Harscode orchestration. Read this when work is coordinated as Work Units/Runs or when current delivery state, blockers, decisions, or routing must be understood.

## Hard rules

- Orchestration coordinates approved work; it does not create product, design, security, or project-domain authority.
- Work Unit identity is logical and independent from repository path, issue, session, harness, or workflow phase.
- Run is one workflow execution occurrence. Participant is the assignee; Session is only execution context.
- When authority is missing or conflicting, escalate through the applicable Decision path instead of inventing an answer.
- Re-entry into a workflow phase creates a new Run and requires a meaningful delta.
- Current state must be reconstructable from durable orchestration records; filesystem ordering is never workflow chronology.
- Keep Work Unit definition, current state, append-only history, and Control Surface projection semantically separate. Current-state fields have one active value; historical transitions belong in Events.
- Cross-Work-Unit dependency topology is owned by the Work Graph; do not create a second independently maintained dependency truth inside Work Unit records.
- Orchestrated Runs receive identity, current-effective inputs, execution-envelope authority, model-routing evidence, and Session-continuation hooks through `run-contract.md`. These dispatch fields operationalize settled authority; they do not create new project/workflow authority.
- Load only the smallest applicable knowledge for the current role, specialization, task scope, and workflow phase.

## Routing

- Protocol semantics and object boundaries → `protocol-v0.1.md`
- Run/session/workspace invocation contract → `run-contract.md`
- Role-specialization guidance routing → `specializations/README.md`
- Engineering workflow execution → `../workflow/AGENTS.md`
- Portable engineering guidance → `../best-practices/AGENTS.md`

Project-specific product truth, Work Unit definitions, Control Surface state, and Harscode Spaces belong in the target project, not this workspace.

## Local runtime configuration

- Machine-local paths, available model registry, Human ownership, and model-selection gates → `local-runtime-config.md`
