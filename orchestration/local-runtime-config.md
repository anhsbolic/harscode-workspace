# Local Runtime Configuration

Local runtime configuration binds an orchestrated target project to machine-local execution context without turning that context into project authority.

The default target-project location is:

```text
.harscode-spaces/.local-config.yaml
```

This file is normally local-only and SHOULD be ignored by Git.

## Scope

Keep this file limited to local/runtime resolution concerns, such as:

- local paths needed to reach Harscode or project resources;
- optional local communication defaults;
- a simple runtime harness binding when one harness is intentionally used for the project;
- models currently available to the human/operator.

Do not store product authority, delivery scope, workflow decisions, credentials, tokens, secrets, or harness-specific commands here.

## Human ownership

The local model registry is **Human-owned, Orchestrator-read-only**.

The Orchestrator MUST NOT:

- add a model;
- remove a model;
- change model capabilities;
- change model cost classification;
- change whether approval is required;
- silently reinterpret a model entry to make dispatch easier.

If the registry is insufficient or appears stale, surface that to the Human.

## Minimal shape

```yaml
communication_language: Bahasa Indonesia

paths:
  project_root: .
  harscode_workspace_root: ../harscode-workspace

runtime:
  harness: codex-cli

available_models:
  - id: example-model
    capabilities:
      - reasoning
      - coding
    cost_tier: standard
    approval_required: false
```

### Model fields

- `id` — exact model identifier meaningful to the operator/runtime.
- `capabilities` — Human-declared capability tags. Keep them factual and useful for routing.
- `cost_tier` — Human-declared relative class: `low`, `standard`, or `high`.
- `approval_required` — whether the Orchestrator must obtain explicit Human approval before dispatching this model.

Additional Human-authored notes MAY exist, but v0 selection must not depend on hidden heuristics.

## Model selection policy

The Orchestrator does not maximize model power. It selects for **fit-for-purpose sufficiency**.

For each Run:

1. determine the minimum capability needs justified by the Role, workflow phase, task scope, and risk;
2. consider only Human-declared available models;
3. prefer a model that sufficiently covers those needs without material capability excess;
4. among sufficiently fitting candidates, prefer the lower declared `cost_tier`;
5. if the selected candidate has `approval_required: true`, stop before dispatch and request explicit Human approval;
6. if no non-gated model is sufficient, request approval for a suitable gated model or ask the Human to revise the registry;
7. never silently fall back to the strongest model merely because it is available.

A model marked `approval_required: true` may be recommended by the Orchestrator, but may not be dispatched until approval is recorded.

## Harness boundary

The v0 config MAY record one simple runtime binding such as:

```yaml
runtime:
  harness: codex-cli
```

This only identifies the operator-selected execution harness for the project. It does not create a harness registry or authorize the Orchestrator to manage harness-specific commands, flags, authentication, tool permissions, or provisioning.

Model capability/cost metadata remains separate from the harness binding.

If real execution later proves that this simple binding is insufficient for correct dispatch, treat that as CRTV evidence before expanding the schema.

## Git behavior

By default, target projects SHOULD add:

```gitignore
.harscode-spaces/.local-config.yaml
```

A project may intentionally commit the file for a bounded validation/pilot when public reproducibility or historical evidence is the purpose.

When committed, use only public-safe values:

- prefer relative paths;
- do not include usernames/home directories;
- do not include credentials, tokens, private endpoints, or other secrets;
- treat model availability as intentionally public evidence.
