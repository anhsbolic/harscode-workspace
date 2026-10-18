# Balad Model Routing — Station 5 Research v0

> **Status:** Experimental guidance for Balad and formed Spaces on `research/harscode-purpose-llm-fit`. Not operational `main` policy, a Codex-native model config, or an automatic execution/approval mechanism.
> **Authority:** Human owns usable model policy; Balad recommends bounded choices and respects gating. See [Workspace Init](workspace-init.md), [Space Formation](space-formation.md), and relevant Codex guidance in `../harness-optimization/codex/`.

## Why a local registry

Model selection should be **per concrete Specialist Agent assignment / invocation need**, not one permanent model per Space or a hardcoded model assigned to old workflow stages. One Space may contain a solution specialist, builder and independent reviewer with materially different requirements. A *reusable Agent Profile* describes capability demand, while *local runtime binding* resolves available model and reasoning effort for the task.

The local registry is a Human-approved **policy and discoverability surface**, not proof of current availability, skill, price, latency, guaranteed performance or permission. Do not construct a model catalog service or keep duplicate registries.

## Registry ownership and proposed shape

Add entries to `<workspace-root>/.harscode-local.yaml` only after the Human confirms applicable locally offered models. All examples below are **illustrative placeholders**, **not claims of available real models**:

```yaml
available_models:
  - id: example-standard-model
    capabilities: [reasoning, coding, repository-work]
    supported_reasoning_efforts: [low, medium, high]
    cost_tier: standard
    approval_required: false

  - id: example-advanced-model
    capabilities: [reasoning, architecture, cross-cutting-analysis, coding]
    supported_reasoning_efforts: [medium, high]
    cost_tier: high
    approval_required: true
```

Minimum fields:
- `id`: exact identifier that the chosen local runtime actually understands; verify against Codex/session/provider access, not merely online model catalogs.
- `capabilities`: coarse **Human-assessed** suitability tags, not benchmark truth; refine from observed task evidence.
- `supported_reasoning_efforts`: actual runtime-supported selectable values. They are model and harness dependent; check live.
- `cost_tier`: **Human-declared relative resource/latency/usage preference**, e.g. low/standard/high; not an invented exact API price or guarantee.
- `approval_required`: Human-defined model-use gate, separate from project/Space permissions and protected work approvals.

**Ownership:** Balad may discover available models, compare vendor/runtime documentation, spot stale metadata and **propose** a registry update. It must not quietly add/remove models, elevate capabilities, change cost tier or approval requirements, or mark an unverified model as verified. Human approval of a change precedes applying it. Avoid treating a previous pilot's real-looking model identifiers, cost labels or reasoning values as current inventory.

Registry may remain empty during read-only formation assessment; if no usable authorized model is configured, Balad may recommend capabilities and list the gap but **cannot claim a model-routed Space ready for invocation**.

## Model selection algorithm (reasoning guidance, not automation)

1. **Identify actual assignment:** first determine whether a Space/Agent needs execution at all. Do not select a model before the task, accepted I/O contract, Agent capability demands and assurance boundary are understood.
2. **Assess sufficient capability:** consider reasoning complexity, uncertainty, repo breadth, product/technical risk, code/test/tool needs, independence obligations, context pressure and empirically known strengths/weaknesses. A stronger model cannot correct missing authority, an absent tool or compromised review independence.
3. **Filter by authorized inventory:** eligible models must be Human-approved, capable enough **for this task**, actually accessible to the selected Codex runtime, and compatible with required tools, reasoning effort, and approval constraints. Model declaration alone is not executable proof.
4. **Choose fit-for-purpose:** among sufficiently safe candidates, prefer lower practical cost/latency/usage, without sacrificing correctness or material safeguards. Choose a sufficient supported reasoning effort, not automatically maximum. Harder design/review may justify a different model from routine implementation even inside one Space.
5. **Explain a consequential route:** for an actual invocation, state Specialist Agent/assignment, model, effort, basis for sufficiency, significant uncertainty and approvals; keep the rationale short when obvious.
6. **Fail closed on a material gap:** if no approved suitable model is available or runtime support is unverified, mark routing **NOT READY**, propose the minimum registry/evidence/permission change, and ask the Human. Do not silently downgrade, upgrade to a gated model, or invent a fallback.
7. **At invocation, verify effective binding:** resolve the actual selected model/effort with native Codex controls and check the observed session config where possible. A recommendation in YAML or Markdown is **not** a runtime switch. Record what was actually used with task output evidence when material.

## Balad model versus Specialist model

Balad operates as **one logical external Pairing role**. Its current Codex session model may be operator-selected independently. Do not introduce mandatory `balad.default_model` or `escalation_model` fields before a concrete usage problem justifies them; keep the v0 config small. If Balad lacks reasoning capability for a consequential judgment, it should report the limitation and recommend Human-led session/model selection rather than claiming it can secretly upgrade itself.

Specialist model choice occurs at **Space binding/invocation**, not by global permanent assignment. Balad may recommend it during formation; the Space uses it only once formed, input-ready and invocation-authorized. For a multi-Agent Space, select per Specialist when runtime supports it; if a shared-model limitation exists, disclose that limitation and adjust the design/assurance honestly. Do not claim independent assurance solely because two Agents have distinct model IDs.

## Evaluation and calibration

Maintain the smallest useful evidence of suitability: actual C1 task quality, rejected/accepted errors, verified outcomes, unexpected cost/latency, runtime failures and Human assessment. Avoid a speculative benchmark/rating system or synthetic model leaderboard before meaningful real comparisons. Changing the registry does not change project product authority or retrospectively upgrade a failed run to PASS.

## Runtime boundary

Codex supports model selection and model-dependent reasoning controls through its own CLI/config/session mechanisms. **`.harscode-local.yaml` is a Harscode metadata file, not Codex's native `config.toml`.** No shell command or specific model ID should be assumed without verifying the operator's installed CLI and current runtime support. The local model registry cannot grant network/filesystem permissions, bypass Human approval, or provision a model absent from the user's access.
