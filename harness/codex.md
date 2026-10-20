# Codex Adapter — Research Guidance

> **Status:** WORKING / UNVERIFIED against the currently installed Codex runtime.
> **Owns:** Codex-specific translation when Codex is selected as the Engineering Space harness. **Not** a source of Engineering policy.

## Verify native mechanics before proposing a launch

- CLI version and available model/effort selection in the **actual** environment.
- Hierarchical instruction loading, task-local skills and available native agent/subagent topology.
- Filesystem write scope and sandbox/network restrictions, approval behavior, tool execution permissions and effective protected paths.
- Context separation for independent review, source access across project worktrees and artifact durability.
- Support for meaningful Human supervision, pause/resume and consequence-based gates.

Do not copy historical Codex flags from [legacy adapter reference](../deprecated/legacy/harness-optimization/codex/README.md) without checking the selected installed CLI. Names such as `workspace-write` or `on-request` may describe native permission settings in a particular version; neither confers Human authority or automatically enforces narrower task-specific output paths.

## Separation

The Space determines WHAT must be produced, reviewed and handed off; this adapter determines WHETHER and HOW Codex can implement those requirements. Native Specialist count/config and model effort are replaceable choices. **An independent Reviewer claim requires observed source access and context independence**, not merely a distinct profile file.

A writing-capable multi-repository workspace may expose sibling repositories to the same agent. Inspect effective permissions and constrain actual actions before relying on a project's protected-path policy. A prompt instruction is not equivalent to filesystem enforcement.

If the intended Space cannot satisfy a material runtime property, report its precise limitation; do not silently substitute a weaker mode or claim an experimental deviation passed.
