# Rancang — Artifact Guidance and Representation Priority

> **Applicability:** Optional authoring aids for the [Rancang output contract](../contracts.md); not an independent approval authority, file-layout mandate, serializer or evidence that outputs exist.

## Precedence and selection

Start with the target project's **current, effective, approved** engineering/Design document standards, API/schema source conventions, diagram notation and existing artifact destinations. **Those project standards take precedence over these Space examples, including where different**, subject to binding Product/Design acceptance, security/protected scope and Human gates. If an artifact format is project-owned and requires a separately approved change, do not edit it without that authorization. See [Space-wide precedence](../../../space-formation.md#project-standards-take-precedence-over-space-base-knowledge).

Choose a representation based on the consumer's actual question: a simple decision table or Markdown section can suffice; an OpenAPI file, diagram, state chart, event schema or separate document is necessary **only when project standards or the actual consumer justify it**. Do not create a fixed number of output files, mandate a diagram per flow, or insert a new source-of-truth copy merely to fill a template.

## Minimum durable artifact envelope

Each materially consumable artifact or addressable bundle section needs these logical facts (not mandatory YAML keys):

| Required fact | Meaning |
| --- | --- |
| Identity, type, owner | Stable ID/anchor, X1 or O1–O5 / supporting contract kind, accountable producer and owner of original authority |
| Revisions and provenance | Actual source I1–I4 anchors + revisions, formed definition reference, output ref/revision, actual input/output dependencies |
| Meaning and standing | Material decision/contract, binding source vs delegated proposal vs Human-pending/unresolved status, scope and exclusions |
| Assurance | Produced vs independently reviewed, executed vs planned verification, exact reviewer/evidence refs and known limits |
| Consumer handoff | Named consumers, actual format compatibility and project-bound fit checks, blockers and conditions for use |

Timestamp, model and Agent/session details should be recorded **only when known, safe and relevant**. Do not invent identifiers, approvals, tool runs or separate metadata files. For an unperformed test write `NOT RUN`, not `PASS`.

## Solution Delivery Bundle — logical index

The Coordinator returns a **revision-pinned index** of X1 and applicable O1–O5 plus any separately authorized typed payload. For each entry provide ID/type, owning producer/project authority, exact artifact ref and input revisions, approval/review standing, intended consumers, compatibility evidence, limitations, required decision and next safe action. Index a source contract by reference rather than create a second independently editable canonical version.

`COMPLETE` means the Space fulfilled applicable production and internal review obligations with truthful limits, **not** that the Human accepted the output or the implementation passed tests. If formal project-required artifacts are missing, mark the affected consumer conditional or `BLOCKED`; never treat a draft interface as an accepted OpenAPI schema.

[Logical templates](templates.md) · [Conditional illustrative examples](examples.md) · [Space I/O and result standing](../contracts.md)
