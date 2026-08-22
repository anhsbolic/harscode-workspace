# harscode-workspace

A portable, local-only guidance system that AI coding agents follow across projects — not a prompt collection, not a framework, but a working manual built from real codebase experience.

## The problem

AI coding agents don't compound. Every session starts from zero context, no matter how many hours you spent teaching the last one. The common fix is throwing more prompts, more rules files, more "best practices" docs at the problem — but most of that content is either too abstract to act on, or too tied to one project to reuse.

`harscode-workspace` is an attempt to solve this differently: a project-agnostic directory of workflow phases and technology-specific best practices, grounded in real examples, designed to be dropped into any repo and actually followed — not just referenced.

## Philosophy: managing amnesiac contractors, not teammates

AI agents aren't growing team members. They don't compound skill over time, they fail confidently without internal signals telling them something's wrong, and they have no skin in the game. The right mental model is closer to **managing a fleet of amnesiac contractors** who can be handed an increasingly complete work manual.

That reframe drives every design decision here. The manageable variables aren't "how smart is the model" — they're things like:

- **Knowledge** — what the agent actually knows going in
- **Memory** — what persists across sessions (usually: nothing, unless you build it)
- **Scope** — what the agent is allowed to touch
- **Verification** — how you catch confident failures before they ship
- **Human checkpoint** — where a person has to sign off before the agent proceeds

`harscode-workspace` is the "work manual" side of that equation.

## Structure

```
workspace/
├── AGENTS.md            # first thing an agent reads — hard rules + routing, no rationale
├── proposals/            # agent-writable proposals for best-practices/ (and, if ever needed, lightweight workflow/ phases)
│   └── README.md
├── workflow/            # development phases, in order of use
│   ├── AGENTS.md         # hard rules + routing for this folder
│   ├── README.md         # source of truth — phase tiering, rationale
│   ├── exploration/       # current-state gap analysis before any plan exists
│   ├── techplan/           # the most formal phase — guardrails, its own proposals/, retro log
│   ├── code-review/
│   ├── testing/
│   └── pull-request/
└── best-practices/      # technology-organized knowledge base
    ├── AGENTS.md          # hard rules + routing for this folder
    ├── index.md            # source of truth — scannable table: trigger keyword → file → summary, plus governance detail
    ├── go/
    ├── graphql/
    ├── postgresql/
    ├── restapi/
    ├── kafka/
    ├── pubsub/
    ├── redis/
    ├── infra/
    ├── pwa/
    └── ...
```

**`workflow/`** encodes *how* an agent should move through a piece of work — exploration before planning, a formal proposal process for architectural decisions, lightweight checklists for lower-stakes phases like testing and PRs. Structural weight is proportional to stakes: `techplan/` has guardrails and a retro log; `code-review/` doesn't need that ceremony.

**`best-practices/`** encodes *what* an agent should know — organized by technology, not by project, so it's genuinely portable. Every entry here has had project-specific references stripped and replaced with neutral examples before it's allowed in.

**`index.md`** is load-bearing infrastructure, not a nice-to-have. Without it, an agent has to scan entire folders to find relevant guidance, which defeats the point. Every new best-practices file gets a row: trigger keywords → path → one-line summary. For security-relevant work specifically, `index.md` also carries a Security Concern Map — a cross-cutting grouping by concern (authn, authz, secrets, PII, etc.) so an agent doesn't have to guess which technology folder a security pattern lives in.

## Design principles

- **Single source of truth over phase-split content.** Cross-cutting knowledge (e.g. Go error handling) lives in `best-practices/`, not duplicated across every workflow phase that touches Go.
- **Agents execute, humans own the guidance.** Agents can work within these files and write proposals for changes, but can't edit stable guidance directly. That boundary is deliberate.
- **Weight matches stakes.** Not every phase needs the full formalism of `techplan/`. Over-engineering lightweight phases was tried and explicitly rejected.
- **Everything here is project-agnostic by construction.** If a best-practice can't be stripped of project-specific context, it doesn't belong here yet.

## Governance

### Protection model, by area

| Area | Editable by agent? | Proposal mechanism |
|---|---|---|
| `best-practices/` (all of it, including `index.md`) | No — not even append | `proposals/` (root) |
| `workflow/techplan/` protected files (`template.md`, `rules.md`, `guardrails.md`, `guidelines.md`, `diagram-guidelines.md`) | No | `workflow/techplan/proposals/` (own, separate from root) |
| `workflow/techplan/examples.md`, `workflow/techplan/retro.md` | Yes — append directly | N/A |
| `workflow/{exploration,code-review,testing,pull-request}/` | Corrected in the moment — no formal protection today | `proposals/` (root) if that ever changes |

Two proposal mechanisms exist on purpose. `workflow/techplan/proposals/` predates the root `proposals/` and is scoped narrowly to techplan's own protected files, with a higher threshold (2+ stories or genuinely structural) because a techplan is a contract a lead signs off on. Root `proposals/` is lower-ceremony, for content that carries lower stakes — knowledge docs, not contracts. The two aren't consolidated; that's the "weight matches stakes" principle applied to governance itself, not just to workflow phases.

### `AGENTS.md` vs `README.md`

Every `README.md` (this file, `workflow/README.md`, `best-practices/index.md`) is the source of truth — read by humans and agents alike, holding the actual rationale, tables, and detail. `AGENTS.md` files are a separate, much thinner layer: the first thing an agent reads on entering a directory, containing only imperative hard rules and a pointer back to the relevant `README.md`/`index.md` for anything beyond that.

`AGENTS.md` is not allowed to accumulate explanatory content over time. If a rule needs justifying, the justification goes in `README.md`, not inline in `AGENTS.md`.

## How this differs from Spec Kit / Superpowers / Amazon Kiro

This project studied those tools but didn't adopt them wholesale. The short version: most existing systems optimize for either heavy spec formalism upfront (Spec Kit) or a general-purpose skill library (Superpowers, Kiro) — neither is built specifically around the exploration → techplan → execution loop with proportional structure per phase, or around a strict separation between agent-writable proposals and human-owned guardrails. `harscode-workspace` trades some generality for being opinionated about that loop.

## Status

This is an active, evolving personal system — not a finished product. Structure gets revised based on real usage (e.g. the `exploration/` phase was recently reworked after practical testing surfaced gaps in how agents were handling multi-area exploration). Expect churn.

## Usage

1. Copy `workspace/` into your project root (or symlink it if you work across multiple repos).
2. Point your agent's system prompt / project instructions at `workspace/AGENTS.md` as the entry point — it routes to `workflow/AGENTS.md` and `best-practices/AGENTS.md` as needed, which in turn point to the full `README.md`/`index.md` for anything beyond the hard rules.
3. Start a task in `exploration/` before jumping to `techplan/` — the workflow assumes you don't skip stages. execute exploration & techplan in one session is better.
4. techplan includes : synthesis -> review -> decomposition (optional)
5. build based on techplan -> write report
6. execute code-review based on build report -> create code review report and patch plan
7. execute patch plan as part of build iteration
8. execute testing based on all build report (build & patches)
9. do patch after testing, when it says "your code need patch" -> write testing report, patch plan, and patch report
10. create pull request

## License

_(TBD — add your preferred license here, e.g. MIT)_