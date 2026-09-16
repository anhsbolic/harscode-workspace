# Product Design

`product-design/` is Harscode's upstream product-to-engineering guidance.

Use it when a product needs deliberate product-brand, UI/UX, visual-system, or design-authority work **before** engineering can safely establish implementation precedent.

This area is not a design trend library and does not prescribe one aesthetic. It documents reusable decision discipline for moving from product truth to implementation-ready design authority.

## Where this fits

```text
product/domain truth
→ product-design/
→ workflow/1-exploration
→ workflow/2-techplan
→ build / review / testing / PR
```

The boundary is deliberate:

- product/domain sources own what the product means;
- `product-design/` owns how product intent becomes coherent design authority;
- `workflow/` owns how engineering work is explored, planned, implemented, reviewed, and verified;
- `best-practices/` owns reusable technical knowledge.

Not every feature needs a fresh product-design cycle. Use this guidance when brand/product-UI intent is materially open, when a new design generation is being established, when legacy design authority conflicts, or when design readiness is unclear.

## Guidance map

| Concern | Read |
|---|---|
| Establish product-brand/UI direction from product truth | `product-brand-and-ui-exploration.md` |
| Promote approved exploration into one clean active authority | `design-authority-and-canonicalization.md` |
| Move approved design authority into engineering without redesigning in code | `design-to-engineering-handoff.md` |

## Core model

A healthy upstream cycle normally looks like:

```text
product truth + user needs
→ product posture
→ competing creative directions
→ human selection / synthesis
→ representative visual proofs
→ concrete design-system decisions
→ canonicalization
→ engineering interpretation
```

The exact artifacts are project-specific. The decision order is the reusable part.

## Hard boundaries

- Product/domain truth outranks design artifacts.
- Visual references do not create business semantics.
- Existing implementation is evidence of current state, not automatic design authority.
- Generated visual studies are evidence only to the extent explicitly approved.
- Brand-defining decisions require a human gate when the project treats them as durable identity/product precedent.
- Materially OPEN design decisions must not be silently resolved inside implementation.

## Human authority and change governance

The files in `product-design/` are shared Harscode guidance, not project-specific design docs.

Agents may read and apply them. Changes to this guidance should go through the root `proposals/` mechanism and human review rather than being silently rewritten during project work.

Project-specific design authority belongs in the target project's own documentation, not here.
