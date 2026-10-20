# Harness — Foundation Research

> **Status:** WORKING / RESEARCH-ONLY. No runtime or adapter is verified or activated by this directory.

## Purpose

Translate **already-owned** Engineering Space requirements and repository protections into the native behavior of an actual tool/harness. Translation is not policy creation. Applicable Product/Design meaning, Space I/O, human approvals and Specialist knowledge remain with their owning domains.

| Need | Read |
| --- | --- |
| Bind a concrete engineering assignment to a verified runner | [Runtime binding](runtime-binding.md) |
| Codex-specific concerns and verification triggers | [Codex adapter](codex.md) |
| Hard routing/permission limits | [Harness AGENTS](AGENTS.md) |

No global harness configuration is provided or implied. Do not infer an available model, subagent system, skill, permission profile or review isolation from docs written for a different harness version.

## Boundary

- **Engineering** defines reusable capability semantics and required evidence: [Engineering](../engineering/README.md).
- **Collaboration** supports Human decisions, but cannot run or authorize a Space by proxy.
- **Harness** checks whether the selected CLI/host can actually enforce those semantics, then implements only the needed translation.

If a mechanism cannot enforce a hard requirement, report the deviation and affected readiness. Do not silently weaken security or independence because the tool has no matching feature.

[Architecture](../ARCHITECTURE.md) · [Checklist](../REFACTOR-CHECKLIST.md)
