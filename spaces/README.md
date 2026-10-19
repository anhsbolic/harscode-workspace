# Reusable Spaces — Station 5 Research

> Status: EXPERIMENTAL candidate definitions on `research/harscode-purpose-llm-fit`, not Harscode `main` or a proven catalog.

A Space is a bounded reusable production capability with an inspectable external input/output contract, internal responsibility map, and honest evidence. Formation requires approval from the authorized Human owner; a definition does not grant project write permissions, runtime access, Specialist dispatch, or invocation.

## Current candidates

- [Feature Solution Design](feature-solution-design/SPACE.md) — **PROPOSED / UNFORMED**. Tech-agnostic reusable responsibility, stack-aware project assignment; C1 Kencleng is a prospective first real-use test, not embedded Space policy.
- Other previously discussed capabilities (Go Backend Works, Next.js Frontend Works, FE/BE Integration, Independent Assurance) remain **conditional composition proposals**, not formed Spaces.

## Routing and authority

- [Space Formation guidance](../space-formation/README.md) owns formation criteria and the Human formation-approval boundary.
- [Balad Pairing](../pairing/AGENTS.md) provides Human-facing advice on project authority, candidate Space discovery, end-to-end chain and consumer compatibility, and may propose Formation Requests. It **does not invoke, request or coordinate with Space Coordinator Agents**. The Human initiates authorized Space execution directly.
- Each Space owns its generic contracts, **Space Coordinator Agent role** and internal Specialist responsibilities, consequence-based Human approval gates, and harness-neutral execution requirements. Harness-specific translation belongs to Harscode-level `harness-optimization/`, while concrete runtime settings and proof belong to the authorized invocation. Project-specific inputs/outputs and approved product meanings remain with the target project.
- Only a definition with explicit Human formation approval + pinned Git revision can be called FORMED. Do not infer formation from the presence of files here.

Read just the selected Space's `SPACE.md` and scoped `AGENTS.md`; do not load every Agent package or every Space by default.
