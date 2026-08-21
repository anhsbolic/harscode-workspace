# Proposal: Human Digest section at the top of techplan.md

> Status: Accepted
> Date: 2026-08-13
> Triggered by: GMRT-51524 (Daily NIE Expiration Check)
> Target: `template.md` (structure), `rules.md` (new § 7), `guardrails.md`
> (new guardrail), `guidelines.md` (new step), `examples.md` (new
> examples)

## Friction Found

`template.md`'s own note claims section order is intentional: "1-7 for
the lead/team audience (no need to open code), 8-13 for the executor
(precise technical detail)." In practice, on GMRT-51524, section 4
(Rules & Validation) had 18 given/when/then rules with exact boundary
conditions, `TransactionID` formats, and filter predicates — genuinely
execution-grade detail, not something a tech lead skims to approve
scope and direction. The audience boundary comment existed but sat in
the wrong place (between 7 and 8); the actual density jump starts
around section 3-4.

This isn't a one-off formatting complaint — any techplan with a
non-trivial rule set (roughly 6+ rules, or any branching/state-machine
logic) will hit the same problem: the "human section" is unreadable in
practice, but genuinely can't be shortened without losing detail the
execution agent needs. This is structural (affects how every future
techplan is authored), which is why it's a proposal rather than a
one-off manual fix.

## Proposed Change

- Add a **Human Digest** section at the very top of `techplan.md`
  (before section 1), written LAST after sections 1-13 are complete.
  It is a condensation of sections 1 (Background), 2 (Scope), 5
  (Decision Log — chosen option only), 7 (Edge Cases & Risks —
  High-severity only), and Open Items — never an independent draft.
- Include a Mermaid diagram in the digest only when the plan has
  genuine branching logic, a state transition, or a multi-step
  cross-component flow. Skip it for linear/CRUD plans.
- Move the primary audience boundary to sit between the digest and
  section 1. Sections 1-13 stay exactly as detailed as they are today
  — nothing is shortened, the digest is purely additive.
- The digest is one-directional: derived FROM 1-13, never authoritative
  on its own. If it ever disagrees with the full plan, the full plan
  wins and the digest gets regenerated.

## Rationale

A separate "human techplan" + "LLM techplan" as two independent
documents was considered and rejected in the same session — it creates
two sources of truth that can drift silently. A single digest section,
regenerated (not hand-maintained) from what's already decided in
sections 1-13, keeps exactly one source of truth while giving the human
reviewer an actual fast path. This mirrors the workspace's existing
"process vs domain knowledge separation" principle, applied at the
document level instead of the folder level — the digest is *how to read
the plan quickly*, sections 1-13 remain *what is actually decided*.

---

*Reviewed and approved directly with the workspace owner in the same
session that surfaced the friction (GMRT-51524 techplan review) — see
`retro.md` 2026-08-13 entry. Merged into `template.md`, `rules.md`,
`guardrails.md`, `guidelines.md`, `examples.md` in the same batch.*