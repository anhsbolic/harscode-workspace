# ChatGPT Plus — Model Routing (Standalone)

> **Derived view** — source of truth is `model-routing.md` (master, v3). Regenerate manually if the master changes.
> Scope: this file only uses models available on ChatGPT Plus. If you were restricted to this subscription alone, this is the full routing.
> Last generated: 2026-08-27.
>
> **Read this before trusting the table below:** only one cell in this entire
> file (Frontend build, Good) is backed by real evidence. Everything else is
> constructed from a naming-tier ladder (Luna/Sol/Terra > 5.5 > 5.4 > mini,
> "Fast" = cheaper/quicker same-tier, "Codex Spark" = coding-specialized) —
> genuinely just an educated guess, flagged ❓ throughout. Don't route
> anything Expert-stakes here until at least the coding-specialist guess is
> validated once.

## Confidence legend
✅ validated · ⚠️ benchmark-informed guess · ❓ vibes/naming guess only

## Models available here

GPT-5.6 Luna / Luna Fast · GPT-5.6 Sol / Sol Fast · GPT-5.6 Terra / Terra Fast · GPT-5.5 / Fast · GPT-5.4 mini / mini Fast · GPT-5.4 / Fast · GPT-5.3 Codex Spark

**Open item that shapes this whole file:** Luna, Sol, and Terra look like parallel capability lines released together, not a ranked ladder. Only Luna has been anywhere near a real test. Sol and Terra are placed below purely because they're unverified, not because they're known to be worse — that placement could easily be backwards.

## What to pick

| Stage | Expert | Good | Enough |
|---|---|---|---|
| Exploration | ❓ GPT-5.6 Luna — only line with any track record | ❓ GPT-5.5 | ❓ GPT-5.4 mini Fast |
| Techplan synthesis | ❓ GPT-5.6 Luna — *no second model in this provider for the adversarial pass; running Luna twice is not a real substitute for a cross-vendor second opinion* | ❓ GPT-5.5 | ❓ GPT-5.4 |
| Decomposition | ❓ GPT-5.6 Terra (only if Step 0 gate justifies it — genuinely a guess which of Luna/Sol/Terra handles long material best) | N/A — doesn't clear gate | N/A — doesn't clear gate |
| Backend build (Go) | ❓ GPT-5.6 Luna | ❓ GPT-5.3 Codex Spark — "Codex" naming is the strongest signal in this whole file, worth prioritizing for a real trial | ❓ GPT-5.4 mini Fast |
| Frontend build (React) | ⚠️ GPT-5.6 Luna — the one cell with real backing: "volume pick" in a 12-model build benchmark | ❓ GPT-5.6 Luna Fast — same family, cheaper | ❓ GPT-5.4 mini Fast |
| Code review | ❓ GPT-5.6 Luna — *single-model only; this provider cannot satisfy the mandatory dual-model Safety-pass pattern on its own* | ❓ GPT-5.5 | ❓ GPT-5.4 mini |
| Testing | ❓ GPT-5.3 Codex Spark — coding-specialized naming fits rule-ID/precision checking | ❓ GPT-5.4 | ❓ GPT-5.4 mini Fast |
| Pull request writing | ❓ GPT-5.4 — mechanical precision work, doesn't need flagship reasoning | ❓ GPT-5.4 mini | ❓ GPT-5.4 mini Fast |

## Where this provider structurally can't match the master routing

- **Techplan synthesis / Code review, Expert**: the master routing mandates a dual-model adversarial pass from two differently-trained vendors. ChatGPT Plus alone can't do that — running two GPT-5.6 variants is still one lab's blind spots twice. Treat any Expert-tier techplan or review done entirely inside this provider as **not meeting the Expert bar**, regardless of which model you pick.

## Untested candidates worth a trial (priority order)

1. **GPT-5.3 Codex Spark** on one real Go and one real React build task — highest-value unknown in this file
2. **Luna vs Sol vs Terra**, same prompt, same task — resolves the biggest structural guess in this table
3. **GPT-5.4 mini Fast** vs your Enough-tier default elsewhere — cheap to test, tells you if this provider is worth using for boilerplate at all

## Open items specific to this provider

- [ ] Characterize Luna vs Sol vs Terra — blocks 3 of 8 rows above from being anything but a guess
- [ ] Trial GPT-5.3 Codex Spark against a known-good coding model on Go and React separately
- [ ] Confirm whether "Fast" variants trade off quality for speed, or are simply cheaper with no quality loss