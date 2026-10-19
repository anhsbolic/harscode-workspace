# S1 Input → Specialist → Output Path Relations — Proposed

This is an **inspectable responsibility and evidence DAG**, not a mandatory sequential engine. Node/edge labels are semantic contracts, not assumed files, job IDs or native Agent objects in any particular harness.

## Internal production paths

```mermaid
flowchart TD
 I1["I1 Approved behavior, requirements, acceptance"]
 I2["I2 Project architecture, design, security constraints"]
 I3["I3 Live repo/target revision"]
 I4["I4 Authorized scope, consumer expectations"]
 A1["P1 Requirements Analyst"]
 X1["X1 Source/requirement & decision-boundary map"]
 A2["P2 Solution Architect"]
 X2["O1 Shared decisions"]
 X3["O2 Interface and invariant contracts"]
 A3["P3 Experience Specialist"]
 X4["O3 Experience/state contracts"]
 A4["P4 Solution Reviewer (independent context)"]
 X5["O4 Verification obligations"]
 X6["O5 Trace, review and conformance evidence"]
 B["Solution Delivery Bundle"]
 I1 --> A1
 I2 --> A1
 I3 --> A1
 I4 --> A1
 A1 --> X1
 X1 --> A2
 X1 --> A3
 I2 --> A2
 I3 --> A2
 I2 --> A3
 A2 --> X2
 A2 --> X3
 X2 --> A3
 A3 --> X4
 I1 --> A4
 I2 --> A4
 I4 --> A4
 X1 --> A4
 X2 --> A4
 X3 --> A4
 X4 --> A4
 A4 --> X5
 A4 --> X6
 X2 --> B
 X3 --> B
 X4 --> B
 X5 --> B
 X6 --> B
```

## Edge contract / accountable responsibility

| Producer input → process → output | Accountable Specialist | Consumer and acceptance |
| --- | --- | --- |
| I1+I2+I3+I4 → P1 → X1 | Requirements Analyst | Architect and Experience Specialist: cited scope, binding invariants, open decisions, authorization/tech constraints; source classification correct |
| X1+I2+I3 → P2 → O1/O2 | Solution Architect | Experience Specialist + Reviewer + backend/frontend consumers: architecture, ownership, explicit interaction/transport/data semantics and errors, without inventing authority |
| X1+I2+O1/O2 → P3 → O3 | Experience Specialist | Reviewer + future frontend/backend consumers: experience states, form/action conditions and consequence/persistence meaning, consistent with interfaces |
| Original I1+I2+I4 and X1+O1+O2+O3 → P4 → O4/O5 | Solution Reviewer | Space outcome: independent source fidelity, coverage and cross-contract findings; no edits to producer artifacts |
| O1+O2+O3+O4+O5 → bundle assembly | Space coordinator responsibility | Human/Balad for scoped decision and handoff; future consumers only after accepted, compatible real output |

Reviewer findings affecting X1/O1/O2/O3 go **back to the responsible producer** for scoped revision, then affected review re-runs. The coordinator records version compatibility and whether follow-up is required. The reviewer may author findings/verification obligations but not quietly “fix” producer material.

## Invariant propagation test (generic)

For a material project invariant: locate original source anchor → X1 requirement/authority map → O1/O2/O3 design commitment(s) → O4 test obligation(s) → O5 reviewer source check → future consumer. Missing any applicable link is a traceability/coverage failure. A test obligation may have more than one evidence producer.

The reviewer must receive *original I1/I2*, not only X1 or producer descriptions. Agent-owned knowledge can inform techniques but never establishes authoritative project behavior. The diagram does not claim consumed inter-Space links: future Go/NestJS/Next.js contracts must be checked when they exist.

## Scheduling and independence

P2 and P3 may collaborate/iterate on shared decisions, but they cannot produce contradictory accepted contracts. P4 must be sufficiently isolated from production reasoning to credibly check against originals; prefer a fresh context when supported. If the selected runtime cannot provide demonstrable independence, report the limitation, do not fabricate it. No hard-coded four-session requirement or parallelism.
