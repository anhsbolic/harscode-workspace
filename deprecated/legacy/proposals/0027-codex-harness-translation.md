# 0027 — Codex root translation: instruction hierarchy, skills, session isolation, sandbox/approvals, and token optimization

**Status:** Accepted
**Date:** 2026-09-13
**Protection Tier:** general
**Triggered by:** Preparing the first Codex frontend dogfood after a target project had already exercised compact hierarchical `AGENTS.md`, shared-component blast-radius governance, and real-browser verification. The remaining gap was not missing workflow policy; it was the absence of a Codex-native translation layer equivalent to the existing Claude Code harness translation.
**Target area:** harness-optimization
**Target file(s):**
- New: `harness-optimization/codex/README.md`
- New: `harness-optimization/codex/instruction-loading.md`
- New: `harness-optimization/codex/skills.md`
- New: `harness-optimization/codex/session-boundaries.md`
- New: `harness-optimization/codex/permissions-and-sandbox.md`
- New: `harness-optimization/codex/token-optimization.md`

## Gap found

`harness-optimization/` already defines the correct boundary — translation only, never policy — and already contains a Claude Code implementation. Codex currently has no sibling translation.

That absence creates five predictable failure modes:

1. **Instruction duplication.** Codex natively consumes hierarchical `AGENTS.md` files. Without explicit guidance, a project may add a second large Codex-specific instruction document or paste Harscode workflow prose into project `AGENTS.md`, creating another source of truth.
2. **No progressive-disclosure mapping.** Codex Skills can expose small selection metadata and load their full body/resources only when used. Harscode has no guidance for using that mechanism without copying/re-authoring policy.
3. **Phase isolation can drift into harness-specific lifecycle policy.** Harscode already defines a four-session default. Codex now has fast-moving native multi-agent/subagent capability, but there is no guidance saying that native agents are an optional isolation optimization rather than a new workflow requirement.
4. **Sandbox and approval controls have no Harscode boundary.** Codex can constrain writes, network access, and approvals. Those controls can reinforce existing project/Harscode authority, but they can also accidentally invent or weaken policy if treated as the source of risk decisions.
5. **The harness-agnostic token rule has no Codex enforcement pattern.** Claude Code has a concrete translation; Codex does not.

## Proposed change

Add a project-agnostic `harness-optimization/codex/` sibling with six files.

### `README.md`

Carry the mandatory effective-as-of / last-verified / re-verify disclaimer, restate the translation-only boundary, and index the Codex-specific files.

The README explicitly says not to create a giant `CODEX.md` by default. Codex's native hierarchical `AGENTS.md` mechanism should remain the normal project instruction carrier.

### `instruction-loading.md`

Translate Codex instruction loading into Harscode's existing source-of-truth model:

- project root/nested `AGENTS.md` = project hard rules, commands, fencing, and routing;
- Harscode workflow/best-practices = on-demand portable guidance;
- `AGENTS.override.md` = explicit override, not the normal baseline;
- `project_doc_fallback_filenames` = compatibility bridge, not a reason to create another canonical project instruction file;
- keep always-loaded instruction content small and move rationale/details to the source that owns them.

As verified in current Codex documentation, project instructions are aggregated from the project root toward the current working directory, with more-specific instructions appearing later, and the project-document loading path has a bounded default budget.

### `skills.md`

Use Codex Skills as progressive-disclosure adapters rather than new policy sources.

A generated project skill should be mechanically derived from an existing Harscode source and should either:

- route to/read that source at runtime; or
- carry an exact generated copy that is explicitly treated as a cache and regenerated when the source changes.

Do not hand-rewrite workflow/best-practice content inside a skill.

The initial recommendation is to start with wrappers aligned to Harscode's existing session/phase boundaries and high-value best-practice discovery, then expand only after dogfood proves additional wrappers useful. Actual `.codex/skills/` instances belong in the target repo or user's Codex setup, not in this workspace.

### `session-boundaries.md`

Map Harscode's existing portable default directly:

```text
Exploration + Techplan
Build + Patch
Code Review
Testing
```

PR generation follows verified output afterward.

Codex native subagents/multi-agent tools may implement some of those isolation boundaries when current mechanics are verified and useful. They are an optional translation detail, not a requirement for Harscode correctness. A fresh/re-grounded Codex session remains the portable fallback.

### `permissions-and-sandbox.md`

Translate existing authority into Codex environment controls:

- planning/review work can use read-only access where practical;
- build/patch needs narrow workspace write access;
- testing gets only the capabilities needed for objective verification;
- protected/high-risk writes still follow the target repo/Harscode human-authority rule;
- network/tool access should be explicit and scoped;
- automatic approval features must not silently approve an operation that the underlying project/workflow requires a human to authorize.

No project path list, risk tier, or approval threshold is invented here.

### `token-optimization.md`

Translate `harness-optimization/token-optimization.md` into one Codex-native persistent instruction surface.

Preferred placement depends on desired scope:

- a dedicated Harscode Codex profile's `developer_instructions` for a harness-wide behavior; or
- one appropriate user/project `AGENTS.md` location when the rule should apply at that scope.

Do not install the same rule in multiple always-loaded surfaces. The underlying Harscode token rule remains authoritative.

## Why there is no `codex/frontend/` yet

The initial translations above do not change by frontend/backend track. Creating a track split now would violate the existing harness-optimization rule that track folders exist only when the actual harness translation genuinely differs.

A future frontend Codex proposal is justified only if real dogfood finds a Codex-specific frontend mechanism that differs materially from backend/general operation — for example a stable browser/computer-use workflow, a genuinely different skill wrapper, or a track-specific subagent/tool boundary.

## Why no project-specific browser command appears here

The real incident that triggered this proposal included proving a target project's Playwright smoke separately from its fast unit-test baseline. That validates the existing Harscode rule that material rendered UI needs real rendered/browser verification.

It does **not** justify putting that project's `npm` command or test layout into Harscode. Codex should discover and use the target repository's native browser verification command through its project instructions/tooling.

## Capability basis, verified 2026-09-13

Current OpenAI/Codex documentation confirms the mechanics this translation relies on:

- `AGENTS.md` / `AGENTS.override.md` are hierarchical instruction sources, with more-specific project instructions layered later;
- Codex config supports `developer_instructions` and project document fallback filenames;
- Skills use progressive disclosure through selection metadata, `SKILL.md`, then optional resources/scripts;
- Codex provides sandbox/approval controls;
- current Codex configuration exposes multi-agent/subagent controls, but that surface is deliberately treated here as fast-moving and optional.

These are harness mechanics, so the new Codex README carries the same re-verification posture already required by `harness-optimization/README.md`.

## Rationale

This change is generic because it never names a target project, framework, command, domain, or protected path. It only explains how Codex's native instruction/context/execution mechanisms should express rules that already exist elsewhere in Harscode or the target repository.

The shape is intentionally smaller than the Claude Code tree. Harscode's own harness structure says a track split or mechanism-specific file should exist only where the translation genuinely differs. Codex already has strong hierarchical instructions and progressive-disclosure skills, so the first useful translation is to preserve source ownership and context discipline rather than recreate Claude Code's exact folder topology.

The proposal also keeps correctness independent of fast-moving native multi-agent support: if subagent mechanics change, the existing Harscode session-boundary guidance still works. That makes the translation degrade safely instead of turning one harness feature into a new workflow dependency.

---

*Accepted after human review on 2026-09-13. Add the target files and leave this proposal in place as the changelog entry. Re-verify Codex mechanics according to the new harness README's stated window.*
