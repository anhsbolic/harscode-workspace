# S1 Artifacts — Envelope, Relations and Evidence

Artifact **semantics** are stable; Markdown with addressable headings/tables is first-pilot default, not mandated universal YAML/JSON. Formal interfaces may additionally require source OpenAPI/schema when authorized. Never confuse output-document existence with evidence of correctness.

## Minimum envelope for every durable S1 artifact

| Field | Required content |
| --- | --- |
| Identity and kind | Stable artifact ID + `I`, `X`, `O`, `REVIEW`, or invocation-state role; source/producer responsibility |
| Revision and provenance | Actual source Git SHA/immutable reference, produced timestamp when known, Agent/model/effort/session only when exposed and safe; omit unknown optional metadata |
| Authority | Owning original source refs and approval/decision standing; solution choices must not be labeled original Product Authority |
| Dependencies | Input IDs/source anchors consumed + revisions; affected downstream artifacts/consumers |
| Content | Checkable decisions, boundaries, formats and references appropriate to this artifact kind |
| Result/evidence | Complete/partial/blocked/failed, check executed vs proposed, unresolved items and next valid action |

Keep **one owning file for a decision** and **one accountable authority for a shared interface revision**; reference rather than duplicate competing canonical content in other artifacts. Intermediate X1 may be stored as a separate working record; the bundle can link to it. An index of linked domain artifacts is a handoff aid, not a project-truth duplicate. Git history is default artifact revision history where tracked. A section-ID plus pinned file SHA is an acceptable anchor for pilot output; don't invent unneeded databases or IDs.

## Cross-Space payload indexing

When an S1 artifact (or addressable O1–O5 section) is offered for downstream consumption, include it in the [Solution Delivery Bundle index](delivery-bundle.md) with kind/contract obligation, owning producer and project authority, exact content ref/revision, relevant original source revisions, intended consumer(s), evidence, decision/approval standing and specific constraints. Additional API, state or experience documents are **consumer-driven**, not required for their own sake. A `COMPLETE` S1 delivery never implies a listed payload has Human acceptance or that FE/BE have validated it.

## Decision record semantics

Each material O1/O2/O3 decision should capture: `ID`, linked I1 requirement/invariant(s), applicable constraints I2, alternatives when material, chosen or proposed solution and reason, decision authority (`APPROVED SOURCE`, `DELEGATED DECISION`, `PROPOSED / HUMAN REVIEW REQUIRED`, `UNRESOLVED`), affected interface/state nodes, and acceptance/test hook. Human-approved changes update owning project source, not only the S1 report.

## Traceability relation semantics

Record rows `source/ref + requirement ID → intermediate X1 → material O1/O2/O3 anchor → O4 verification obligation → O5 review verdict`. If a requirement requires no changed solution surface, document the reason and observable evidence boundary. Coverage counts cannot silently treat `UNKNOWN` as satisfied.

## Disagreement and failure

A contradiction is recorded with both exact source locations and respective authority. An unsupported product decision remains blocked for relevant consumers. If a produced artifact exists but reviewer cannot inspect its revision, mark **UNVERIFIED** instead of saying passed. Don't recreate huge chat transcripts as process evidence.

## Example envelope (illustrative, not parser)

```yaml
artifact_id: O2
kind: interface-and-invariant-contract
space_definition_ref: <approved-git-sha>
invocation_ref: <project-owned-reference>
project_source_ref: <pinned-project-sha>
producer: solution-architect
input_refs: [X1, I2, I3]
result: PARTIAL
decision_standing: PROPOSED / HUMAN REVIEW REQUIRED
output_ref: <actual-project-owned-artifact-path-or-commit>
verification:
  performed: false
  reason: pending review
```

No exact local paths/identifiers, timestamp, model or tool evidence should be invented. Separate optional operational continuity from canonical output authority.
