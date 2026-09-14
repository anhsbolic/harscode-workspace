# AGENTS.md — harness-optimization/

This tree translates existing Harscode policy into harness-native mechanisms. Do **not** read the full harness-optimization README by default merely to route ordinary work.

## Hard rules

- **Translation only. Never policy.** The underlying rule must already exist in `workflow/` or `best-practices/`.
- Files in this tree are proposal-gated on ordinary work; use root `proposals/`.
- Read the specific harness README/file needed for the active mechanism; do not scan unrelated harness tracks.
- Harness capability/version claims are time-sensitive. Respect each harness README's effective/verified/re-verify disclaimer.
- Project-specific harness instances/config belong in the target repo or user configuration, not in this reusable translation tree.

## Routing

- Cross-harness output efficiency → `token-optimization.md`
- Codex → `codex/README.md` and the specific mechanism file it routes to
- Claude Code → `claude-code/README.md` and the relevant track/mechanism only
