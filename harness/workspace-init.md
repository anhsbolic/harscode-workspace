# Workspace Init — Local Harscode Routing Bootstrap

> **Standing:** WORKING / RESEARCH-ONLY on `refactor/harscode-foundation`. Local bootstrap guidance, **not** a command, completed setup claim, Space authorization, or an operational `main` policy.
> **Owner:** Harness for workspace-local path/config and routing setup. [Collaboration / Balad](../collaboration/pairing.md) owns advisory behavior; [Engineering](../engineering/README.md) owns Space capabilities; target repositories own project truth.

## Scope and entry

On a Human request to initialize or repair a multi-repository Harscode workspace, prepare **only** its root `AGENTS.md` and `.harscode-local.yaml` unless separate exact write scope is approved. An existing workspace may include `harscode-workspace/`, `kencleng/`, and optional `harscode-state/`; none is a mandatory directory name or an instruction to create/populate state. The workspace root need not be a Git repository.

Human may say "Mang, perbaiki workspace init di sini" when the root is unambiguous from the actual environment, or supply its absolute path. Do not demand a long setup form. An ordinary "Mang, kita kerjain ORG-01 ya" **starts advisory project discovery**, not workspace initialization, a Space invocation or automatic writing.

## Inspect → reconcile → authorize → verify

1. **Locate:** Determine the real intended workspace root; inspect existing files, directory ownership, symlinks and any path escapes. Confirm actual Harscode checkout and its branch/revision. Do not guess a home directory, run `git init`, create a new workspace root, switch branches or silently manipulate project repositories.
2. **Read current guidance:** Read the actual `harscode-workspace/AGENTS.md`, [Balad guidance](../collaboration/pairing.md), [local state-path routing](runtime-binding.md#local-workspace-state-path-routing), and the target project's root/scoped `AGENTS.md` only as relevant. **Never reactivate `deprecated/legacy/pairing/` to make a broken path resolve.**
3. **Reconcile:** Check workspace-root `AGENTS.md` against the active paths below, and `.harscode-local.yaml` against the actual workspace. Preserve unrelated local instructions, configured model entries, explicitly chosen project overrides and YAML comments. For mismatches propose **minimal, reviewable edits**, not a blind overwrite or a migration of old run artifacts.
4. **Authorize:** Obtain explicit Human approval for the actual root files/changes before creating or editing them. If the CLI's sandbox doesn't permit writing the parent/workspace root, report the limitation and provide a bounded patch; do not bypass with unsafe flags/symlinks or request blanket writable access.
5. **Verify:** Re-read edited files, check resolved targets and scoped path safety, ensure no stale active `pairing/` routing, inspect Git/untracked effects where applicable, and rerun the same reconciliation logically to ensure **idempotence** (no changes on a second run). No mandatory script or automatic daemon is implied.
6. **Report:** Identify created/updated/unchanged/blocked files, selected Harscode/project refs, actual path resolution and unresolved gaps. **Workspace routing configured** is distinct from runtime model availability, Harness readiness, Space invocation and project-artifact acceptance.

## Workspace-root AGENTS.md — minimal routing template

Use this as a **content baseline** for an absent or obsolete workspace-root router. Resolve `paths.harscode_workspace_root` from the YAML; the example below assumes its actual resolved value is `./harscode-workspace`. If it differs, adjust the links **to the existing checkout** rather than hardcoding a nonexistent directory. Do not replace additional operator instructions unnecessarily.

```markdown
# Workspace Routing

- Read `.harscode-local.yaml` for local project locations, optional project state-root overrides, runtime declaration and Human-owned model inventory **when relevant**. Resolve paths from that file's directory. It is not authority, native Codex configuration or write permission.
- For "Mang", "Balad", "Lur", "Dulur" or Human–AI pairing, read `harscode-workspace/AGENTS.md` and `harscode-workspace/collaboration/pairing.md`. Short intents start permitted read-only discovery; Balad advises Human and does not invoke or coordinate a Space.
- For workspace initialization/repair, read `harscode-workspace/harness/workspace-init.md`. For runtime/tool/model capability checks, consult `harscode-workspace/harness/README.md` and actual runtime inventory. No model/effort is authorized by a filename alone.
- For a target project, resolve `projects.<id>.root` in local config and read that repository's root and applicable scoped `AGENTS.md` plus owning effective sources/revisions. Prior chats and history do not replace project authority.
- For Engineering capabilities/formation, consult `harscode-workspace/engineering/README.md` and `harscode-workspace/engineering/space-formation.md` as relevant. For Human-direct Rancang, use `harscode-workspace/engineering/spaces/feature-solution-design/README.md` and exact formation approval. Balad has no dispatch channel.
- For assignment state and working artifacts, follow `harscode-workspace/harness/runtime-binding.md`: project `harscode_state_root` override first, else configured workspace state root plus project ID. The resolved location is a candidate; exact destinations, writes and consequential actions still need Human authorization.
- Follow project protections and Human gates. `harscode-workspace/deprecated/` is historical evidence only. Foundation Refactor is research-only; Harscode `main` remains the operational baseline.
```

These are navigation hints for **the actual discovered checkouts**. They do not preload every domain, install a Coordinator, alter Codex's native `AGENTS.md` precedence, or supply a universal workflow.

## Local YAML — minimal shape, not an executable profile

Only create a new config when missing and the Human approves it; retain existing configured values otherwise. Resolve every relative path from the **directory containing the YAML**, never the shell CWD. Example for a workspace with a discovered Kencleng checkout (omit the project entry if it is not actually present):

```yaml
communication_language: Bahasa Indonesia

paths:
  workspace_root: .
  harscode_workspace_root: ./harscode-workspace
  harscode_state_root: ./harscode-state

projects:
  kencleng:
    root: ./kencleng
    harscode_state_root: ./kencleng/harscode-state

runtime:
  harness: codex-cli

# Human-owned inventory; workspace-init never invents entries.
available_models: []
```

- **State selection:** use `projects.<id>.harscode_state_root` if present; otherwise use `paths.harscode_state_root/<id>`. Config does not auto-create directories, migrate Run #1 or make a destination writable. An absent or unsafe location is a reported gap; don't substitute `docs/engineering` without authorization. Durable project-owned state/accepted output and discoverable work references must remain correct regardless of storage layout.
- **Model policy:** Human owns `available_models`. Preserve model IDs, `capabilities`, `cost_tier`, and per-model `reasoning_efforts: {effort: allowed | human_approval}`. Empty `[]` is valid for advisory discovery, **not** evidence of a runnable model-dependent Space. `allowed` removes only an additional *model-choice* gate inside an otherwise Human-authorized assignment; `human_approval` needs that exact model+effort and task approval. Missing/unknown effort is not an approval. Do not emit legacy `approval_required`, `supported_reasoning_efforts`, or `auto_select_efforts`, auto-populate models, or silently convert old registry semantics. Verify actual supported models/efforts in the current runtime when needed.
- **Safety:** Do not put secrets/credentials in the YAML or commit operator-local config by default. Check normalized paths, symlinks, access and tool write scope before side effects. `workspace-write` or `on-request` is not semantic Human approval. This initialization never dispatches a Space, changes project authority, installs tools, writes solution artifacts, creates a global registry or certifies Harness R1–R8.

## Safe local repair

For an existing workspace-root `AGENTS.md` that still routes to `harscode-workspace/pairing/AGENTS.md`, `pairing/workspace-init.md` or `pairing/model-routing.md`, treat those links as **obsolete**, inspect the present active checkout, and replace only the affected routing with the current entrypoints above **after scoped Human approval**. Preserve operator-specific paths/preferences and check the new files exist. Do not resolve obsolescence by moving archived files back into active directories.

[Harness](README.md) · [Balad](../collaboration/pairing.md) · [Runtime binding](runtime-binding.md)
