# Human Pairing

This area is a Human-facing operator handbook for working with Harscode and Orchestrator Protocol v0.1.

It does not define product authority, workflow phase authority, engineering correctness rules, or agent behavior. Those remain owned by their canonical Harscode areas.

Use this area to understand how a Human should operate the system without becoming the prompt engineer for every Run.

## Scope

Human Pairing guidance covers:

- Human Authority versus Orchestration Operator responsibilities;
- how to approve, correct, or escalate without rewriting agent prompts;
- how to interpret Work Unit / Run / Session state;
- how to handle session continuation and context hygiene;
- how to work with model selection and approval gates;
- how to preserve durable evidence instead of relying on chat memory.

## Reading map

- Session continuity and context hygiene → `session-continuity.md`
- Runtime/model configuration and approval mechanics → `../orchestration/local-runtime-config.md`
- Orchestration objects, state, routing, Decisions, Runs → `../orchestration/protocol-v0.1.md`
- Workflow phase behavior and checkpoints → `../workflow/`

## Operating principle

The Human should communicate intent, decisions, approvals, corrections, and protected authorizations.

The Orchestrator and durable Run artifacts should carry execution semantics.

Prefer:

```text
Stage 1 Approved, lanjut ke Stage 2.
```

over restating the workflow, authority hierarchy, scope, model choice, and solution constraints in every Human message.

If an agent requires repeated Human prompt engineering to follow already-durable instructions, treat that as system/pilot evidence rather than normal operating procedure.

## Boundary

Human-facing guidance may summarize canonical semantics for usability, but it must link back to the owning Harscode source and must not silently redefine it.
