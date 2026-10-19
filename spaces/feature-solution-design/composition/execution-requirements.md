# S1 Specialist Execution Requirements — Harness-Neutral

> **Status:** Reusable capability requirements of a PROPOSED / UNFORMED Space. These are **not** runner configuration, native agent definitions, implementation mechanics, or runtime evidence.

This document owns what the execution environment **must make possible** for S1's declared I/O contract. Harscode-level `harness-optimization/` owns translations into particular harnesses; each authorized invocation owns concrete model/tool/context choices, permissions and observed readiness.

## Required capabilities

| ID | Space requirement | Observable readiness / failure evidence |
| --- | --- | --- |
| R1 — Source fidelity | Each Specialist can inspect applicable original authority and pinned current project baseline, not only forwarded summaries | Real source/revision reads; missing access or stale binding → BLOCKED |
| R2 — Bounded artifact production | Producers can write only their approved solution/evidence artifacts and return inspectable refs/revisions | Effective write boundaries inspected; unauthorized output locations → NOT READY |
| R3 — Scoped Specialist context | Each role can access its own profile, guidance, guardrails and relevant **agent-owned knowledge** without globally loading every package | Actual context construction and read evidence; incomplete context → NOT READY for affected responsibility |
| R4 — Review independence | Reviewer can inspect original authority + current producer artifacts in a context sufficiently independent to catch producer assumptions; must not edit producer-owned output | Execution topology/context isolation is stated and checked; independence not observed → INDEPENDENCE UNVERIFIED, and no claim that independent review requirement was satisfied |
| R5 — Versioned handoffs | A later Specialist can identify source/producer output revision, unresolved findings and decision standing without chat recall | Actual artifact and state refs, checked version joins and fresh-reader reconstruction; otherwise PARTIAL/BLOCKED as appropriate |
| R6 — Explicit Human gates | Human-invoked Coordinator enforces [consequence-based Human gates](human-approval-gates.md) in both modes, pausing before protected/material transitions with exact revision/authority and resuming only within valid scope | Actual decision/authorization and applicable tool enforcement checked; missing/stale approval → BLOCKED for affected action |
| R7 — Truthful evidence | The runner/operator can distinguish performed tests/checks from proposed ones and record actual results, tools and limitations | Source-linked report; never claim MODEL VERIFIED, independent or runtime PASS merely from a declarative profile |
| R8 — Coordinator/observability | The selected runtime supports Human-direct Coordinator interaction, meaningful supervised progress review (default), or explicitly Human-selected autonomous delegation; actual Agent/context routing and durable reporting are checked | No self-selected autonomous mode or hidden bypass of Human gate; unsupported delegation/pause-resume → NOT READY for the requested mode |

## Capability needs, not model configuration

- Requirements Analyst: faithful source retrieval, requirements/authority discrimination, precise trace.
- Solution Architect: coupled cross-boundary tradeoff reasoning, data/identity consistency and risk analysis.
- Experience Specialist: interaction/state semantics, applicable design source fidelity, observable negative paths.
- Solution Reviewer: critical source comparison and contradiction detection with verifiable context independence.

Apply proportionate reasoning depth based on task risk/ambiguity; no preset model ID, vendor-specific reasoning effort, invocation command, tool name, sandbox scheme, or number of native subprocesses belongs here. The actual harness translation **must not modify these required semantics** merely for tool convenience.

## Preflight and first-use evidence

The authorized runtime/operator records selected harness and version when known; how each R1–R8 is satisfied or limited; project revision and Space definition SHA; tool and path access; permitted model/effort policy; source/Agent knowledge loading behavior; and reviewer independence evidence. Unknown/unavailable capability is a readiness gap, not assumed success.

If a future harness cannot meet a material requirement, select another authorized execution approach, seek a scoped Human decision, or report NOT READY. Do not create a scheduler, registry or universal adapter merely to satisfy this definition.
