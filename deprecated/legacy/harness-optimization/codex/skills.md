# skills.md (Codex)

## What this translates

Codex Skills provide progressive disclosure: small selection metadata is
available up front, the `SKILL.md` body is loaded when the skill is used, and
supporting references/scripts can be loaded only when needed.

A Codex Skill is an **adapter to an existing Harscode source**, not a place to
invent or rewrite policy.

## Two useful wrapper classes

### 1. Workflow wrappers

Prefer thin wrappers around canonical phase entrypoints, for example:

```text
harscode-explore  → Exploration
harscode-techplan → Techplan synthesis/review/decomposition gates
harscode-build    → Build/Patch
harscode-review   → Code Review
harscode-test     → Testing
harscode-pr       → Pull Request
```

These are example Skill names, not new Harscode phase names.

A project may also expose a convenience planning orchestrator such as
`harscode-plan`, but it must honor `workflow/context-management.md`: after
Exploration it follows the phase handoff's `CONTINUE`/`FRESH` recommendation.
It must not force Exploration + Techplan into one session or one context window.

A workflow wrapper should:

1. resolve the target repo's applicable `AGENTS.md` instructions;
2. resolve `{HARSCODE_WORKSPACE_ROOT}`;
3. read the current canonical Harscode phase prompt;
4. verify the prompt's inputs/preconditions;
5. load only the required/triggered authority that prompt routes to;
6. execute the phase and write artifacts only where Harscode/target-repo
   guidance owns them;
7. preserve phase handoff, human gates, and output completeness.

Do not paste a stale hand-edited copy of the phase prompt into the Skill. A
Skill that spans multiple phases must still respect fresh/independent boundaries
rather than treating Skill activation as permission to keep one giant context.

### 2. Best-practice discovery wrappers

`best-practices/index.md` provides routing signals for portable engineering
guidance. Codex Skills can translate that routing into automatic progressive
disclosure:

```text
best-practices index entry / trigger signal
→ skill name + description

underlying best-practice source
→ skill body/reference source
```

Do not invent trigger semantics or rewrite engineering rules while wrapping
them.

## Source strategies

Choose one strategy per generated Skill and make it explicit.

### Preferred when Harscode is reliably readable

Keep the Skill thin and read the current Harscode source at runtime:

```md
---
name: <skill-name>
description: <mechanically derived trigger/usage description>
---

Resolve `{HARSCODE_WORKSPACE_ROOT}`.
Read and follow:
`{HARSCODE_WORKSPACE_ROOT}/<authoritative-source>.md`

Also obey the target repo's applicable `AGENTS.md` files.
Do not reinterpret or restate the source rule here.
```

### Fallback when the external Harscode path is not reliably accessible

Generate an exact copy of the source into the project Skill, but treat it as a
**generated cache**, not a new authority. Record source path/revision and
regenerate when Harscode changes; do not hand-maintain both copies.

## Skill structure

Use supporting references/scripts only when they materially reduce repeated
work or keep conditional detail out of the entrypoint.

- `SKILL.md` should stay short and discriminating;
- `references/` are appropriate for multiple conditional Harscode sources;
- `scripts/` are for deterministic repeated transforms/checks, not policy.

## Placement

Actual Skill instances belong in the target repo's supported project-local
Codex skill surface or the user's Codex Skill installation, depending on scope.
Do not commit target-project instances into `harscode-workspace` itself.

## Keep the first installation small

Do not generate one Skill for every Harscode file merely because it is
possible. Start with wrappers that remove real lookup/friction, dogfood them,
and add more only when benefit outweighs metadata/synchronization cost.

Manual routing through `workflow/` and `best-practices/index.md` remains a
valid fallback.

## Verification checklist

- [ ] Skill points to an existing authoritative Harscode source.
- [ ] Description is derived from existing routing/phase intent, not new policy.
- [ ] Target-repo `AGENTS.md` authority is preserved.
- [ ] Project artifacts stay in Harscode/project-owned locations.
- [ ] Copied content is a generated cache with source revision metadata.
- [ ] Multi-phase wrappers honor Harscode phase handoff/session boundaries.
- [ ] Removing/failing to trigger the Skill falls back safely to manual
      Harscode lookup rather than changing correctness requirements.
