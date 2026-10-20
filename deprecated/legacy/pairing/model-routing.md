# Balad Model Routing — Station 5 Research v0

> **Status:** Experimental guidance on `research/harscode-purpose-llm-fit`. Not Harscode operational `main` policy, native Codex configuration, an execution engine or an automatic authorization mechanism.
> **Authority:** Human owns `available_models` inventory, model/effort policy and Space invocation. Balad may inspect and **advise** on model fit but does not select/bind a model for a Space Coordinator or Specialist, invoke a Space or coordinate dispatch. See [Workspace Init](workspace-init.md), [Pairing Composition](space-formation.md) and [Human-led Space Formation](../space-formation/contract-and-readiness.md).

## Intent and scope

Support **Human-directed selection** of a model + configured reasoning effort for each real Coordinator/Specialist assignment, not one immutable model per Space or one model per old workflow phase. Balad's use of this guidance is advisory only. Reusable Agent capability requirements differ from local invocation binding. A configured registry is **Human-declared policy**, not runtime proof of access, competence, pricing, outcome quality or session identity.

Station 5 initially targets one configured `codex-cli` harness. Do not introduce a multi-harness catalog, vendor adapters, automatic fallback, a runtime dispatcher or a model leaderboard before real requirements justify them.

## Human-owned model inventory

`<workspace-root>/.harscode-local.yaml` contains `available_models`. Only the Human decides which model IDs are offered, their task-suitability hints, relative cost preference and each permitted effort's approval state.

Balad:
- MAY read the registry and inspected evidence **on Human request**, point out mismatches and **recommend** a model/effort or a registry change; this advice does not bind a Space.
- MUST NOT autonomously populate the registry during `workspace-init`, self-approve a model or effort, silently broaden availability, or alter the Human's policy to facilitate dispatch.
- MAY mechanically apply **exact Human-approved local configuration edits** after separate scoped write authorization for those files only. This is not permission to open/request a Coordinator session or assign models to Agents.
- MUST NOT treat a missing/empty/old-style entry as unrestricted permission.

## Registry shape and unambiguous effort policy

This is a **generic example**, not a claim that any example-model ID exists:

```yaml
available_models:
  - id: example-model
    capabilities: [reasoning, coding, repository-work]
    reasoning_efforts:
      low: allowed
      medium: allowed
      high: human_approval
    cost_tier: standard
```

Per entry:
- `id`: exact local runtime-recognized identifier. The Human-invoked Coordinator/runtime operator verifies actual access before executing assignments.
- `capabilities`: coarse Human-assessed suitability hints, **not proven benchmarks**. Examples: `reasoning`, `coding`, `repository-work`, `cross-cutting-analysis`. Avoid presenting `security-risk` as a guaranteed model capability; the assignment's risk and assurance duties are separate.
- `reasoning_efforts`: one mapping from **runtime-supported effort name** to the Human's **selection policy** for that *model+effort* pair:
  - `allowed`: the Human-invoked Coordinator/runtime actor may use that model+effort **within a separately authorized invocation and granted tool/scope**, without an additional model-choice approval. Balad may recommend but cannot dispatch or bind this selection.
  - `human_approval`: before the Coordinator/runtime actor selects or dispatches this pairing, **Human approval for that exact model+effort and concrete task scope** is required. If absent, expired or out of scope, stop; Balad cannot approve, request dispatch or silently obtain a broader grant.
- **Absent effort**: not configured/eligible. Do not infer it from vendor documentation or earlier runtime observations. A key being present expresses Human-configured support and policy, but **actual** runtime support/access must still be checked when material.
- `cost_tier`: Human-selected relative resource preference (`low`, `standard`, `high`), not an exact bill, performance ranking or entitlement guarantee.

**No separate blanket `approval_required`, `supported_reasoning_efforts`, or `auto_select_efforts` in this schema.** Their old combinations are ambiguous and **not a recognized grant** under this candidate. Existing configs using old fields require explicit Human reconciliation before a model-dependent invocation; don't silently translate `approval_required: false` to universal `allowed`.

This policy is **fail-closed**: unknown status values, duplicate model entries, unsupported effort names, conflicting old and new fields, missing approval evidence, or runtime mismatch cause `NOT READY` for the affected pairing. Do not choose another model/effort silently to evade a gate.

## Selection, approval and runtime binding

1. The **Human-invoked Coordinator/runtime actor** determines the authorized assignment and relevant Space I/O contract. Balad may give Human-only advisory fit analysis, never operational routing or dispatch.
2. Identify material complexity, uncertainty, code/tool requirements, risk, independence/assurance duties and concrete Specialist capability needs. A larger effort does not inherently make a model safe for a security-critical task.
3. Read the Human-owned registry. Filter for sufficient task fit, supported local runtime, configured `reasoning_efforts`, and applicable project constraints. A model absent from the registry is not eligible.
4. Among sufficiently capable, permitted candidates, favor the lower suitable resource/latency effort **without weakening correctness or required assurance**. Use real execution evidence to calibrate suitability. Do not automatically maximize effort.
5. For `allowed`, the authorized Coordinator may make **model-choice selection only** within the valid invocation and tool permissions. For `human_approval`, present **model ID + effort + concrete task/scope + reason** to the Human and wait for exact approval; neither mode bypasses this gate.
6. Before invocation, verify the effective model/effort using the harness's **native** controls and report what was observed. The Harscode YAML cannot select/provision Codex models, provide credentials or bypass runtime/sandbox security.
7. If no suitable, authorized or runnable pairing exists, mark the **affected invocation NOT READY**, state the smallest gap and ask the Human. No silent downgrade, unapproved upgrade, or substitute model.

**Independent review/verification is an execution-assurance boundary**, not automatically achieved by changing model IDs or effort. Two Specialist Agents sharing one model can still have materially independent context depending on actual verified execution setup; different IDs alone do not prove independence.

## Balad session versus Specialist invocation

Balad is **one logical Human-facing advisory role**. Its own session model is separate from Coordinator/Specialist runtime settings. The Human directly invokes the Coordinator (`supervised` unless the Human explicitly selects `autonomous`); actual model/effort binding and tool checks belong to that authorized execution context. Balad does not invoke, assign, request dispatch from or communicate with any Coordinator Agent. An `allowed` model entry does not override Human Approval Gates.

## Evidence and evolution

Treat the Human's local CLI catalog observations as scoped evidence of available effort names, not proof that a model succeeded during a session. For each consequential route, preserve only the evidence needed to know what was **selected, approved and actually used**. Do not claim a plausible registry as empirical capability validation.

Future multi-harness support (e.g., OpenCode with provider/model IDs and variants) remains a separate possible extension. Do not normalize unrelated harness variant semantics into Codex effort names without verifying the need and runtime behavior.
