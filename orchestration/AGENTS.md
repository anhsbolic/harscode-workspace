# AGENTS.md — orchestration/

This is the HOT router for Harscode orchestration. Read this when work is coordinated as Work Units/Runs or when current delivery state, blockers, decisions, or routing must be understood.

## Hard rules

- Orchestration coordinates approved work; it does not create product, design, security, or project-domain authority.
- Work Unit identity is logical and independent from repository path, issue, session, harness, or workflow phase.
- Run is one workflow execution occurrence. Participant is the assignee; Session is only execution context.
- When authority is missing or conflicting, escalate through the applicable Decision path instead of inventing an answer.
- Treat a Human kickoff prompt as intent, not as the workflow specification. In a fresh Orchestrator Session, reconstruct the current frontier from durable project state plus current Harscode guidance before asking the Human to restate decisions, blockers, routing, or dispatch mechanics that are already discoverable.
- When a Human-owned question has a known owner and is decision-ready, facilitate it conversationally in the current interaction: give the bounded context/recommendation and ask the exact decision. Do not substitute a blocker/action report, new Run, or durable-state update for asking the question; reconcile durable state after the Human answers.
- Follow the target project's current-effective communication profile for Orchestrator Human-facing communication and Orchestrator-owned prose when such guidance exists; preserve canonical Harscode terms/enums and technical identifiers where translation would reduce precision.
- Keep source status explicit: distinguish Harscode guidance stated by a source, reasoned interpretation derived from guidance, and target-project authority; do not promote an interpretation into an explicit Harscode rule.
- Before dependent Build, reconcile any material post-approval Decision that makes the current Approved Techplan spine stale through a fresh Planner revision and applicable Review/report/Human approval. Preserve the prior approved spine as predecessor until superseded. After approval, reconcile only affected task snapshots; do not reopen an unchanged decomposition topology merely because task contents were refreshed.
- In Human-Assisted posture, always show the required dispatch package in the Human-facing response; do not require the Human to open the Invocation merely to discover Run/Profile/model/effort/session/working-directory/prompt mechanics.
- Re-entry into a workflow phase creates a new Run and requires a meaningful delta.
- Current state must be reconstructable from durable orchestration records; filesystem ordering is never workflow chronology.
- Keep Work Unit definition, current state, append-only history, and Control Surface projection semantically separate. Current-state fields have one active value; historical transitions belong in Events.
- Cross-Work-Unit dependency topology is owned by the Work Graph; do not create a second independently maintained dependency truth inside Work Unit records.
- Orchestrated Runs receive identity, current-effective inputs, execution-envelope authority, model-routing evidence, and Session-continuation hooks through `run-contract.md`. These dispatch fields operationalize settled authority; they do not create new project/workflow authority.
- Load only the smallest applicable knowledge for the current role, specialization, task scope, and workflow phase.

## Routing

- Protocol semantics and object boundaries → `protocol-v0.1.md`
- Pilot #2 candidate guidance ownership/routing → `pilot-2-candidate/README.md` (do not read the whole candidate directory by default)
- Fresh Orchestrator resume / initial or bounded bootstrap → `pilot-2-candidate/project-orchestration-bootstrap.md`
- Run/session/workspace invocation contract → `run-contract.md`
- Role-specialization guidance routing → `specializations/README.md`
- Engineering workflow execution → `../workflow/AGENTS.md`
- Portable engineering guidance → `../best-practices/AGENTS.md`

Project-specific product truth, Work Unit definitions, Control Surface state, and Harscode Spaces belong in the target project, not this workspace.

## Local runtime configuration

- Machine-local paths, available model registry, Human ownership, and model-selection gates → `local-runtime-config.md`
