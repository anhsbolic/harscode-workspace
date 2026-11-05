# Engineering Project Standards — Definition & Evolution

> **Standing:** A4 ZERO-BASED RESEARCH DRAFT / HUMAN CONTENT REVIEW PENDING (2026-11-05). Direct reusable guidance, **not a formed Space**, not project-owned technical policy, not operational Harscode `main` and not a tool/write authorization.
> **Owner:** Guidance for locating, evaluating, adopting and reconciling **the target project's own** reusable Engineering Standards.

## Direct entrypoint

- [Definition](definition.md) — applicable technical-rule meaning, decision process and usable result.
- [AGENTS](AGENTS.md) — source selection, security, permission and change boundaries.
- [Authority and Handoff](authority-and-handoff.md) — ownership, acceptance, supersession and consumer sufficiency.
- [Rancang Engineering Solution](../spaces/rancang/README.md) — a *consumer* of project standards, not the default standards owner.

## When this concern matters

Use it when real cross-feature technical rules need to be identified, assessed for adequacy, introduced, changed or reconciled: architecture/stack conventions, shared API/event/data rules, persistence/migration compatibility, relevant security/privacy baseline, reliability/operability constraints, testing/SOP or other material engineering practices.

**Reuse/no change is a complete answer** when current effective project rules suffice. A new project need not invent a catalog or directory of standards before ordinary delegated solution design can begin. Project standards may already live in ADRs, code-owned authoritative contracts, accepted project configuration or other valid project sources; their *standing* matters more than file extension.

This folder **does not own** Product/UX meaning, feature-specific architecture, individual API/schema adoption, implementation, runtime/installation, deployment or Harscode-wide technical policy. It is **not** a universal best-practices library or workflow engine.

## Core boundary

The owning project and legitimately delegated Human/Engineering authority determine what is effective. Rancang may report a missing project-wide rule or propose a narrow candidate; only the relevant project standards authority can approve its adoption or supersession. Security-sensitive rule changes require independent protection scrutiny, not only Engineering feasibility.
