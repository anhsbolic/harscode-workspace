# Balad Workspace Initialization — Station 5 Research v0

> **Status:** Experimental guidance on `research/harscode-purpose-llm-fit`. Not operational Harscode `main`, a completed workspace initialization, or authorization for Space execution.
> **Purpose:** Enable one short Human request, given the **absolute path** of a workspace root, to bootstrap a discoverable, locally configured Balad entrypoint for future Codex CLI sessions.
> **Authority:** Human explicitly approves the workspace-init write scope. Root/project instructions and security permissions remain binding. See [Balad entrypoint](AGENTS.md) and [Model Routing](model-routing.md).

## Applicability and ownership

Use when the Human wants a multi-repository workspace root (for example, a folder containing `harscode-workspace/`, `harscode-state/`, and `kencleng/`) to become the working directory for future Balad sessions. This is **workspace environment bootstrap**, not project initialization, Space creation, engineering production or a new orchestration state model.

- `harscode-workspace/`: reusable Harscode guidance and research definitions. `main` remains operational; Station 5 candidate guidance is scoped to research branch.
- `harscode-state/`: proposed location for mutable, active operational continuity; discovering a folder does **not** authorize populating it or establish a schema.
- `kencleng/` or other target repositories: own product authority, source, accepted outputs and applicable local project instructions.
- **Workspace root:** owns a thin, local routing file `AGENTS.md` and a machine/operator-local `.harscode-local.yaml`. It must not become competing project authority.

The workspace root may not itself be a Git repository. Do not require one or run a repository-wide `git init` to make Balad work. For tracked roots, respect Git status and do not commit local config by default.

## Bootstrap from a short Human instruction

Example Human intent: "Lur, init Harscode workspace di <absolute-path>, cek yang sudah ada, siapkan AGENTS.md dan local config saja."

1. **Locate:** Resolve the supplied absolute root path; confirm it exists, is the intended directory, and contains the expected Harscode research checkout. Do not infer a user home path, create a new root or change current Git branches. Inspect symlinks and out-of-root references before trusting paths or writing.
2. **Ground:** Read current `harscode-workspace/AGENTS.md`, `pairing/AGENTS.md`, relevant research guidance, existing root `AGENTS.md` and `.harscode-local.yaml` if present. Discover project repositories from actual directories, not assumed names. Verify Harscode research branch/ref and project branch where needed; report mismatches rather than silently checking out.
3. **Plan:** Propose only the precise root files to create or minimally reconcile, preserving user/local instructions and any existing config. For a missing config initialize `available_models: []` and let the Human populate its entries later. Show unexpected conflicts and ask the Human before replacing competing instructions, changing user-authored model policy, moving files or expanding write scope.
4. **Authorize and write:** Only after explicit Human authorization for these **root-local files**, perform bounded file creation/editing. When starting Codex in `harscode-workspace/`, its default sandbox may not allow writes to the parent root; do not bypass permissions with symlink tricks, blanket unsafe flags or command delegation. Request a safe scoped approval or have Human apply the proposed patch if necessary.
5. **Verify:** Check created file content and path resolution, routing to Balad and project-owned `AGENTS.md`, no accidental repository changes, no secret leakage and idempotent behavior when invoked again. Distinguish **workspace routing ready** from **model routing ready** and **Space invocation ready**.
6. **Handoff:** Tell the Human how to start a new Codex CLI session **at workspace root**, and that a normal short Balad prompt may now be used. Do not bootstrap Space operational state or dispatch work.

## Workspace-root AGENTS.md — minimum intended behavior

Keep it short. It should:
- Route "Balad", "Lur", "Dulur", Human–Agent Pairing and Space readiness/formation requests to `harscode-workspace/pairing/AGENTS.md`; load `space-formation.md` only when triggered.
- Route `workspace-init` requests to `harscode-workspace/pairing/workspace-init.md`; model choice requests to `harscode-workspace/pairing/model-routing.md`.
- Point to `.harscode-local.yaml` for non-authoritative local path and runtime/model metadata. This file is **not** native Codex configuration or an authorization grant.
- Instruct agents to read each target repository's own root/scoped `AGENTS.md` and owning project authority before project actions; parent instructions do not override protected project paths or Human decisions.
- State that research-only Space-oriented guidance does **not** replace Harscode `main` globally, and Balad's default readiness discussion is read-only.

Do not copy entire Balad guidance into workspace-root `AGENTS.md`. Avoid duplicate policy and don't shadow an existing root instruction without meaningful reconciliation.

## Local config — minimum shape

`<workspace-root>/.harscode-local.yaml` is local/operator-controlled metadata. Resolve **all paths relative to this file's parent directory**, not to the current shell working directory.

```yaml
communication_language: Bahasa Indonesia

paths:
  workspace_root: .
  harscode_workspace_root: ./harscode-workspace
  harscode_state_root: ./harscode-state

projects:
  kencleng:
    root: ./kencleng

runtime:
  harness: codex-cli

# Human-owned model inventory and per-effort selection policy.
# Balad leaves it empty during workspace initialization.
available_models: []
```

- The model registry is part of **minimum structural config** because Balad will later select models for Specialist Agents in Spaces. An empty registry is valid for initial workspace discovery and **read-only Pairing assessment**, but **not sufficient for model-dependent Space invocation**.
- **Human owns and populates `available_models`**, including model IDs, qualitative capability hints, cost tiers and each configured model+effort policy. Workspace initialization must **not** discover/fill models by default, copy entries from an old pilot or grant unrestricted usage. Balad may identify gaps and offer an exact proposed change; only Human-approved edits may be applied within separately authorized write scope.
- The current schema uses `reasoning_efforts: {effort: allowed | human_approval}` per model; see [Model Routing](model-routing.md) for authoritative research semantics. Do **not** emit legacy `approval_required`, `supported_reasoning_efforts` or `auto_select_efforts` in new configs. An existing old-style registry needs explicit Human reconciliation, not silent conversion.
- Do not add default/escalation models, model registries per project, or a launcher service until real use justifies them.
- An actual Codex model/effort must be selected through the runtime's supported controls; writing Harscode YAML **does not switch or provision** Codex models.
- `harscode_state_root` is **only a path pointer**. Never auto-create `harscode-state` contents, a snapshot, audit history or a Run registry.
- Project entries name local repositories and location, not their product authority, branch selection, approved task or identity.

## Data security and reproducibility

Prefer local-only, untracked config. If root is Git-tracked, ignore `.harscode-local.yaml` unless a separately authorized public-safe pilot artifact is deliberately committed. Do not include credentials, auth tokens, connection strings, full home directories as committed examples, private endpoints, secrets or sensitive model-access data. Local absolute workspace path is supplied at runtime and should not be hardcoded in reusable Harscode guidance.

Initial bootstrap must be **idempotent**: if files already conform, report ready without rewriting. If a file is present but contradictory, propose a minimal change; do not reset user-chosen configuration or model policy. If write access to parent is absent, leave a clear bounded patch and exact blocker instead of claiming success.

## Exit and evidence

Report concrete observed:
- Resolved workspace root and discovered Git repositories / checked branches where relevant.
- Files **created / updated / unchanged / blocked**.
- Root Balad routing and each configured relative path successfully resolved (or why not).
- Runtime harness declaration versus actual CLI/tool availability, including unverified claims.
- Model registry status: missing, empty, Human-configured, needing legacy-policy reconciliation, or runtime-invalid; do not equate config presence with availability or a runnable route.
- Next safe action and any required scoped Human decision.

`workspace-init` is complete only for the checks actually performed. It **never** certifies a formed Space, appropriate model selection, valid C1 project authority, or authorized execution.
