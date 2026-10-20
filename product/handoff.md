# Product-to-Consumer Handoff

> **Status:** WORKING / RESEARCH-ONLY. A semantic completeness test, not a required new packet format or execution stage.
> **Authority:** The target project's accepted product artifacts and exact revisions remain the only binding sources.

## Goal

A Design, Engineering, or Human advisory consumer should reconstruct **the same actor experience and product truth** from durable sources, without chat history or a new product decision.

The handoff must preserve two equally important things: the **human-facing narrative** explaining what is meaningful, and the **approved behavioral constraints/acceptance** protecting its truth. Neither replaces the other.

## Minimum answerable questions

| Concern | What a fresh reader needs |
| --- | --- |
| **Scope and authority** | Product/project, owning Human, approved artifact/revision, precedence, working versus binding decisions |
| **Actor outcome** | Relevant actor situation, meaningful action, successful change, and why it matters |
| **Experience anchor** | Narrative or bounded reference covering entry, pre-effect understanding, success, inspection and applicable negative paths |
| **Product obligations** | Confirmed behavior, invariants, material experience/system requirements and acceptance references; explicit source and standing |
| **Dependencies** | Real prerequisite product behavior versus specified/seeded/unimplemented behavior; conditional or blocked interfaces |
| **Boundaries** | What remains open, parked or out of scope; what Design can express and Engineering may decide |
| **Consumer** | Who needs which contract or evidence, and what claim is not yet proven |

These are **logical fields**. They can live in a small index linking authoritative files, in one cohesive artifact, or in a larger project-owned specification where warranted. Do not create hand-maintained copies of already authoritative behavior simply to fill a template.

## Preserve experience continuity

The recommended reading route is:

```text
Owning Product Authority and selected commitment
→ Actor experience anchor (with provenance/standing)
→ Confirmed product behavior and invariants
→ Applicable acceptance / experience / system requirements
→ Scoped dependencies, gaps and consumer boundary
```

An exploratory experience scene may be useful **supporting evidence**. Unless explicitly approved as authority, do not promote its choices over binding behavior/requirements. If the scene and approved behavior differ, use the approved source and flag any material contradiction.

Design may decide interaction form, visual expression and accessibility implementation without changing the consequential product meaning. Engineering may choose architecture, APIs, transactions, state design and test mechanisms within owning project constraints. Neither may silently decide an unresolved material business rule.

## Consumer readiness, not automatic invocation

A product commitment accepted for product elaboration may still require multiple solution-design or implementation assignments. The consumer chooses bounded work with its own input contract and authorization. **Product handoff does not prescribe one commitment = one Space or validate the downstream runtime.**

Check before downstream use:

1. The Human's exact approved product claim and current source revision are identifiable.
2. An actual person-facing narrative is available, with required exception meaning; it does not overclaim observed user evidence.
3. Semantic requirements and invariants remain binding and traceable to owning sources.
4. Material unavailable prerequisites, identity/security/trust boundaries and known external signals are visible rather than assumed.
5. Intended consumers, decision freedoms, current blockers and evidence limits are explicit.
6. The reader can identify whose decision is needed for any material unresolved product question.

If these are not true, label the affected consumption **PARTIAL/BLOCKED** and route the specific gap. Do not require a new Product phase just to record a gap.

## Evidence and completion

- **Product clarification/handoff complete** means the scoped product semantics are durable and approved where required.
- **Cold-read inspection** is an internal source review; **independent fresh-session consumption** requires an actual separate reader and evidence.
- **Design reviewed** does not imply a working backend, successful security controls or production delivery.
- **Delivered product behavior** requires real implementation and meaningful verification; a seeded scenario can support learning but cannot satisfy a missing real dependency.

Capture only necessary source revisions, authority decisions and consumer feedback in the owning project. If a downstream implementation surfaces new evidence that changes product truth, return the affected concern to its Human owner and persist the resulting decision there.
