# Model Routing (Draft v3 — Expert / Good / Enough)

> Status: DRAFT — personal reference, not yet workspace guidance. Proposed location if formalized: `best-practices/model-routing.md`.
> Last reviewed: 2026-08-27.
> Change from v2: dropped the "Tier trigger" framing (rule-count thresholds). Replaced with three subjective quality levels applied directly per stage. Provider/quota table demoted to a pure availability reference — it no longer drives the decision, it just tells you where a chosen model lives and how much runway it has.

## Why this shape

Two earlier framings didn't fit how you actually decide:
- v1's Tier triggers (rule-count thresholds) tried to be objective but required counting things nobody counts in practice.
- Provider-first structure (v2) made "which model" secondary to "which subscription" — backwards, since the model choice should come first and provider is just where you go get it.

v3 answers one question per stage: **"how good does this specific piece of work need to be?"** — not "how complex is it on paper."

## Confidence legend

- ✅ validated — backed by real usage in this workspace (the driving story) or a direct benchmark hit on your actual stack
- ⚠️ benchmark-informed guess — grounded in a real (if imperfect/aggregator-sourced) benchmark, not yet self-tested
- ❓ vibes — naming/positioning guess only, needs a real trial before trusting

Everything here is explicitly subjective per your own call — the legend just tracks *how* subjective each cell is, so future-you knows what to re-test first.

---

## Level definitions

| Level | What it means | Roughly replaces (v1) |
|---|---|---|
| **Expert** | Stakes are high enough that a wrong or mediocre output costs real rework — cross-service contracts, auth/payment/PII, anything a lead will approve, or output you can't easily eyeball-verify yourself. Worth the cost/latency/quota hit. | Complex |
| **Good** | Normal day-to-day work. Needs to be right, but you'll review it anyway and errors are cheap to catch. | Medium |
| **Enough** | Mechanical, template-shaped, or low-blast-radius. Optimize for speed/cost; a slightly worse model costs you seconds of review, not hours of rework. | Simple |

---

## Routing table — Stage × Level

| Stage | Expert | Good | Enough |
|---|---|---|---|
| **Exploration** | ⚠️ MiMo-V2.5 (OpenCode Go) — large multi-area material, needs high effective context retention | ✅ DeepSeek V4 Flash | ✅ DeepSeek V4 Flash |
| **Techplan synthesis** | ✅ **GLM 5.2 (max) + DeepSeek V4 Pro adversarial (mandatory dual-model)** | ✅ GLM 5.2 (max) or DeepSeek V4 Pro (single pass) | ✅ DeepSeek V4 Flash / GLM 5.2 default |
| **Decomposition** | ⚠️ MiMo V2.5 Pro — only if Step 0 gate justifies it | N/A — doesn't clear gate | N/A — doesn't clear gate |
| **Backend build (Go)** | ⚠️ Claude Opus 4.8 (Claude Code) — leads SWE-bench Multilingual (84.4%); GLM 5.2 (max) alt for long multi-file work | ⚠️ DeepSeek V4 Pro (OpenCode Go) — strong on algorithmic/rule-precise Go, cheap | ✅ DeepSeek V4 Flash |
| **Frontend build (React/Next.js)** | ❓ Kimi K3 (OpenCode Go) — rated cleanest code in a 12-model build benchmark, but 110 req/5hr means reserve for genuinely hard UI work only; Claude Opus 4.8 as the practical Expert default given Kimi's quota | ⚠️ GPT-5.6 Luna (ChatGPT Plus or OpenCode Go) — "volume pick" in the same benchmark, good balance of quality and quota (2,050/5hr on Go) | ✅ DeepSeek V4 Flash / GLM-5.3-Flash for boilerplate components |
| **Code review** | ✅ **GLM 5.2 (max) + DeepSeek V4 Pro parallel (mandatory Safety pass)** | ✅ GLM 5.2 (default) / DeepSeek V4 Pro, or Sonnet 5 if the review needs a trade-off discussion | ✅ DeepSeek V4 Flash |
| **Testing** | ✅ DeepSeek V4 Pro — rule-ID count-check needs more reliability than Flash | ✅ DeepSeek V4 Flash | ✅ DeepSeek V4 Flash |
| **Pull request writing** | ✅ DeepSeek V4 Pro — precision on Changes/Demo matching actual diff | ✅ DeepSeek V4 Flash | ✅ DeepSeek V4 Flash |

**Notes on the two ❓/⚠️-heavy rows (build):**
- Backend and frontend are split because the underlying evidence is genuinely different in shape: Go benchmarks are proxy-weak (most public leaderboards are Python-biased), while the frontend pick has one real built-and-judged benchmark behind it. Don't read the confidence markers as "frontend data is better" — just "differently uncertain."
- Kimi K3's Expert slot is a genuine tension: best output quality found so far, worst quota. Treat it as a scalpel (one hard component, one tricky animation), not a daily driver — burning 20 of your 110 requests on routine work leaves nothing for the day you actually need it.

---

## Non-negotiable dual-model rows (unchanged from v2)

Two cells above are **not** A/B choices — both models run, results get diffed manually:

1. **Techplan synthesis, Expert** — GLM 5.2 (max) + DeepSeek V4 Pro adversarial second pass.
2. **Code review, Expert** — GLM 5.2 (max) + DeepSeek V4 Pro parallel Safety pass. DeepSeek is a *supplement* here (weaker on cybersecurity-specific evals), not a substitute — don't run it alone at this level.

## Claude fallback mapping

If Claude Code models are unavailable:

| Cell that used Claude | Fallback | Compensating control |
|---|---|---|
| Backend build, Expert | GLM 5.2 (max) | Heavier manual review — GLM has a documented reward-hacking tendency and less reliable instruction-following than Opus |
| Frontend build, Expert (Opus fallback) | GPT-5.6 Luna, or spend Kimi K3 quota | Manual visual/UX check — neither fallback has Opus's cross-task consistency in the source benchmark |
| Code review Good (Sonnet option) | DeepSeek V4 Pro | None needed — low-risk substitution |

---

## Provider Availability (reference only — does not drive decisions)

> Use this table AFTER picking a model from the routing table above, to find
> where to actually run it and how much runway you have. If your first-choice
> model's quota is currently exhausted, come back here for the next-best
> option in the same routing cell — don't just grab whatever's available.

### OpenCode Go — quota = requests / 5hr window

| Model | Quota/5hr | Appears in routing table as |
|---|---|---|
| Kimi K3 | 110 | Frontend build, Expert |
| Qwen3.8 Max | 160 | — (not currently routed; unused capacity) |
| Grok 4.6 | 169 | — (not currently routed) |
| GPT-5.6 Luna | 2,050 | Frontend build, Good |
| GLM-5.3-Flash | 3,160 | Frontend build, Enough |
| MiniMax M3 | 3,200 | — (not currently routed) |
| Qwen3.7 Plus | 4,300 | — (not currently routed) |
| DeepSeek V4 Flash | 7,600 | Exploration/Testing/PR, Enough; Backend build, Enough |
| LongCat-2.0 | 11,400 | — (not currently routed) |
| MiMo-V2.5 | 30,100 | Exploration, Expert |
| Hy3 | 34,400 | — (not currently routed) |
| Muse Spark 1.2 Contributor | 45,300 | — (limited regions, not currently routed) |

**Open items (quota not in source chart):**
- [ ] GLM 5.2 (non-Flash) quota/5hr — used in the two mandatory dual-model rows, worth knowing the ceiling
- [ ] DeepSeek V4 Pro quota/5hr — used across Good/Expert cells, same concern
- [ ] MiMo V2.5 Pro quota/5hr — confirm if distinct SKU from MiMo-V2.5 above

### Claude Code

| Model | Appears in routing table as |
|---|---|
| Opus 4.8 | Backend build, Expert; Frontend build, Expert (fallback) |
| Sonnet 5 | Code review, Good (optional) |
| Haiku 4.5 | Not currently routed — candidate for a Simple/Enough coding slot, untested against DeepSeek V4 Flash |

### ChatGPT Plus

| Model | Appears in routing table as |
|---|---|
| GPT-5.6 Luna / Luna Fast | Frontend build, Good |
| GPT-5.6 Sol / Sol Fast | Not currently routed — ❓ open item, unclear how it differs from Luna |
| GPT-5.6 Terra / Terra Fast | Not currently routed — ❓ open item |
| GPT-5.5 / Fast | Not currently routed |
| GPT-5.4 mini / mini Fast | Candidate for Enough-tier coding, untested |
| GPT-5.3 Codex Spark | Candidate for Backend/Frontend build Good, untested — "Codex" naming suggests coding specialization |

---

## Open Items (consolidated, carried from v2 + new)

- [ ] GLM 5.2 / DeepSeek V4 Pro / MiMo V2.5 Pro quota-per-5hr on OpenCode Go
- [ ] Characterize GPT-5.6 Luna vs Sol vs Terra — currently only Luna is placed in the routing table
- [ ] Head-to-head: Haiku 4.5 vs DeepSeek V4 Flash vs GPT-5.4 mini Fast for Enough-tier coding
- [ ] Trial GPT-5.3 Codex Spark on a real Good-tier build task (Go and React separately — don't assume it transfers)
- [ ] First real comparative data point: Opus 4.8 vs GLM 5.2 (max) on a Complex/Expert techplan synthesis, side-by-side
- [ ] Validate Kimi K3's Expert-frontend placement against Opus 4.8 on one real hard component from Kencleng

## Caveats

- Every ⚠️/❓ cell traces back to aggregator blogs or vendor-published numbers, not independent verification or your own testing. Treat this whole table as a starting point to challenge, not a settled ranking.
- Go-language benchmarks in general are proxy-weak — most public leaderboards skew Python. The Backend build row leans more on general SWE-bench Multilingual/Pro standing than a Go-specific, independently-run benchmark.
- The frontend build row rests on one 144-build benchmark study — a real signal, but a single source. Don't treat it as consensus.
- Pricing and quota move fast; re-verify before trusting this beyond a few weeks.

## Formalization threshold

Keep this as personal working notes until either:
- The same routing decision proves right or wrong across 2+ real stories/tasks, or
- You run your own Go/React mini-benchmark (planned, not yet started) and can replace ⚠️/❓ cells with ✅

At that point it's a normal proposal candidate for `best-practices/index.md`, same threshold as everything else in this workspace.