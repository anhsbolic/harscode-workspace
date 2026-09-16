# harscode-workspace

A portable, local-only guidance system for moving product intent into reliable software with AI agents — not a prompt collection, not a framework, but a working manual built from real product and codebase experience.

## The problem

AI agents don't compound. Every session starts from limited context, no matter how many hours you spent teaching the last one. The common fix is throwing more prompts, more rules files, more "best practices" docs at the problem — but most of that content is either too abstract to act on, too tied to one project to reuse, or begins too late in the lifecycle after important product/design decisions have already been made implicitly.

`harscode-workspace` is an attempt to solve this differently: a project-agnostic system for carrying work from upstream product/design intent into engineering execution with explicit authority, human checkpoints, reusable technical guidance, and verification.

A useful shorthand is:

```text
product truth
→ product design
→ engineering exploration
→ techplan
→ build
→ review
→ testing
→ pull request
```

Not every task needs every upstream step. The point is to make the boundary explicit when product/design intent is still materially open, rather than letting implementation become accidental product authority.

## Philosophy: managing amnesiac contractors, not teammates

AI agents aren't growing team members. They don't compound skill over time, they fail confidently without internal signals telling them something's wrong, and they have no skin in the game. The right mental model is closer to **managing a fleet of amnesiac contractors** who can be handed an increasingly complete work manual.

That reframe drives every design decision here. The manageable variables aren't "how smart is the model" — they're things like:

- **Knowledge** — what the agent actually knows going in
- **Memory** — what persists across sessions (usually: nothing, unless you build it)
- **Scope** — what the agent is allowed to touch
- **Authority** — which artifact owns a decision, and which artifacts are only evidence/reference
- **Verification** — how you catch confident failures before they ship
- **Human checkpoint** — where a person has to sign off before the agent proceeds

`harscode-workspace` is the "work manual" side of that equation.

## Structure

```text
workspace/
├── AGENTS.md              # first thing an agent reads — hard rules + routing, no rationale
├── proposals/             # human-reviewed changes to protected/shared guidance
│   └── README.md
├── product-design/        # upstream product-brand/UI/UX and design-authority guidance
│   ├── AGENTS.md
│   ├── README.md
│   ├── kickoff-prompt.md
│   ├── discussion-facilitation.md
│   ├── product-brand-and-ui-exploration.md
│   ├── design-authority-and-canonicalization.md
│   └── design-to-engineering-handoff.md
├── workflow/              # engineering phases, in order of use
│   ├── AGENTS.md
│   ├── README.md
│   ├── exploration/
│   ├── techplan/
│   ├── build/
│   ├── code-review/
│   ├── testing/
│   └── pull-request/
└── best-practices/        # technology-organized reusable technical knowledge
    ├── AGENTS.md
    ├── index.md
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

**`product-design/`** encodes how product/domain truth becomes coherent, implementation-ready design authority. It covers product posture, brand + UI exploration, collaborative decision facilitation, visual proofs, canonicalization, and design-to-engineering handoff. It is intentionally **not** a mandatory per-feature workflow phase: use it when product-brand/UI intent is materially open, when a new design generation is being established, when legacy design authority conflicts, or when design readiness is unclear.

**`workflow/`** encodes *how* an engineering task should move through execution — exploration before planning, a formal proposal process for architectural decisions, lightweight checklists for lower-stakes phases like testing and PRs. Structural weight is proportional to stakes: `techplan/` has guardrails and a retro log; `code-review/` doesn't need that ceremony.

**`best-practices/`** encodes *what* an agent should know technically — organized by technology, not by project, so it's genuinely portable. Every entry here has had project-specific references stripped and replaced with neutral examples before it's allowed in.

**`index.md`** is load-bearing infrastructure for `best-practices/`, not a nice-to-have. Without it, an agent has to scan entire folders to find relevant guidance, which defeats the point. Every new best-practices file gets a row: trigger keywords → path → one-line summary. For security-relevant work specifically, `index.md` also carries a Security Concern Map — a cross-cutting grouping by concern (authn, authz, secrets, PII, etc.) so an agent doesn't have to guess which technology folder a security pattern lives in.

## Product-to-engineering boundary

Harscode deliberately separates four kinds of authority:

```text
product/domain truth
→ what the product means and what is factually/semantically true

product-design/
→ how that truth becomes coherent product-brand/UI/UX authority

workflow/
→ how engineering interprets, plans, builds, reviews, and verifies work

best-practices/
→ reusable technical knowledge applied while doing that work
```

This prevents several common failure modes:

- existing code becoming accidental product/design authority simply because it exists;
- prototypes or generated visuals being treated as business specifications;
- brand decisions being reopened during Build without material evidence;
- materially OPEN design decisions being silently invented inside JSX/CSS;
- technical implementation details being over-prescribed upstream as if they were product intent.

A healthy handoff is asymmetric:

> **Design hands off invariants and intent; engineering owns implementation mechanics.**

## Design principles

- **Product truth before implementation convenience.** Design and engineering may frame or represent product truth, but must not silently upgrade or invent it.
- **Single source of truth over phase-split content.** Cross-cutting knowledge lives in its owning area, not duplicated across every phase that touches it.
- **Agents execute; humans own durable guidance and material product/brand precedent.** Agents can explore, compare, recommend, implement, and propose changes. Human checkpoints remain explicit where authority matters.
- **Evidence and authority are different.** A prototype, screenshot, generated visual, old implementation, or prior design artifact may be useful evidence without being current authority.
- **Weight matches stakes.** Not every feature needs product-design work, and not every engineering phase needs full techplan formalism.
- **Calibrate before proliferating.** When establishing a new visual/product system, prove it on a representative slice before spreading it across the product.
- **Everything here is project-agnostic by construction.** If guidance cannot be stripped of project-specific context, it does not belong in this workspace yet.

## Governance

### Protection model, by area

| Area | Editable by agent? | Proposal mechanism |
|---|---|---|
| `product-design/` shared guidance | No — changes require human-reviewed proposal | `proposals/` (root), Protection Tier: `general` |
| `best-practices/` (all of it, including `index.md`) | No — not even append | `proposals/` (root), Protection Tier: `general` |
| `workflow/2-techplan/` protected files (`template.md`, `rules.md`, `guardrails.md`, `guidelines.md`, `diagram-guidelines.md`, `report-template.md`) | No | `proposals/` (root), Protection Tier: `techplan-protected` |
| `workflow/2-techplan/examples.md`, `workflow/2-techplan/retro.md` | Yes — append directly | N/A |
| `workflow/{1-exploration,3-build,4-code-review,5-testing,6-pull-request}/` | Corrected in the moment — no formal protection today | `proposals/` (root), Protection Tier: `general`, if that ever changes |

One proposal mechanism, one shared numbering sequence: `proposals/` at the workspace root. This used to be two separate mechanisms — a root `proposals/` and a narrower `workflow/2-techplan/proposals/` for techplan's own protected files — kept apart because a techplan is a contract a lead signs off on and changes more slowly than everything else. In practice, two independent numbering sequences that occasionally needed to cross-reference each other produced colliding numbers with no way to tell them apart. The fix was to consolidate into one folder and one sequence, keeping the tier distinction as a **Protection Tier field on each proposal** (`general` vs `techplan-protected`) instead of by folder location. `techplan-protected` keeps the higher bar (2+ tasks or genuinely structural); `general` keeps the lower one. See `proposals/README.md` for the full mechanics, template choice, and numbering rule.

### `AGENTS.md` vs `README.md`

Every area-level `README.md` (this file, `product-design/README.md`, `workflow/README.md`, `best-practices/index.md`) is the source of truth — read by humans and agents alike, holding the actual rationale, tables, and detail. `AGENTS.md` files are a separate, much thinner layer: the first thing an agent reads on entering a directory, containing only imperative hard rules and a pointer back to the relevant `README.md`/`index.md` for anything beyond that.

`AGENTS.md` is not allowed to accumulate explanatory content over time. If a rule needs justifying, the justification goes in the owning `README.md`, not inline in `AGENTS.md`.

## Product-design usage model

Product design is **upstream authority-building work**, not a rigid engineering stage machine.

Use `product-design/kickoff-prompt.md` when:

- product-brand/UI direction is still materially open;
- trust, persuasion, provenance, imagery, or visual-system strategy needs deliberate reasoning;
- multiple design generations conflict;
- a prototype or visual reference exists but its authority is unclear;
- the project needs to decide whether design is READY, PARTIAL, or OPEN before engineering proceeds.

The kickoff intentionally runs as a collaborative conversation rather than an interview checklist. `discussion-facilitation.md` defines the interaction model: ask the highest-leverage unresolved question, interpret the answer, challenge where consequences matter, recommend when enough evidence exists, keep human authority explicit, and periodically summarize decisions as `LOCKED`, `WORKING`, `OPEN`, or `REJECTED`.

A typical upstream design cycle is:

```text
product/domain truth
→ product posture + user/trust constraints
→ competing creative directions
→ human selection / synthesis
→ representative visual proofs
→ concrete visual-system decisions
→ canonicalization + legacy cleanup
→ design-to-engineering handoff
```

If the project already has sufficiently clear design authority, do not rerun this cycle just because the folder exists. Move into engineering exploration instead.

## How this differs from Spec Kit / Superpowers / Amazon Kiro

This project studied those tools but didn't adopt them wholesale. The short version: most existing systems optimize for either heavy spec formalism upfront (Spec Kit) or a general-purpose skill library (Superpowers, Kiro). Harscode is opinionated about a different boundary: preserve upstream product/design authority when needed, then move through exploration → techplan → execution with proportional structure and explicit human ownership of shared guidance.

`product-design/` does not turn Harscode into a design framework. It exists to prevent engineering from becoming the place where unresolved product-brand/UI decisions are accidentally made.

## Status

This is an active, evolving personal system — not a finished product. Structure gets revised based on real usage. New areas should earn their weight from real friction and reusable lessons, not from a desire to model every possible phase in advance.

## Usage

1. Copy this workspace's content into your project (or symlink it if you work across multiple repos) — the exact location is up to you; every prompt in `workflow/` refers to it as `{HARSCODE_WORKSPACE_ROOT}`, set once per project. See `workflow/README.md` § Path Variables Convention.
2. Point your agent's system prompt / project instructions at `{HARSCODE_WORKSPACE_ROOT}/AGENTS.md` as the entry point. It routes upstream product-design work to `product-design/`, engineering lifecycle work to `workflow/`, and technical knowledge lookup to `best-practices/`.
3. **If product/design authority is materially open**, start with `product-design/kickoff-prompt.md`. Use the product-design guidance until the relevant design intent is implementation-ready. If product/design authority is already sufficiently clear, skip this step — product-design is not mandatory per feature.
4. *(Optional — only if the project groups its work by domain; see `workflow/README.md` § Domain-Grouped Projects.)* Before the first feature in a new domain, run `workflow/0-domain-sequencing-prompt.md` once to produce that domain's `_domain-manifest.md`. Skip this for a domain's 2nd+ feature once the manifest already exists and nothing new has been added to scope.
5. Start an engineering task in `1-exploration/` before jumping to `2-techplan/`. Exploration should consume current product/design authority as input; it should not reopen approved upstream decisions without material evidence.
6. Techplan includes: synthesis → review → decomposition (optional).
7. Build against the techplan → write a build report.
8. Run code review against the build report → produce a review report and, if needed, a patch plan.
9. Execute that patch plan as part of the build loop — patches are always executed and reported in `3-build/`, regardless of which phase requested them.
10. Run testing against all build reports (initial build + every patch).
11. If testing says the code needs a patch, write a testing report and patch plan in `5-testing/`, then execute that patch in `3-build/`, producing a patch report there.
12. Create the pull request.
13. *(Optional — domain-grouped projects only.)* Once every feature in a domain has finished testing, run `workflow/7-domain-closure-prompt.md` before declaring the domain done. Its findings go back through the normal cycle.

### Task Working Directory Structure

*(Domain-grouped projects only — a project that doesn't group work by domain has no `{DOMAIN_PATH}`; each `{TASK_PATH}` stands on its own.)*

`{DOMAIN_PATH}` is the parent directory holding every feature's `{TASK_PATH}` within one domain. `_domain-manifest.md` (output of `workflow/0-domain-sequencing-prompt.md`) and `_domain-closure-review.md` (output of `workflow/7-domain-closure-prompt.md`) are the only files that live directly under `{DOMAIN_PATH}` rather than inside a specific feature's `{TASK_PATH}`.

Each engineering task gets one root working directory in the target repo — referred to as `{TASK_PATH}` throughout every prompt in `workflow/`. Its subfolders mirror `workflow/`'s phase numbering:

```text
{TASK_PATH}/
├── 1-exploration/
│   └── logs/                    # raw exploration output (gap analysis, sniffing findings, solutioning)
├── 2-techplan/
│   ├── techplan.md
│   └── tasks/                   # only if decomposition (2-3) was run — task files + manifest
├── 3-build/
│   ├── report.md                # initial build report
│   └── patch-report-<n>.md      # every patch execution report lands here, whoever asked for it
├── 4-code-review/
│   ├── review-findings-<n>.md
│   └── patch-plan-<n>.md        # the ask only — execution + report happens in 3-build/
├── 5-testing/
│   ├── testing-report-<n>.md
│   └── patch-plan-<n>.md        # same — cross-references the patch-report number in 3-build/
└── 6-pull-request/
    └── pr-description.md
```

The rule in one sentence: **patches are always executed and reported in `3-build/`**, no matter how many rounds or which phase requested them — patching is build activity by definition. `4-code-review/` and `5-testing/` only ever hold the *request* (a patch plan), cross-referenced to the patch report number that actually did the work.

## License

_(TBD — add your preferred license here, e.g. MIT)_