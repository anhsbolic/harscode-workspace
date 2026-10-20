# Claude Code — Model Routing (Standalone)

> **Derived view** — source of truth is `model-routing.md` (master, v3). Regenerate manually if the master changes.
> Scope: this file only uses models available in Claude Code. If you were restricted to this subscription alone, this is the full routing.
> Last generated: 2026-08-27.

## Confidence legend
✅ validated · ⚠️ benchmark-informed guess · ❓ vibes/naming guess only

## Models available here

Opus 4.8 · Sonnet 5 · Haiku 4.5

*(Fable 5 / Mythos 5 excluded — Mythos-tier / API access, not part of standard Claude Code coding flow.)*

With only three models spanning one capability ladder, most cells below follow the obvious mapping (Opus = Expert, Sonnet = Good, Haiku = Enough). The genuinely open questions are marked where they occur.

## What to pick

| Stage | Expert | Good | Enough |
|---|---|---|---|
| Exploration | ❓ Opus 4.8 | ❓ Sonnet 5 | ❓ Haiku 4.5 |
| Techplan synthesis | ❓ Opus 4.8 — *no second vendor available here; running Opus twice is not a real substitute for a cross-vendor adversarial pass* | ❓ Sonnet 5 | ❓ Haiku 4.5 |
| Decomposition | ❓ Opus 4.8 (only if Step 0 gate justifies it) | N/A — doesn't clear gate | N/A — doesn't clear gate |
| Backend build (Go) | ⚠️ Opus 4.8 — leads SWE-bench Multilingual (84.4%) among tracked models | ❓ Sonnet 5 | ❓ Haiku 4.5 — untested, candidate worth validating |
| Frontend build (React) | ⚠️ Opus 4.8 — tied for most wins in a 12-model build benchmark | ❓ Sonnet 5 | ❓ Haiku 4.5 |
| Code review | ❓ Opus 4.8 — *single-vendor only; this provider cannot satisfy the mandatory dual-model Safety-pass pattern on its own* | ✅ Sonnet 5 — the one cell with real standing in the master table, specifically when a review needs discussion of a trade-off rather than a checklist pass | ❓ Haiku 4.5 |
| Testing | ❓ Opus 4.8 | ❓ Sonnet 5 | ❓ Haiku 4.5 |
| Pull request writing | ❓ Sonnet 5 — mechanical precision work, Opus is likely overkill here | ❓ Sonnet 5 | ❓ Haiku 4.5 |

## Where this provider structurally can't match the master routing

- **Techplan synthesis / Code review, Expert**: the master routing mandates a dual-model adversarial pass from two differently-trained vendors. Claude Code alone can't do that — Opus 4.8 and Sonnet 5 likely share enough training lineage that running both isn't a genuine second opinion. Treat any Expert-tier techplan or review done entirely inside this provider as **not meeting the Expert bar**, regardless of which model you pick.

## Untested candidates worth a trial

- **Haiku 4.5** for Enough-tier coding (both Backend and Frontend) — the master table currently defers to DeepSeek V4 Flash by default; if Haiku is comparably clean at Claude Code's pricing, it's worth knowing for sessions where you don't want to leave this provider at all
- **Sonnet 5** for PR writing / testing — plausible it's already "enough" for these mechanical stages, meaning Opus is never actually needed here

## Open items specific to this provider

- [ ] Head-to-head: Haiku 4.5 vs a known-good Enough-tier model, on both Go and React
- [ ] First real comparative data point: Opus 4.8 on a Complex/Expert techplan synthesis, judged against a genuinely cross-vendor adversarial pass — to quantify how much is lost by staying single-provider at Expert tier