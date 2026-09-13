# permissions-and-sandbox.md (Codex)

## What this translates

Harscode and the target repository already decide:

- which phase owns which kind of work;
- which files/areas are protected;
- when a human must authorize or review work;
- what evidence a task needs.

Codex sandbox, network, and approval controls are **execution controls for those existing decisions**. They are not a new policy source.

## Default mapping by phase

Use the narrowest environment capability that still allows the current Harscode phase to complete.

```text
Exploration + Techplan
→ read-mostly; write only task/planning artifacts when required

Build + Patch
→ workspace write, narrowed to the authorized project scope

Code Review
→ read-only production code where practical

Testing
→ read-only production code where practical; allow the commands/artifact writes objective verification actually requires

Pull Request
→ repository/GitHub actions only to the extent explicitly authorized by the user/project workflow
```

This mapping supports Harscode's existing separation-of-authority principle. It does not create new phase rules.

## Protected paths

The protected-path list comes from the target repository's applicable instructions/specs, not from this file.

When a target repo says an area is read-only without explicit human authorization:

- keep it outside the ordinary write path;
- do not use a sandbox escape, alternate tool, subagent, connector, or script to route around the restriction;
- if the task genuinely requires the protected write, surface the boundary and obtain the authority the target repo requires.

A harness control should make the policy easier to follow, not provide a second way around it.

## Human-required approval stays human-required

Codex can route some approval prompts through automated reviewers or other approval mechanisms.

Do not configure automation to silently approve an operation when the underlying project/Harscode rule requires explicit human authorization or human review.

Examples include any target-repo-defined protected/Tier-0 area, manual production/destructive operation, or another gate that the owning source explicitly reserves for a person.

This file does not define which operations are human-required; it preserves whatever the authoritative source says.

## Network access

Prefer explicit, task-relevant network access over open-ended outbound access.

Before enabling a new destination/tool, ask whether the active phase actually needs it:

- dependency/docs lookup may need package/vendor documentation;
- browser/integration verification may need the target stack/service;
- ordinary local code review often needs no network at all.

Do not broaden network access merely to avoid fixing an environment/setup problem that should be solved locally.

## Connectors / MCP / external tools

External tools are useful when they expose a real project dependency (GitHub, issue tracker, browser, etc.), but they do not change source ownership.

A connector write should obey the same authority boundary as an equivalent local/CLI write.

For example, if the workflow says a PR may be prepared but not merged without human review, using a GitHub connector does not turn merge into an agent-owned action.

## Secrets and credentials

Harness configuration may reference authentication mechanisms, but project guidance about secrets still applies.

Do not:

- embed reusable secrets/tokens directly in checked-in Harscode examples;
- print secret values into reports/logs;
- widen credential scope because a tool supports it.

Use the harness/platform's supported credential storage and the minimum scope needed for the task.

## Failure posture

When Codex cannot complete a phase because the sandbox or approval boundary blocks a needed action:

1. verify the action is actually required by the current plan/phase;
2. verify the target repo/Harscode authority allows it;
3. request only the narrow capability/approval needed;
4. continue once the boundary is satisfied.

Do not rewrite the requirement, skip evidence, or broaden the whole environment just to make the blocker disappear.

## Configuration snippets are examples, not policy

Codex configuration keys and allowed values change faster than Harscode workflow rules.

Any concrete `config.toml` / requirements example derived from this document must be re-verified against the current Codex version before use. Prefer documenting the intended capability boundary here and keeping machine-specific values in the user's/target project's actual configuration.
