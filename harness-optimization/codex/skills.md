# skills.md (Codex)

## What this translates

Codex Skills provide progressive disclosure: small selection metadata is available up front, the `SKILL.md` body is loaded when the skill is used, and supporting references/scripts can be loaded only when needed.

That maps well to Harscode's existing goal of keeping portable detail on demand instead of stuffing it into every project instruction file.

A Codex Skill is therefore an **adapter to an existing Harscode source**, not a place to invent or rewrite policy.

## Two useful wrapper classes

### 1. Workflow/session wrappers

A project may expose thin skills aligned to the existing Harscode lifecycle/session boundaries, for example:

```text
harscode-plan
→ Exploration + Techplan

harscode-build
→ Build + Patch

harscode-review
→ Code Review

harscode-test
→ Testing

harscode-pr
→ Pull Request
```

These names are examples, not new Harscode phase names.

A wrapper should:

1. resolve the target repo's applicable `AGENTS.md` instructions;
2. resolve `{HARSCODE_WORKSPACE_ROOT}`;
3. read the current Harscode prompt/guidelines for that phase/session;
4. verify the inputs/preconditions the Harscode prompt requires;
5. execute the phase and write generated artifacts only where Harscode/target-repo guidance says they belong;
6. preserve Harscode's output completeness and self-check requirements.

Do not paste a stale hand-edited copy of the phase prompt into the skill and then let the two evolve independently.

### 2. Best-practice discovery wrappers

`best-practices/index.md` already provides the routing signal for portable engineering guidance.

Codex Skills can translate that routing into automatic progressive disclosure. Keep the transform mechanical:

```text
best-practices index entry / trigger signal
→ skill name + description

underlying best-practice source
→ skill body/reference source
```

Do not invent new trigger semantics or rewrite the engineering rule while wrapping it.

## Source strategies

Choose one strategy per generated skill and make it explicit.

### Preferred when Harscode is reliably readable from the target workspace

Keep the skill thin and read the current Harscode source at runtime.

This minimizes synchronization drift.

Conceptual shape:

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

Generate an exact copy of the source into the project skill, but treat it as a **generated cache**, not a new authority.

The generation process must record the source path/revision and regenerate when Harscode changes. Do not manually maintain both copies.

## Skill structure

Current Codex skills support a required `SKILL.md` plus optional resources such as scripts/references/assets.

Use extra files only when they materially reduce repeated work or keep conditional detail out of the skill entrypoint. Do not create structure for its own sake.

For Harscode wrappers:

- `SKILL.md` should stay short and discriminating;
- supporting `references/` are appropriate when the wrapper needs multiple Harscode sources conditionally;
- `scripts/` are appropriate only for deterministic repeated transforms/checks, not for encoding policy that belongs in Markdown sources.

## Placement

Actual skill instances belong in the target repo's supported project-local Codex skill surface (for example `.codex/skills/` where current Codex supports it) or the user's Codex skill installation, depending on desired scope.

Do not commit target-project skill instances into `harscode-workspace` itself. This directory documents the reusable transform.

## Keep the first installation small

Do not generate one skill for every Harscode file on day one just because it is possible.

Start with wrappers that remove real repeated lookup/friction in the target project. Dogfood them. Add more only when actual use shows the progressive-disclosure benefit outweighs the metadata/synchronization surface.

This is an optimization rule, not a new lifecycle requirement: manual routing through `workflow/` and `best-practices/index.md` remains a valid fallback.

## Verification checklist

For every generated Harscode-backed Codex skill:

- [ ] The skill points to an existing authoritative Harscode source.
- [ ] Its description is derived from existing routing/phase intent rather than new policy wording.
- [ ] It does not weaken target-repo `AGENTS.md` rules.
- [ ] It does not create project artifacts outside the locations Harscode/project guidance owns.
- [ ] If content was copied, the copy is marked/generated as a cache with source revision metadata.
- [ ] Removing/failing to trigger the skill falls back safely to manual Harscode lookup rather than changing correctness requirements.
