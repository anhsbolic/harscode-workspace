# Model Routing (Draft)

> Status: DRAFT — personal reference, not yet workspace guidance. Proposed location if formalized: `best-practices/model-routing.md` (domain knowledge — "what model fits which job" — not process knowledge, so it belongs in `best-practices/`, not `workflow/`).
> Last reviewed: 2026-08-18. Model landscape moves fast — re-check pricing/benchmarks before trusting this beyond a few weeks old.

## Why this exists

Not every stage in the workflow needs the same model. Techplan synthesis at Complex tier and a one-line PR description have wildly different stakes, and routing both to the most expensive model wastes cost while routing both to the cheapest risks the exact kind of gaps `techplan/retro.md` already documents (R18 dropping, severity leaking, inverted diagram conditions). This routes by **tier × stage**, not by "always use the best available model."

## Tier definitions

Reused across every stage below — one definition, not redefined per row.

| Tier | Trigger |
|---|---|
| **Simple** | `template.md` §4 rules < 5, single service/area, no diagram, no breaking-change trigger |
| **Medium** | §4 rules 5–15, one diagram, 1–2 Open Items, nontrivial branching logic |
| **Complex** | §4 rules ≥ 15, cross-service, breaking-change trigger, or touches auth/payment/PII/Kafka-pubsub contract |

## Routing table

| Stage | Simple | Medium | Complex |
|---|---|---|---|
| **Exploration** | DeepSeek V4 Flash — interactive, small material | DeepSeek V4 Flash — still sufficient | MiMo V2.5 Pro — large/multi-area material, needs >200k effective token retention |
| **Techplan (synthesis)** | DeepSeek V4 Flash / GLM 5.2 (default) | GLM 5.2 (max) / DeepSeek V4 Pro | **GLM 5.2 (max) primary + DeepSeek V4 Pro second-pass adversarial (mandatory)** — see `techplan-review-prompt.md` |
| **Decomposition (techplan → tasks)** | N/A — doesn't clear Step 0 gate | N/A | MiMo V2.5 Pro — only if Step 0 gate justifies it |
| **Coding / build** | DeepSeek V4 Flash | GLM 5.2 (max) / DeepSeek V4 Pro | Decomposed: GLM 5.2 (max) / DeepSeek V4 Pro per sub-task. Not decomposed: GLM 5.2 (max) + heavier manual code-review after |
| **Code review** | DeepSeek V4 Flash | GLM 5.2 (default) / DeepSeek V4 Pro | **GLM 5.2 (max) + DeepSeek V4 Pro parallel (mandatory), diff manually** — no exception at this tier |
| **Testing** | DeepSeek V4 Flash | DeepSeek V4 Flash | DeepSeek V4 Pro — rule-ID count-check needs more reliability than Flash once rule count ≥15 |
| **Pull request writing & documentation** | DeepSeek V4 Flash | DeepSeek V4 Flash | DeepSeek V4 Pro — precision on Changes/Demo sections matching actual diff, still mechanical (not GLM-tier reasoning) |

## When two options are listed — how to pick

- **GLM 5.2 vs DeepSeek V4 Pro (Medium tier, techplan/build/review)**: GLM when the work leans on diagrams, state-transitions, or multi-step reasoning. DeepSeek V4 Pro when it's rule-table-heavy/precision work without a diagram — DeepSeek ties Claude on SWE-bench Verified specifically, the benchmark closest to "resolve a real issue in a real codebase."
- **DeepSeek V4 Flash vs GLM 5.2 default (Simple techplan)**: Flash for pure mechanical template execution. GLM default when there's a small judgment call (e.g. which section needs more detail).
- **Sonnet 5 vs DeepSeek V4 Pro (Medium code review, if Claude is available)**: Sonnet when the review needs back-and-forth discussion of a trade-off. DeepSeek V4 Pro for a fast checklist-driven pass.

## Non-negotiable dual-model rows

Two rows in this table are **not** A/B choices — both models run, results get diffed manually:

1. **Techplan Complex — synthesis + adversarial second pass.** This is the formalized version of what accidentally happened across the driving story's three passes: a different model catches different gaps than a self-check list run by the same model that wrote the plan.
2. **Code review Complex — parallel Safety pass.** GLM 5.2 has demonstrated real signal on vulnerability-pattern detection (outperformed Claude Code on an IDOR benchmark); DeepSeek V4 Pro adds a second, differently-trained perspective. Given DeepSeek's known weakness on cybersecurity-specific evals, it is a *supplement* to GLM here, not a substitute — don't run DeepSeek alone at this tier.

## Claude fallback mapping

If Opus 5 / Sonnet 5 are unavailable (access, cost, or otherwise):

| Row that used Claude | Fallback | Compensating control |
|---|---|---|
| Techplan Complex (primary) | GLM 5.2 (max) | Heavier manual review before Approved — GLM 5.2 has a documented reward-hacking tendency from training and less reliable instruction-following precision than Opus |
| Code review Complex (Safety) | GLM 5.2 (max) + DeepSeek V4 Pro parallel | Manual spot-check on critical bug classes (auth/IDOR/injection) — don't fully trust the two-model pass unsupervised |
| Exploration (interactive) | DeepSeek V4 Flash | None needed — low-risk substitution |
| Code review Medium | DeepSeek V4 Pro | None needed — low-risk substitution |

## Caveats — read before trusting this table long-term

- **All benchmark figures cited when building this table are vendor-reported** unless otherwise noted. Independent evaluation (e.g. NIST CAISI's review of DeepSeek V4 Pro) has found gaps between vendor claims and independently-measured performance on at least one model in this table — treat every number here as a hypothesis to validate against real stories, not settled fact.
- **Tier thresholds (5, 15 rules; 200k token) are starting guesses**, not calibrated. Adjust after running this against a handful of real stories — same approach as every other guidance change in this workspace (gap found → logged → adjusted, not decided upfront).
- **Pricing moves fast.** DeepSeek's own pricing page warned of a rate change effective 2026-08-16; GLM's cheapest listed price dropped ~47% over the prior 90 days per one tracker. Re-check before assuming today's cost math still holds.
- **Don't apply this table to stages it wasn't designed for.** `testing/` and `pull-request/` were deliberately left flat (no tiering) — this table respects that; don't add tiering there without a real recurring reason, consistent with "weight matches stakes."

## Formalization threshold

Keep this as personal working notes until either:
- The same model-routing decision proves right or wrong across 2+ real stories, or
- A genuinely structural gap shows up (e.g. a tier boundary is consistently wrong)

At that point it's a normal proposal candidate for `best-practices/index.md`, following the same threshold `guidelines.md` already defines for everything else in this workspace.