# Rancang — Logical Artifact Templates (Optional)

> **Purpose:** Minimal *content prompts*, not obligatory files or project specifications. Use the actual project's accepted templates/notation first; if none exists, adapt these to the consumer. Each item needs the [artifact envelope](README.md#minimum-durable-artifact-envelope) or a shared, addressable bundle index. Omitted non-applicable fields need a short reason, not filler content.

## X1 — Source and obligation map

| Original source/ID + revision | Accepted obligation or negative path | Authority class/owner | In scope? | Consequential interface/experience/verification link | Unknown, delegated or Human-owned decision |
| --- | --- | --- | --- | --- | --- |
| `<ref>` | `<precise behavior and non-guarantees>` | `<approved / derived / delegated / historical>` | `<yes/no/conditional>` | `<O1/O2/O3/O4 ref or pending>` | `<owner + affected dependency>` |

Requirements Analyst creates X1; original authority is still read by producers and Reviewer. A line item is not accepted because it appears in this table.

## O1 — Shared solution decision

| Decision ID, linked X1 | Shared issue and actual consumer | Chosen/proposed rule + trade-off | Ownership/invariant | Standing and required Human gate |
| --- | --- | --- | --- | --- |
| `<id/source>` | `<problem>` | `<decision/rationale; material alternative if needed>` | `<owner>` | `<delegated/proposed/blocked>` |

Avoid catalogs of unselected architectures. Record only decisions necessary to avoid incompatible downstream interpretations.

## O2 — Interface, state and invariant contract

For each material boundary name producer and consumer; exact inputs, outputs, error/denial/partial/unknown outcomes; identity and authorization enforcement; state/data owner; transaction/consistency/retry requirements if triggered; source/acceptance links and current schema/API owner; proposed-vs-approved standing. If a formal interface is required, link the **actual project-owned** typed artifact and revision. Do not manufacture endpoint details to populate an example.

## O3 — Experience and state contract

| Actor intention/action | Prerequisite or authorization | System-owner state/result (O2 ref) | Truthful user-visible meaning | Failure/unknown/denied path | Acceptance/source + verification link |
| --- | --- | --- | --- | --- | --- |
| `<goal/step>` | `<precondition>` | `<actual owner, event/result>` | `<guaranteed and not guaranteed>` | `<only applicable states>` | `<I1/I2 / O4>` |

Experience Specialist aligns with current project Design authority; this is not a pixel/UI-component design template. Include pre-effect disclosure and durable later inspection only where accepted requirements call for them.

## O4 — Verification obligations (producer-owned)

| Source obligation | What observable result would pass/falsify | Negative/risk path | Future evidence boundary and owner | Performed evidence / NOT RUN |
| --- | --- | --- | --- | --- |
| `<X1 + O1/O2/O3>` | `<expected condition>` | `<relevant failure>` | `<unit/contract/integration/rendered/security owner when applicable>` | `<actual ref or NOT RUN>` |

Solution Architect and Experience Specialist produce O4 as applicable, with **one named accountable owner**; independent Reviewer assesses adequacy but does not edit it.

## O5 — Independent review and handoff

**Reviewer findings:** exact original source and output revisions checked; independent-context evidence/limits; source conformance and interface/experience/verification mismatches; severity and affected consumer; assigned producer correction; re-review standing. Never alter X1/O1–O4 to obtain PASS.

**Coordinator assembly and Human handoff:** actual bundle index/revision, triggered Human gates and their subject revisions, consumer-by-consumer fit (`verified / conditional / blocked / unverified`), result `COMPLETE / PARTIAL / BLOCKED / FAILED`, exact Human acceptance standing and next safe action. **Reviewer owns findings; Coordinator owns assembly**, not reviewer edits or final acceptance.

[Artifact envelope and bundle](README.md) · [Representation examples](examples.md)
