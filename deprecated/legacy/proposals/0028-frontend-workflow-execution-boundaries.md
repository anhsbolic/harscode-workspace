# 0028 — Canonical phase prompts, execution profiles, Techplan convergence, and browser-automation boundary

**Status:** Accepted
**Date:** 2026-09-13 (proposed) · 2026-09-14 (revised and accepted)
**Protection Tier:** general
**Triggered by:** A real Codex frontend dogfood that completed Exploration + Techplan + independent review. The run surfaced both useful independent-review findings and avoidable process cost from re-authoring canonical prompts, ad-hoc model/client routing, recursive plan polishing, and treating a target project's browser automation as if it were a workflow gate.
**Target area:** workflow + harness-optimization + best-practices
**Target file(s):**
- `workflow/README.md` — new § Canonical Phase Prompts and § Phase Convergence
- `workflow/AGENTS.md` — one hard-rule bullet pointing at both sections *(added in revision)*
- `workflow/2-2-techplan-review-prompt.md` — materiality tag on Blocking findings + convergence/stopping rule; stays Draft
- `harness-optimization/codex/README.md` — canonical-prompt rule + § Execution profiles
- `harness-optimization/claude-code/frontend/slash-commands.md`, `harness-optimization/claude-code/backend/slash-commands.md` — commands route to root `*-prompt.md` *(added in revision)*
- `harness-optimization/claude-code/frontend/subagents.md`, `harness-optimization/claude-code/backend/subagents.md` — subagent bodies route to root `*-prompt.md` *(added in revision)*
- `best-practices/react/testing-automation-boundary.md` — verification vs browser-automation distinction

## Revision notes (2026-09-14)

This proposal arrived as a staged handoff package (`PROPOSAL.md`, `MANIFEST.md`, `full-files/`) prepared against baseline `5f3c9bc`. Before acceptance it was checked against the repository at that same baseline. The following revisions were made; everything not listed here is unchanged from the staged version.

**R1 — Claude Code translations added to the target list.** The staged version targeted only the Codex translation. The existing Claude Code translations already violated change A: `claude-code/{frontend,backend}/slash-commands.md` and `subagents.md` pointed commands and subagents at `workflow/<phase>/` folders and `guidelines.md` files, skipping the root `*-prompt.md` that carries each phase's inputs, response-style setting, and output format (only `/domain-sequence` already routed to its prompt). They did not inline content, so this was not duplication, but accepting A without fixing them would have left the workspace violating its own new rule on the day it landed.

**R2 — Ownership of "material" made explicit in change D.** The staged convergence rule said to re-review only when a resolution is material, but did not say who decides. Left implicit, the actor resolving findings — usually the same model or person that synthesized the plan — would grade its own fix. Revised split:
- the reviewer tags each Blocking finding with the material concern it touches, at review time;
- the resolver declares whether the resolution as a whole changed scope, architecture/ownership, business/security semantics, or verification strategy, regardless of how findings were tagged;
- the human gate makes the final re-review call.

A matching guard was added to the general convergence principle: deferral to Build covers mechanical detail only, and Build stops and reports if it hits a material decision the plan left open.

**R3 — Phases without a root prompt.** `6-pull-request/` has no root `*-prompt.md`. Change A is scoped to "where one exists"; such phases are invoked from their folder's guidance files.

**R4 — Change E aligned with `best-practices/react/visual-verification.md`.** That file already requires rendered verification for UI-affecting changes. The staged wording could be read as loosening that. Revised: rendered verification stays required per that file; the boundary introduced here is only about *committing and running a browser automation suite*, not about whether rendered verification happens.

**R5 — `workflow/AGENTS.md` bullet.** Per `workflow/README.md` § `AGENTS.md` vs this file, imperative rules go in `AGENTS.md` with rationale in `README.md`. One thin bullet was added.

**R6 — Known tension recorded, not resolved.** `best-practices/model-routing.md` contains named-model tables and "mandatory dual-model" rows, and `2-2-techplan-review-prompt.md` § Notes cites them. That sits uneasily with change C's principle that generic phase guidance stays model-neutral. This proposal deliberately does not edit `model-routing.md`; it remains the generic routing reference for its rows until its own separate revision lands. The execution-profile principle applies to phase prompts, harness translations, and target projects.

**R7 — Observed but out of scope.** `2-2-techplan-review-prompt.md`'s status banner still names a stale proposed location (`workflow/techplan-review-prompt.md`). Not fixed here.

## Gap found

The dogfood exposed five related ownership problems.

### 1. Canonical phase prompts can be bypassed by custom harness/project prompts

Harscode already has paste-ready phase entrypoints (`1-exploration-kickoff-prompt.md`, `2-1-techplan-synthesis-prompt.md`, `3-build-prompt.md`, `4-code-review-prompt.md`, `5-testing-prompt.md`). A custom prompt was nevertheless authored on top of the guidance during dogfood. It worked, but duplicated phase logic and made it easier to carry project/tool-specific mechanics into the wrong layer.

The workspace explained prompt shape and path variables, but did not state that the root `*-prompt.md` files are the default invocation surface — and its own Claude Code translation routed around them (R1).

### 2. Stack specialization and lifecycle specialization are easy to conflate

Frontend work genuinely needs different best-practice context, visual/rendered capability, design authority, and sometimes different model/client selection. None of that implies a different lifecycle. Without an explicit boundary, the natural response is frontend/backend copies of phase prompts, which duplicate workflow policy and drift.

### 3. Model/client/tool choice has no explicit layer separate from workflow policy

The dogfood moved between Codex models and clients based on perceived task difficulty. That decision is real, but it is not Harscode lifecycle policy.

```text
workflow phase     → what must be accomplished
execution profile  → model / reasoning effort / client / capabilities suitable for the work
```

### 4. Independent Techplan review lacks an explicit convergence boundary

The Draft review prompt produced meaningful signal: ambiguous error classification, missing project-state evidence, and browser-environment determinism that synthesis missed. After those were resolved, the loop continued into mechanical details — exact future command selectors, command-literal whitespace. The plan became the object being perfected rather than a sufficient contract for Build. The prompt defined what to review, not when a review-fix cycle has converged.

### 5. Browser automation can be mistaken for a phase obligation

A target repo had Playwright available, and exact Playwright execution mechanics began to be treated as part of Techplan approval before the feature's browser spec existed. A named browser-automation framework is tooling; Harscode should require evidence appropriate to the behavior and risk, and leave the choice to automate to target-project policy and human judgment.

## Proposed change (as implemented)

The target files are the source of truth for the exact text; this section records what each change establishes.

### A. Canonical phase prompts are the default invocation surface

`workflow/README.md` § Canonical Phase Prompts:
- where a phase has a root `*-prompt.md`, start from it — fill its variables, adapt only where it allows (R3);
- harness wrappers (slash commands, subagents, skills) route to or mechanically wrap it, never restate it;
- project/harness overlays add only narrow context or capability details the prompt doesn't already own;
- no per-project or per-stack copy of a phase prompt without a proposal establishing a real lifecycle difference.

Claude Code slash commands and subagents updated to route to the root prompts (R1). Codex README states the same rule; `codex/skills.md` already required it and needed no change.

### B. One lifecycle; specialize through layering

Same README section documents:

```text
Harscode phase prompt
+ matching best-practices/ files for the stack
+ target repo authority
+ harness/project execution profile
```

A track-specific harness folder remains justified only when the harness translation itself genuinely differs.

### C. Execution profiles, without model routing in phase prompts

`harness-optimization/codex/README.md` § Execution profiles: a target project or user may keep a Codex execution profile (model, reasoning effort, Desktop vs CLI, browser/rendered capability, image/design capability, other tool availability) in user Codex configuration or the target repo. It must not redefine lifecycle, project truth, approval authority, or testing obligations. No Codex model names are added to Harscode; no `codex/frontend/` folder for model or visual-tool preferences. See R6 for the `model-routing.md` tension.

### D. Techplan convergence/stopping rule (prompt stays Draft)

`workflow/README.md` § Phase Convergence states the general principle: a phase artifact is sufficient when the next phase can proceed without inventing a material decision; stop polishing after that; the next phase stops and reports if it hits one anyway.

`workflow/2-2-techplan-review-prompt.md`:
- only *material* findings are Blocking — Build would otherwise have to invent a product/domain decision, cross an authority/security boundary, choose a materially different architecture/state/ownership shape, or proceed without a meaningful verification strategy; or the defect changes meaning or makes the contract unusable;
- mechanical findings (wording, formatting, exact command spelling, local implementation shape) go under Non-blocking;
- each Blocking finding carries its material-concern tag;
- default shape: synthesis → one review (only when the Complex gate applies) → one resolution pass → human gate;
- resolver declares material change; re-review runs when yes unless the human gate waives it, and the human gate may order one even when the answer is no (R2).

The Draft status and 2+ real Complex-tier formalization threshold are unchanged.

### E. Rendered verification vs browser automation

`best-practices/react/testing-automation-boundary.md`: evidence requirements come from the property, its risk, and target-repo authority — including rendered verification per `visual-verification.md` (R4). Committing and running a browser automation suite is a separate choice justified by repeatability, regression value, or risk, not by the change being frontend or by the workflow reaching a phase. Framework choice is a target-repo tooling decision. Decision table row and checklist updated to match.

## Explicit non-goals

This proposal does **not**:

- create a new frontend lifecycle or frontend versions of phase prompts;
- remove Harscode Testing;
- weaken objective verification requirements, including rendered verification per `visual-verification.md`;
- require all rendered verification to be manual;
- ban Playwright or another browser framework;
- add project-specific browser commands, paths, or model names to Harscode;
- replace or repair `best-practices/model-routing.md`;
- promote the Draft independent Techplan review prompt to a hard gate.

## Rationale

These changes preserve the workspace's single-source-of-truth discipline. A phase prompt owns phase mechanics once. Stack-specific correctness comes from `best-practices/`. Project truth comes from the target repo. Harness mechanics come from `harness-optimization/` or project/user execution profiles. A browser framework stays tooling rather than a hidden lifecycle phase.

The convergence rule applies the same principle temporally: once an artifact is sufficient for the next phase, further polishing of mechanical detail adds cost without proportional correctness signal.

All findings are about source ownership and lifecycle/tooling boundaries, not one React app — they apply to any harness, any stack, any planning artifact, and any UI-capable project. The intended outcome is **less ceremony with clearer ownership**, not a new layer of mandatory artifacts.

## Evidence posture

- one real Codex frontend dogfood completed Exploration + Techplan + independent review;
- independent review found genuine material issues missed by synthesis;
- the same run demonstrated recursive over-convergence after the material issues were resolved;
- Build, Code Review, Testing, and PR were intentionally not completed in that experiment.

Enough for the ownership/convergence corrections above at the `general` tier; not enough to formalize the Draft independent review mechanism beyond its existing evidence threshold. Revisit change D once the review prompt has run on 2+ real Complex-tier plans.

---

*Accepted 2026-09-14 with revisions R1–R7. Merged into the target files above; this proposal stays in place as the changelog entry.*
