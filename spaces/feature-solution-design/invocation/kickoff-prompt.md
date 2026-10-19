# S1 Kickoff — Harness-Neutral Human and Space Preflight

> **Status:** TEMPLATE for a PROPOSED / UNFORMED reusable Space. **Do not invoke** until the authorized Human has approved a pinned definition, actual runtime suitability has been checked against [execution requirements](../composition/execution-requirements.md), and the relevant Human has separately authorized the concrete project assignment.

## Human-to-Pairing request (after formation)

```text
Siapkan penggunaan Feature Solution Design Space untuk [approved project commitment].

Temukan current project authority dan pinned baseline. Periksa input/output
contract S1 dan kesesuaian binding, lokasi artifact/state, Specialist
capability requirements, independence, izin runtime, dan batas keputusan Human.

Laporkan preflight, risiko/blockers, dan authorization yang diperlukan.
Jangan mulai Space execution sebelum invocation ini disetujui.
```

This is a suggested human intent; the project's actual Pairing entrypoint may use different wording. Natural language is **not** authorization.

## Space assignment entry (after scoped invocation authorization)

```text
Operate only within an explicitly authorized Feature Solution Design Space invocation.

Read the pinned Space definition's SPACE.md and AGENTS.md, required generic
contracts, composition/input-output-chain.md, composition/execution-requirements.md
and composition/interaction-sequence.md when sequencing handoffs or review; read
this kickoff and the actual assignment binding, scoped project
instructions and original approved authority directly.

Confirm the pinned input revision, output destinations, permission boundaries,
current durable state owner, Specialist capability fit and independent reviewer
context against actual runtime observations. Report BLOCKED and stop if a
material precondition or required Human approval is absent.

Assign bounded responsibilities using composition/responsibilities.md. Give
each responsible Specialist its profile, relevant local guidance/guardrails/
knowledge, exact input revisions and authorized output paths. The runtime
adapter/launcher is external; do not assume these Markdown files instantiate
native agents or grant tools/models.

Preserve source → intermediate → output → reviewer traceability. Route material
findings to the owning producer; the reviewer reads original project authority.
Assemble only actually available, checked artifacts into the delivery bundle.

Do not implement production features, modify product meaning, bypass privileged
approval, infer a valid runtime claim, or treat internal review as integrated
product assurance. Return real output refs, observed conformance and
independence, blockers, Human acceptance required, and next action.
```

Actual harness-specific launch commands, model/effort policy, sandbox controls and session/subagent mechanics are **not** defined by this Space. They belong to Harscode-level harness translation plus the authorized project/runtime binding. If the chosen runtime cannot satisfy a material execution requirement, report NOT READY rather than silently weakening it.

Use [state and handoff](state-and-handoff.md) only when staging preflight/operation; kickoff is not automatic execution.
