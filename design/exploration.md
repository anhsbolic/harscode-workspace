# Design Exploration — Interaction and Expression

> **Status:** WORKING / RESEARCH-ONLY. Reusable guidance, not target-project design authority.

## Entry

Use when a material interaction, information hierarchy, brand expression, visual precedent or accessibility behavior remains unresolved. Start with **the approved Product experience**: actor, context, meaning of actions, consequences, uncertainty, success and failure. If any material Product meaning is missing, return it to the Product owner; Design must not invent it.

## Deliberate design work

1. **Locate constraints.** Read only the applicable project product/design sources; distinguish locked decision, working candidate, evidence and unknown.
2. **Frame the human problem.** What must the person notice, understand, decide, or recover from? Which mistaken inference would harm correctness or trust?
3. **Choose the open design concern.** Interaction sequence, content priority, visual expression or brand character may be open independently. Do not reopen settled concerns by default.
4. **Explore proportionately.** Compare meaningfully distinct directions where choice matters; otherwise make a local candidate. State trade-offs, especially when persuasion could outpace evidence.
5. **Use representative proofs.** Prototypes, rendered UI, contrast examples and accessibility checks should answer a concrete question. Their scope, source data, assumptions and approval status must be clear. No seeded mock proves backend behavior or external legitimacy.
6. **Converge through Human judgment.** Record what is approved, what remains open and which proof supports it. Do not prolong exploration after evidence is sufficient.

## Truthful expression

- Distinguish actor-provided, reviewed, verified, inferred, pending, failed and unavailable information whenever the underlying Product semantics require those distinctions.
- Provide understandable pre-effect consequence information for material actions; design treatment does not replace authorization.
- Make success, incomplete, uncertain, conflict, and recovery states distinguishable when relevant to the accepted experience. Never label a network timeout as a confirmed failure or success without evidence.
- Preserve keyboard, screen-reader and non-color-only communication; responsive layouts must preserve priority, not pixel coordinates.
- Avoid celebratory, institutional or urgent visuals that imply proof, status or progress the product does not possess.
- Design-system abstraction follows recurring semantic use, not visual similarity alone.

## Stop or hand off

A design direction is mature enough for review when relevant experience constraints are preserved, important states are covered, representative evidence is inspectable, trade-offs and open decisions are explicit, and the Human can approve the bounded concern without hidden Product guesses. Exact artifact shape belongs to the owning project.
