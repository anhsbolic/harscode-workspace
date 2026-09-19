# AGENTS.md — harscode-workspace

This is the lightweight router and hard-rule surface. Do **not** load the full root `README.md` by default merely to route ordinary work; read the relevant section when workspace structure/governance rationale is actually needed.

## Where to go

- Coordinating work as Work Units/Runs, routing decisions/blockers, or using a Harscode Space → `orchestration/AGENTS.md`.
- Working in upstream product brand / UI/UX / design authority → `product-design/AGENTS.md`.
- Running or changing an engineering workflow phase → `workflow/AGENTS.md`, then the phase's canonical root `*-prompt.md` where one exists.
- Looking up engineering guidance → `best-practices/AGENTS.md`.
- Writing a proposal → `proposals/README.md`.
- Creating/editing Harscode guidance itself → `AUTHORING.md`.
- Harness-specific translation/configuration → `harness-optimization/AGENTS.md`.

## Hard rules that apply everywhere

- `product-design/`, `best-practices/`, `harness-optimization/`, and protected `workflow/2-techplan/` files are proposal-gated. Never change them on an ordinary project task without the applicable proposal/human authority.
- One proposal mechanism: root `proposals/`, one shared numbering sequence; use the applicable protection tier.
- Project-specific product/domain truth, brand decisions, design tokens, visual assets, Work Unit state, Decisions, Control Surface state, Project Learning, and implementation facts belong in the target repo, not Harscode.
- Prefer targeted reads over broad folder scans. Load additional guidance when a concrete trigger requires it; do not read files merely because they are adjacent.
- Under Orchestrator Protocol v0.1, Work Unit/Run/Participant/Session identity and path semantics come from `orchestration/`; canonical workflow phase rules still come from `workflow/`.
