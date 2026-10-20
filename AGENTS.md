# AGENTS.md — harscode-workspace

> **V-Next refactor branch only.** This inherited router points to legacy guidance pending migration. It is **not** proof that the proposed architecture is effective or ready for project execution. See [V-NEXT-ARCHITECTURE.md](V-NEXT-ARCHITECTURE.md) and [V-NEXT-CHECKLIST.md](V-NEXT-CHECKLIST.md). Use `main` for operational Harscode; do not invoke production work from this incomplete refactor branch.

This is the lightweight router and hard-rule surface. Do **not** load the full root `README.md` by default merely to route ordinary work; read the relevant section when workspace structure/governance rationale is actually needed.

## Where to go

- **Station 5 research Pairing:** when addressed as **Balad** (Lur/Dulur), or asked to assess a commitment, map end-to-end Space I/O or report a missing capability → `pairing/AGENTS.md`, then `pairing/space-formation.md` for composition/Formation Request. **Balad does not create Space definitions.**
- **Station 5 research Space candidate/definition:** inspect `spaces/README.md`, then the selected Space's `SPACE.md` and `AGENTS.md`. Candidate files are not evidence of approved formation or invocation.
- **Station 5 research Space Formation:** when Anhar + ChatGPT are designing/revising a reusable Space from a Formation Request → `space-formation/AGENTS.md`, then its scoped guidance. **Definition work and invocation are separately authorized.** Both routes are EXPERIMENTAL, not operational `main` policy.
- Turning project-owned product/domain truth into confirmed product behavior, traceable requirements, and a durable pre-engineering handoff → `pre-engineering/AGENTS.md`.
- Working in upstream product brand / UI/UX / design authority → `product-design/AGENTS.md`.
- Running or changing an engineering workflow phase → `workflow/AGENTS.md`, then the phase's canonical root `*-prompt.md` where one exists.
- Looking up engineering guidance → `best-practices/AGENTS.md`.
- Writing a proposal → `proposals/README.md`.
- Creating/editing Harscode guidance itself → `AUTHORING.md`.
- Harness-specific translation/configuration → `harness-optimization/AGENTS.md`.

## Hard rules that apply everywhere

- `pre-engineering/`, `product-design/`, `best-practices/`, `harness-optimization/`, and protected `workflow/2-techplan/` files are proposal-gated. Never change them on an ordinary project task without the applicable proposal/human authority.
- One proposal mechanism: root `proposals/`, one shared numbering sequence; use the applicable protection tier.
- Project-specific product/domain truth, brand decisions, design tokens, visual assets, and implementation facts belong in the target repo, not Harscode.
- Prefer targeted reads over broad folder scans. Load additional guidance when a concrete trigger requires it; do not read files merely because they are adjacent.
