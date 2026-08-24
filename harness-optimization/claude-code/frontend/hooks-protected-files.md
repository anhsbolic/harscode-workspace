# hooks-protected-files.md (Claude Code, frontend track)

**Tier:** 2 — higher risk than Tier 1. A hook that's too aggressive
silently blocks legitimate edits (and an agent may just work around it in
a way that's harder to notice than an honest failure); a hook that's too
narrow gives false confidence that protection exists when it doesn't.
Keep the matching logic as simple as possible — a plain path deny-list,
not clever pattern inference.

## What this translates

This workspace already declares certain files agent-protected —
`best-practices/`'s entire tree, `workflow/<high-ceremony-phase>/`'s
`template.md`/`rules.md`/`guardrails.md`/`guidelines.md`-class files,
`harness-optimization/` itself. Today that protection is enforced by a
line in each tree's `AGENTS.md` — prose an agent is expected to read and
honor. This workspace has already directly observed, more than once, that
a rule restated as prose gets skipped regardless of model or person (see
`workflow/2-techplan/retro.md`) — and this same workspace's own drafting
process for this pillar hit that exact failure (a protected-file edit
made directly instead of via proposal, caught only on manual review, not
prevented). A `PreToolUse` hook makes the same rule hold deterministically
instead of depending on the rule being read and remembered.

## Pattern

```json
// .claude/settings.json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          { "type": "command", "command": ".claude/hooks/protect-paths.sh" }
        ]
      }
    ]
  }
}
```

```bash
#!/usr/bin/env bash
# .claude/hooks/protect-paths.sh
# Reads tool input JSON on stdin; exits 2 (blocking) if the target path
# falls under a protected tree. Keep this list a plain match, not
# inferred — a protected path either is or isn't in the list.

INPUT=$(cat)
FILE_PATH=$(echo "$INPUT" | jq -r '.tool_input.file_path // empty')

PROTECTED_PATTERNS=(
  "best-practices/*"
  "workflow/*/template.md"
  "workflow/*/rules.md"
  "workflow/*/guardrails.md"
  "workflow/*/guidelines.md"
  "harness-optimization/*"
)

for pattern in "${PROTECTED_PATTERNS[@]}"; do
  if [[ "$FILE_PATH" == $pattern ]]; then
    echo "Blocked: $FILE_PATH is agent-protected. Write a proposal to \
proposals/ instead of editing directly." >&2
    exit 2
  fi
done

exit 0
```

The protected-path list here is illustrative of the *pattern*, not a
fixed inventory — it must be kept in sync with whatever each tree's own
`AGENTS.md` actually declares protected, since that's the real source of
truth this hook is enforcing, not inventing.

## Checklist

- [ ] The protected-path list in the hook script is derived from what
      each tree's own `AGENTS.md` already declares, not independently
      decided here — the hook enforces an existing rule, it doesn't set
      one (see `harness-optimization/README.md`'s translation-only rule)
- [ ] Matching is a plain path/glob check, not an attempt at semantic
      inference ("does this edit look like a typo fix") — clever
      matching is exactly where a hook becomes a silent failure mode
- [ ] The hook's block message tells the agent what to do instead
      (write a proposal), not just that the action failed — an agent
      that hits a bare rejection with no next step tends to route
      around it rather than follow the correct process
- [ ] The hook is tested against both a case that should block and a
      case that shouldn't, before being trusted — asymmetric failure
      (over-blocking legitimate work vs under-blocking a real violation)
      are different failure modes and both need a check
- [ ] This hook protects paths; it does not replace the actual proposal
      review process — a hook stops an unproposed direct edit, it
      doesn't evaluate whether a proposal itself is any good. That stays
      a human, same as every other pillar's governance model