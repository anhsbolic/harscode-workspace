# Proposal 0035 — Orchestrator Protocol v0.1 Pilot

Status: Accepted for pilot validation
Date: 2026-09-19
Protection Tier: general

## Problem

The operational workflow assumes one task workspace with ordinal phase folders. Real delivery can branch, re-enter phases, run frontend/backend work in parallel, require explicit human decisions, and accumulate reusable project learning. Directory order therefore cannot safely represent execution chronology or current delivery state.

## Proposed direction

Introduce a project-agnostic orchestration layer with:

- logical Work Units;
- event/run-based chronology;
- Role / Specialization / Participant / Session separation;
- explicit Decision, Finding, Blocker, and Dependency semantics;
- scoped knowledge retrieval and specialization routing;
- optional durable Harscode Spaces;
- Control Surface projection;
- scheduling state plus NOW/NEXT/LATER;
- workflow-gap proposal rather than silent workflow invention.

Adapt canonical workflow invocation so orchestrated runs can use explicit Run paths and prior-artifact pointers instead of relying on ordinal task-folder chronology.

## Authority boundary

The Orchestrator coordinates approved work. It does not create project product/domain/design/security authority.

## Validation

Validate this candidate through Kencleng Slice 1 — Public Campaign Understanding. Do not promote to `main` solely because the conceptual model is accepted. Promotion requires CRTV evidence.

## Human review

The project owner explicitly approved the v0.1 protocol design and requested a dedicated pilot branch before real-task validation.
