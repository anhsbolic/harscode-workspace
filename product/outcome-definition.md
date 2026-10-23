# Outcome Definition

> Scope: Harscode Product guidance in the current branch. The target project and its authorized Human own Product semantics; no change to operational main.

Phase: `PROD-DEF`. Output kind: `PROD-CONTRACT` — Product Contract.

## Purpose

Turn the Human-selected bounded outcome into a self-contained Product Contract. A downstream consumer must be able to understand binding Product meaning from that document, without chat history or decoding upstream research identifiers.

## Define the outcome

Describe actor entry, pre-effect understanding, attributable and permitted actions, truthful successful state, durable inspectability, failures, incomplete/uncertain paths, and scope exclusions. Keep Product semantics separate from UI form, authentication timing, APIs, data models and implementation mechanisms.

Specify outcome-level Success Criteria, approved behavior and invariants, Product requirements, observable Acceptance Criteria, dependencies and delegated solution freedom. Acceptance should trace to obligations and Success Criteria *inside the contract*. Requirement count is not evidence of Product coherence.

Product must reconcile current primary authority, conflicting claims and upstream references before exact-revision approval. Material missing business meaning returns to the Human decision owner; do not import historical requirements by inheritance.

## Codes and consumer boundary

Use phase and output type codes from [Product phase catalog](README.md). The target project owns the stable outcome instance key and within-contract identifiers. Upstream reference codes are Product provenance; they do not carry additional binding semantics outside the approved Product Contract.

An important compatibility limit remains: formed Rancang v3 currently requires original upstream source inspection. This Product-side boundary is not an effective Rancang amendment; Rancang behavior can change only after its owning definition receives separate approval.

## Template

[Product Contract — Bahasa Indonesia](templates/product-contract.id.md) or [English](templates/product-contract.en.md). These provide an authoring shape, not a mandatory file count, Product Space or Engineering invocation.

Next: Product Review & Approval (`PROD-APR`).
