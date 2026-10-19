# S1 Generic Input Contract — Proposed

## Required input envelope

| ID | Required semantic input | Conformance / provenance |
| --- | --- | --- |
| I1 | Approved, bounded behavior/requirements and original acceptance obligations | Inspectable owning source, approved status, scope, revision; distinguish product authority from navigation/evidence |
| I2 | Current project/design/architecture/security constraints | Applicable source + revision, precedence and protected-write/permission rules; technology choices are project binding, not generic Space policy |
| I3 | Target repository and current implementation baseline | Exact repository, branch/ref and target SHA (or immutable equivalent); read access, known active contracts and environment facts |
| I4 | **Human-direct** invocation assignment, consumers and scoped authorization | Exact Human-approved objective, required output/state destinations, downstream consumer expectations, allowed actions and material Human gates, selected mode (`supervised` unless explicit Human `autonomous`), authority and decision evidence; actual runtime suitability is separately checked against execution requirements |

Optional: supporting research and examples that are clearly marked non-authoritative; dependencies or real prior output from another approved Space; relevant live technical evidence. Do not require a fixed PRD/TRD format or a pre-existing API.

## Acceptance and refusal

The Space checks existence, provenance, ownership and cross-input consistency **for the Human-direct received assignment**; Balad may provide prior upstream composition **advice to the Human**, but does not invoke or coordinate S1 and does not delegate product-quality judgment as a mandatory re-audit. Reject/hold if material authority is missing, the target revision is ambiguous, inputs conflict about binding product meaning, an expected consumer cannot be identified, or required access/permission is absent. Record the exact gap instead of inventing missing semantics.

**Design freedom** (auth implementation, route shape, database schema, detailed state representation) is not itself missing Product Authority. Produce a reasoned solution within project-owned constraints, and escalate only decisions actually owned by Human or material risk gates.

## First pilot binding (external, not reusable content)

Kencleng C1 binds Stage 5/6 approved requirements, Stage 7 navigation, root/scoped `AGENTS.md`, relevant `docs/ui-ux/` and `docs/project/`, and current clean-baseline tree. C1 product rules, branch SHA, solution choices and artifact destinations belong to its actual invocation input, **not this file**. Historical C1 solution/Techplans/old code are excluded as routine initial authority per pilot entry.

## Do not assume

- The existence of a formed downstream Space, concrete consumer contract, initialized state directory, configured or authorized Specialist execution, or permission to edit a shared project contract solely because Harscode guidance describes them.
- A model's nominal capability, approved formation or historical successful engineering flow proves runtime competence.
