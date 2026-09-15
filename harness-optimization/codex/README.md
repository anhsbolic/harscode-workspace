# codex/ — OpenAI Codex harness translations

**Effective as of:** OpenAI Codex CLI / Codex agent mechanics documented in September 2026
**Last verified:** 2026-09-15
**Re-verify:** every ~2–3 months, or after material Codex changes to instruction loading, skills, sandbox/approval, sessions/subagents, usage/status surfaces, or hosted capabilities.

## Scope

Translation only. Never policy.

Portable rules live in `workflow/` and `best-practices/`. This directory maps them onto Codex-native instruction/session/skill/sandbox behavior.

## Mapping

```text
project hard rules / routing
→ target repo hierarchical AGENTS.md

on-demand reusable procedures / knowledge discovery
→ Codex Skills / targeted references

phase/context separation
→ workflow/context-management.md translated by session-boundaries.md

runtime write/network/tool authority
→ permissions-and-sandbox.md

session usage / CRTV operator observability
→ benchmarking.md

output/process terseness
→ token-optimization.md translation
```

Do not create a giant `CODEX.md` or duplicate the same persistent rule across profile/user/project/skills.

## Canonical phase prompts

Start each lifecycle phase from Harscode's canonical root `workflow/*-prompt.md`. A Codex wrapper may resolve variables and add target-repo/execution-profile context; it may not maintain a re-authored lifecycle copy.

## Execution profiles

A target project/user may configure fast-moving mechanics such as model, reasoning effort, CLI/client, browser/rendered capability, image/design capability, and other tool availability. That profile lives in target/user configuration, not generic Harscode workflow policy.

A stronger model does not skip a workflow gate. A missing capability does not erase an evidence obligation; satisfy it another authorized way or surface the gap.

Do not put project-specific model names/commands/paths in this reusable translation directory merely because one project uses them.

## Files

- `instruction-loading.md` — hierarchical instruction loading / avoiding duplicate project policy.
- `skills.md` — progressive-disclosure wrappers around existing Harscode sources.
- `session-boundaries.md` — same/fresh session translation and re-grounding.
- `permissions-and-sandbox.md` — runtime authority translation and proportional destructive-operation approvals.
- `benchmarking.md` — session-level usage/quality observability for CRTV/operator benchmarking.
- `token-optimization.md` — output/context-efficiency translation.

There is no Codex frontend/backend split by default. Add a track only when Codex translation itself differs materially, not when stack guidance/model preference differs.

## Project instancing

Actual target-repo `AGENTS.md`, `.codex/skills/`, concrete config values, browser/test commands, protected-path lists, benchmark artifact paths, and execution profiles belong in the target repo/user config.

## Capability references

Fast-moving Codex mechanics should be re-verified against current OpenAI/Codex sources before concrete configuration is copied into a project. Harness drift must not silently rewrite Harscode lifecycle policy.
