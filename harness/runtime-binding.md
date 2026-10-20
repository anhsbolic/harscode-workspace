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

## Execution modes

Default to direct Human-authorized **supervised** work. Autonomous/delegated execution needs separate explicit authorization and effective Human gates. A normal Coordinator session can establish readiness before requesting actual production; do not invent a separate mandatory preflight-only invocation.

Where a tool allows broader writes than the task permits, state the exact unenforced boundary and do not claim full containment. A Human may authorize a scoped experimental deviation only where the consequential risk is acceptable and existing project protections remain intact. Approval of wider *tool access* is not permission for unrelated changes.

Do not assume approval persists after a material change to definition, project revision, objective, code boundary or affected artifact. Stop or re-authorize the affected work.

## Status

Record verified properties, limitations, provenance and exact revisions. Use `READY` only if all **material** requirements for that assignment are actually satisfied. Otherwise report `NOT READY`, `PARTIAL`, or a specific `UNVERIFIED` requirement. Keep the evidence near the actual authorized invocation in its owning project/execution state, not a central Harscode run registry.
