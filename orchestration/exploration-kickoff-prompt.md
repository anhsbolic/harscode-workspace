# Orchestrated Exploration Kickoff

Thin wrapper for running canonical Harscode Exploration under Orchestrator Protocol v0.1. It does not re-author Exploration.

## Required inputs

```text
HARSCODE_WORKSPACE_ROOT
WORK_UNIT_ID
RUN_ID
RUN_PATH
ROLE = Explorer
TASK
CODEBASE_CONTEXT
PRIOR_ARTIFACTS = none or explicit relevant current-effective inputs
optional SPECIALIZATION / PARTICIPANT / SESSION / WORK_UNIT_PATH / PROJECT_LANGUAGE_PROFILE / Ticket / Area
```

## Invocation

```text
Run the canonical Exploration contract from:
{HARSCODE_WORKSPACE_ROOT}/workflow/1-exploration-kickoff-prompt.md

Apply orchestration identity/path semantics from:
{HARSCODE_WORKSPACE_ROOT}/workflow/orchestrated-run-overlay.md

Work Unit: {WORK_UNIT_ID}
Run: {RUN_ID}
Run path: {RUN_PATH}
Role: {ROLE}
Specialization: {SPECIALIZATION if any}
Participant: {PARTICIPANT if known}
Session: {SESSION if known}
Project language: {PROJECT_LANGUAGE_PROFILE if defined}

Task: {TASK}
Codebase context: {CODEBASE_CONTEXT}
Ticket: {ticket/link if any}
Area: {known area or "not sure yet"}

For this Run, write durable Exploration evidence under {RUN_PATH}, not an
ordinal legacy TASK_PATH phase directory. When a project language profile is
provided, use it for human-facing prose while preserving canonical Harscode
terms/enums and code/API/schema identifiers. Stage 1 remains the canonical hard
stop. Do not steer Exploration toward expected gaps, Work Units, or solutions.
```
