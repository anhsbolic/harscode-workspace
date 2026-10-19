# Balad Model Routing — Station 5 Research v0

> **Status:** Experimental guidance on `research/harscode-purpose-llm-fit`. Not Harscode operational `main` policy, native Codex configuration, an execution engine or an automatic authorization mechanism.
> **Authority:** Human owns `available_models` inventory and all model/effort policy. Balad reads the registry, assesses task fit, proposes routes and respects Human gates. See [Workspace Init](workspace-init.md), [Pairing Composition](space-formation.md) and [Human-led Space Formation](../space-formation/contract-and-readiness.md).

## Intent and scope

Select **a model + configured reasoning effort for each real Specialist Agent assignment**, not one immutable model per Space or one model per old workflow phase. Reusable Agent capability requirements differ from local invocation binding. A configured registry is **Human-declared policy**, not runtime proof of access, competence, pricing, outcome quality or session identity.

Station 5 initially targets one configured `codex-cli` harness. Do not introduce a multi-harness catalog, vendor adapters, automatic fallback, a runtime dispatcher or a model leaderboard before real requirements justify them.

## Human-owned model inventory

`<workspace-root>/.harscode-local.yaml` contains `available_models`. Only the Human decides which model IDs are offered, their task-suitability hints, relative cost preference and each permitted effort's approval state.

Balad:
- MAY read the registry, inspect runtime evidence **on request or when necessary to verify an impending route**, point out mismatches and **propose** a change.
- MUST NOT autonomously populate the registry during `workspace-init`, self-approve a model or effort, silently broaden availability, or alter the Human's policy to facilitate dispatch.
- MAY mechanically apply **exact Human-approved changes** after separate scoped write authorization; Human remains the authorizing owner. A Human can instead edit the local YAML directly.
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
- `id`: exact local runtime-recognized identifier. Confirm against the current Codex installation and user access when routing.
- `capabilities`: coarse Human-assessed suitability hints, **not proven benchmarks**. Examples: `reasoning`, `coding`, `repository-work`, `cross-cutting-analysis`. Avoid presenting `security-risk` as a guaranteed model capability; the assignment's risk and assurance duties are separate.
- `reasoning_efforts`: one mapping from **runtime-supported effort name** to the Human's **selection policy** for that *model+effort* pair:
  - `allowed`: Balad may select this pairing without an **additional model/effort-choice approval**. This is not permission to form/invoke a Space or bypass tool/path/project safeguards.
  - `human_approval`: before selecting or dispatching this pairing for a concrete invocation, Balad must obtain Human approval for that exact choice and scope. If the approval is absent or expired/outside scope, stop and ask. Approval must not silently carry over to unrelated work.
- **Absent effort**: not configured/eligible. Do not infer it from vendor documentation or earlier runtime observations. A key being present expresses Human-configured support and policy, but **actual** runtime support/access must still be checked when material.
- `cost_tier`: Human-selected relative resource preference (`low`, `standard`, `high`), not an exact bill, performance ranking or entitlement guarantee.

**No separate blanket `approval_required`, `supported_reasoning_efforts`, or `auto_select_efforts` in this schema.** Their old combinations are ambiguous and **not a recognized grant** under this candidate. Existing configs using old fields require explicit Human reconciliation before a model-dependent invocation; don't silently translate `approval_required: false` to universal `allowed`.

This policy is **fail-closed**: unknown status values, duplicate model entries, unsupported effort names, conflicting old and new fields, missing approval evidence, or runtime mismatch cause `NOT READY` for the affected pairing. Do not choose another model/effort silently to evade a gate.

## Selection, approval and runtime binding

1. **Determine the actual assignment** and accepted Space I/O contract first; no model routing merely because Balad is coordinating settled facts.
2. Identify material complexity, uncertainty, code/tool requirements, risk, independence/assurance duties and concrete Specialist capability needs. A larger effort does not inherently make a model safe for a security-critical task.
3. Read the Human-owned registry. Filter for sufficient task fit, supported local runtime, configured `reasoning_efforts`, and applicable project constraints. A model absent from the registry is not eligible.
4. Among sufficiently capable, permitted candidates, favor the lower suitable resource/latency effort **without weakening correctness or required assurance**. Use real execution evidence to calibrate suitability. Do not automatically maximize effort.
5. For `allowed`, proceed with **model-choice selection only** if the separate Space formation/invocation and tool permissions are valid. For `human_approval`, present **model ID + effort + concrete task/scope + reason** and wait for explicit Human authorization before initiating that exact pairing.
6. Before invocation, verify the effective model/effort using the harness's **native** controls and report what was observed. The Harscode YAML cannot select/provision Codex models, provide credentials or bypass runtime/sandbox security.
7. If no suitable, authorized or runnable pairing exists, mark the **affected invocation NOT READY**, state the smallest gap and ask the Human. No silent downgrade, unapproved upgrade, or substitute model.

**Independent review/verification is an execution-assurance boundary**, not automatically achieved by changing model IDs or effort. Two Specialist Agents sharing one model can still have materially independent context depending on actual verified execution setup; different IDs alone do not prove independence.

## Balad session versus Specialist invocation

Balad is **one logical Human-facing Pairing role**. The Human's Balad Codex session model can be chosen separately; do not invent default/escalation model fields. Specialist model/effort is decided at Space binding and checked again at invocation. The first C1 Space invocation remains separately Human-authorized even if its model+effort policy is `allowed`.

## Evidence and evolution

Treat the Human's local CLI catalog observations as scoped evidence of available effort names, not proof that a model succeeded during a session. For each consequential route, preserve only the evidence needed to know what was **selected, approved and actually used**. Do not claim a plausible registry as empirical capability validation.

Future multi-harness support (e.g., OpenCode with provider/model IDs and variants) remains a separate possible extension. Do not normalize unrelated harness variant semantics into Codex effort names without verifying the need and runtime behavior.
