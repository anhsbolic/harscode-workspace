# codex/ — OpenAI Codex harness translations

**Effective as of:** OpenAI Codex CLI / Codex agent mechanics documented in September 2026
**Last verified:** 2026-09-13
**Re-verify:** recommended every ~2-3 months, or immediately if Codex ships a major change to `AGENTS.md` loading, Skills, sandbox/approval behavior, or multi-agent/subagent mechanics.

## Scope

This directory translates existing Harscode rules into Codex-native mechanisms.

The parent rule still applies:

> **Translation only. Never policy.**

If a Codex-specific file would need to invent a lifecycle rule, testing obligation, risk threshold, approval rule, or engineering best practice, stop and propose that rule in `workflow/` or `best-practices/` first.

## Codex-native mapping

Use Codex mechanisms according to the concern they actually own:

```text
project hard rules / commands / fencing / routing
→ hierarchical AGENTS.md in the target repo

on-demand reusable procedures / best-practice discovery
→ Codex Skills

phase/context isolation
→ Harscode session boundaries first; Codex subagents optionally

runtime write/network/tool boundaries
→ Codex sandbox + approval configuration

cross-phase response terseness rule
→ one persistent Codex instruction surface
```

Do not create a giant `CODEX.md` by default. Codex already has a native hierarchical project-instruction mechanism; adding another always-loaded project policy file normally creates duplication rather than capability.

## Files

- `instruction-loading.md` — how Codex's `AGENTS.md` hierarchy maps to Harscode/project source ownership without duplicating policy.
- `skills.md` — how to wrap Harscode guidance as Codex Skills using progressive disclosure.
- `session-boundaries.md` — how Harscode's existing session guidance maps to Codex sessions and optional native subagents.
- `permissions-and-sandbox.md` — how Codex sandbox/approval controls reinforce existing authority without defining new authority.
- `token-optimization.md` — how to enforce the harness-agnostic Harscode output rule in one Codex-native persistent instruction surface.

There is no `frontend/` or `backend/` split yet because the initial translation above is track-agnostic. Add a track subfolder only when real use proves the Codex translation itself differs materially by track.

## Project instancing rule

Actual target-repo artifacts such as:

- root/nested `AGENTS.md` content;
- `.codex/skills/` packages;
- machine/user `config.toml` values;
- concrete browser/test commands;
- project protected-path lists;

belong in the target repository or user Codex configuration, not here.

This directory is the reusable translation pattern, not an instance of it.

## Capability sources used for this verification

- https://openai.com/index/unrolling-the-codex-agent-loop/
- https://openai.com/index/running-codex-safely/
- https://github.com/openai/codex/blob/main/codex-rs/core/config.schema.json
- https://github.com/openai/codex/blob/main/codex-rs/skills/src/assets/samples/skill-creator/SKILL.md

Treat these as fast-moving harness references. If current Codex behavior diverges from this directory, re-verify the mechanism first; do not silently rewrite Harscode policy to fit a harness change.
