# Experience Specialist — Agent-Owned Best Practices

Applied local knowledge for designing a consumable **experience contract**, not a general UI component cookbook.

## Truthful interaction states

- List only meaningful states required to honor current product acceptance, but include pending, invalid/unattributed, incomplete, known conflict, denied, unavailable and retry paths when relevant.
- Make irreversible/consequential action meaning clear *before* effect at the specific decision point when required by authority. A decorative warning after success is not equivalent.
- A success surface must correspond to the system-authoritative success condition, not the client believing an HTTP request was sent.
- Durable user-facing meaning requires a later inspection path when the original obligation requires it; transient toast alone cannot satisfy that property.
- Distinguish provenance class (user/Organization-provided) from independent verification or curation; avoid status badges or words that imply unsupported trust.

## Interaction/API consistency

- For each material UI state, identify its server/API authority, required data, response/error category and how stale/unknown/partial data is presented.
- Avoid separate client-owned truth for server-authoritative role or establishment state.
- Unauthorized client view may be a UX concern; server-side permission remains the enforcement owner.
- Requirements for accessibility and responsive behavior may flow from project design authority, but visual/pixel validation belongs to real rendered verification, not solution design.

## Context usage

Use local knowledge and current applicable project `docs/ui-ux/` authority. No mandatory global Best Practices index. If framework-specific implementation detail appears, leave it to the Next.js/other frontend producer unless it changes O2/O3 contract.
