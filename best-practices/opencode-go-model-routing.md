# OpenCode Go — Model Routing (Standalone)

> **Derived view** — source of truth is `model-routing.md` (master, v3). Regenerate manually if the master changes.
> Scope: this file only uses models available on OpenCode Go. If you were restricted to this subscription alone, this is the full routing.
> Last generated: 2026-08-27.

## Confidence legend
✅ validated · ⚠️ benchmark-informed guess · ❓ vibes/naming guess only

## Models available here & quota (requests / 5hr window)

| Model | Quota/5hr |
|---|---|
| Kimi K3 | 110 |
| Qwen3.8 Max | 160 |
| Grok 4.6 | 169 |
| GPT-5.6 Luna | 2,050 |
| GLM-5.3-Flash | 3,160 |
| MiniMax M3 | 3,200 |
| Qwen3.7 Plus | 4,300 |
| DeepSeek V4 Flash | 7,600 |
| LongCat-2.0 | 11,400 |
| MiMo-V2.5 | 30,100 |
| Hy3 | 34,400 |
| Muse Spark 1.2 Contributor | 45,300 (limited regions) |
| GLM 5.2 (max/default) | ❓ open item |
| DeepSeek V4 Pro | ❓ open item |
| MiMo V2.5 Pro | ❓ open item |

## What to pick

| Stage | Expert | Good | Enough |
|---|---|---|---|
| Exploration | ✅ MiMo-V2.5 — large multi-area material, high effective context retention | ✅ DeepSeek V4 Flash | ✅ DeepSeek V4 Flash |
| Techplan synthesis | ✅ **GLM 5.2 (max) + DeepSeek V4 Pro — run both, diff manually** | ✅ GLM 5.2 (max) or DeepSeek V4 Pro | ✅ DeepSeek V4 Flash / GLM 5.2 default |
| Decomposition | ⚠️ MiMo V2.5 Pro (only if Step 0 gate justifies it) | N/A — doesn't clear gate | N/A — doesn't clear gate |
| Backend build (Go) | ⚠️ GLM 5.2 (max) — leads long-horizon, multi-file agentic coding benchmarks | ⚠️ DeepSeek V4 Pro — strong on algorithmic/rule-precise Go, cheap | ✅ DeepSeek V4 Flash |
| Frontend build (React) | ❓ Kimi K3 — rated cleanest code in a 12-model build benchmark; 110/5hr means spend it only on genuinely hard components | ⚠️ GPT-5.6 Luna — "volume pick" in the same benchmark, good quality-to-quota balance | ✅ DeepSeek V4 Flash / GLM-5.3-Flash for boilerplate |
| Code review | ✅ **GLM 5.2 (max) + DeepSeek V4 Pro — run both, diff manually** | ✅ GLM 5.2 (default) or DeepSeek V4 Pro | ✅ DeepSeek V4 Flash |
| Testing | ✅ DeepSeek V4 Pro — rule-ID count-check needs more reliability than Flash | ✅ DeepSeek V4 Flash | ✅ DeepSeek V4 Flash |
| Pull request writing | ✅ DeepSeek V4 Pro — precision on Changes/Demo matching actual diff | ✅ DeepSeek V4 Flash | ✅ DeepSeek V4 Flash |

## If your first pick is quota-exhausted (within this provider only)

| If this is out of quota... | ...try this instead |
|---|---|
| Kimi K3 (Frontend Expert) | Qwen3.8 Max or Grok 4.6 — untested, but next-highest naming-tier candidates with their own (tight) quota |
| MiMo-V2.5 (Exploration Expert) | LongCat-2.0 |
| DeepSeek V4 Flash (any Enough cell) | GLM-5.3-Flash or LongCat-2.0 |

## Unused capacity — subscribed but not routed anywhere

Qwen3.8 Max, Grok 4.6, MiniMax M3, Qwen3.7 Plus, LongCat-2.0, Hy3, Muse Spark 1.2 Contributor. Not a bug — no stage has justified a slot for them yet. First candidates to test during the eventual self-benchmark.

## Open items specific to this provider

- [ ] Real quota/5hr for GLM 5.2 (non-Flash), DeepSeek V4 Pro, MiMo V2.5 Pro — these carry the most-used cells above and aren't in the source usage chart
- [ ] Confirm "2x usage" (GLM-5.3-Flash) / "8x usage" (Hy3) quota-multiplier semantics
- [ ] Whether MiMo V2.5 Pro is a distinct SKU from MiMo-V2.5, or the same model at a different access tier