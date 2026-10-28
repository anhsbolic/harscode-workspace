# Engineering Runtime Binding

> **Status:** WORKING / RESEARCH-ONLY. A verification contract, not an automatic checklist to run for every Product/Design discussion.

## Required binding

Before a **concrete Engineering Space invocation**, identify:

| Concern | Evidence required |
| --- | --- |
| Space definition | Actual approved capability/revision and the requirements that need translation |
| Project binding | Target repo/branch/SHA, approved inputs, consumers, output/state destinations |
| Human authority | Direct authorized assignment, permitted actions, protected paths, material gates and selected execution mode |
| Runtime inventory | Actual CLI/host version, enabled models, tools, session/subagent support and effective sandbox permissions |
| Source/context access | Original project authority can be opened by every role that requires it |
| Artifact containment | Effective allowed write scope is enforced or an explicit scoped deviation is recorded |
| Specialist context | Role-specific knowledge/guardrails are available without unnecessary global loading |
| Independence | Reviewer can inspect source and producer output in meaningfully independent context; evidence, not an agent title |
| Handoff durability | Output revision, owner, source references, decisions and stop/resume state survive session loss where required |
| Human gates | Actual blocking/enforcement before consequential changes, valid only for the approved scope/revision |
| Evidence | Performed tests, review and tool results distinct from planned actions; unknowns reported honestly |

Relevant requirements depend on the **approved Space definition**. For historical Rancang reference these were R1–R8; a new candidate cannot claim runtime fitness just because it lists them.

## Local workspace state-path routing (research guidance)

When a task needs to **locate or propose storage for Harscode assignment state and working solution artifacts**, read the operator-owned `<workspace-root>/.harscode-local.yaml`, **if actually accessible**. All relative values resolve from the **directory containing that file**, never from the current shell directory. This local config chooses a *candidate physical destination*, **not** artifact authority, approved scope, automatic directory creation, write permissions or a native Codex configuration. Project-owned source/accepted-output authority and project instructions still prevail.

For a selected `projects.<project_id>`, resolve the location using this order:

1. Explicit `projects.<project_id>.harscode_state_root` override, when configured.
2. Otherwise `paths.harscode_state_root/<project_id>` as the workspace-level default **candidate**, if configured and accessible.
3. If no trustworthy candidate can be resolved, report the path gap and ask for the specific destination during assignment authorization. **Do not guess** a project `docs/` directory or silently fall back to an unrelated historical run.

For example, the local Kencleng research override may be:

```yaml
projects:
  kencleng:
    root: ./kencleng
    harscode_state_root: ./kencleng/docs/engineering
```

With the example override, an authorized `ORG-01` Rancang assignment can **propose** a new project-conventional location under `kencleng/docs/engineering/`, distinct from earlier run records. A future operator may choose `./harscode-state/kencleng` instead. Neither move changes where effective Product/Design/Engineering decisions are owned. External storage is usable only if its durability, access, versioning and a discoverable project-owned reference satisfy the actual consumers; otherwise report the gap rather than claim downstream readiness. Existing run artifacts are never migrated automatically.

**Awareness versus access:** Balad may consult the resolved path for **advisory discovery**; Human-direct Coordinator resolves the assignment's exact writable destination and provides scoped paths to Specialists. Each Agent that materially needs path context must use this same resolution rule, but **need not load the entire YAML/model registry**. Verify real files, path normalization/symlinks, repository ownership and effective tool permissions before a consequential action. A configured path never authorizes a write, bypasses Human gates or makes an independent review claim true.

## Execution modes

Default to direct Human-authorized **supervised** work. Autonomous/delegated execution needs separate explicit authorization and effective Human gates. A normal Coordinator session can establish readiness before requesting actual production; do not invent a separate mandatory preflight-only invocation.

Where a tool allows broader writes than the task permits, state the exact unenforced boundary and do not claim full containment. A Human may authorize a scoped experimental deviation only where the consequential risk is acceptable and existing project protections remain intact. Approval of wider *tool access* is not permission for unrelated changes.

Do not assume approval persists after a material change to definition, project revision, objective, code boundary or affected artifact. Stop or re-authorize the affected work.

## Status

Record verified properties, limitations, provenance and exact revisions. Use `READY` only if all **material** requirements for that assignment are actually satisfied. Otherwise report `NOT READY`, `PARTIAL`, or a specific `UNVERIFIED` requirement. Keep the evidence near the actual authorized invocation in its owning project/execution state, not a central Harscode run registry.
