# Diagram Guidelines (Mermaid)

Reference for the Summary's optional decision-flow diagram
(`rules.md` § 7). Read this before writing any Mermaid diagram into a
techplan, and re-check against it before finalizing.

## When to include (recap — see rules.md § 7 for the full criteria)

Only when the plan has genuine branching logic, a state transition, or
a multi-step cross-component flow where order matters. Skip for
linear/CRUD plans.

## Correct edge syntax

Flowchart edges MUST use **double-dash** arrows. Single-dash is not
valid Mermaid flowchart syntax and silently fails to render.

| Syntax | Meaning | Valid? |
|---|---|---|
| `A --> B` | solid arrow | ✅ |
| `A -- label --> B` | solid arrow with label | ✅ |
| `A -->|label| B` | solid arrow with label (alt syntax) | ✅ |
| `A -.-> B` | dotted arrow | ✅ |
| `A ==> B` | thick arrow | ✅ |
| `A --- B` | solid line, no arrowhead | ✅ |
| `A -> B` | single-dash | ❌ invalid, fails silently |
| `A - B` | plain dash | ❌ invalid |

## Common mistakes checklist (self-check before finalizing)

- [ ] Every edge uses a double-dash form (`-->`, `-- text -->`, or
      `-->|text|`) — none use a bare single-dash `->`.
- [ ] Node labels with special characters (`==`, `<=`, `>=`, quotes)
      are wrapped in quotes if they cause parse issues, e.g.
      `TD{"expiry <= today"}`.
- [ ] Node IDs are unique and consistent — no reusing one ID for two
      different nodes.
- [ ] Every node referenced in an edge is defined somewhere — no
      dangling references.
- [ ] Diagram direction is declared once at the top (`flowchart TD` or
      `flowchart LR`) — not mixed mid-diagram.
- [ ] Line breaks inside a node label use `<br/>` inside the node's
      bracket, not floating outside it.

## Validation step (mandatory, not optional polish)

Before finalizing a techplan that includes a diagram, re-read every
edge line one at a time and confirm it matches a valid pattern from the
table above. This is a cheap, mechanical check — treat it with the same
seriousness as `guardrails.md` § 5 (Don't Invent Technical Facts). A
diagram with broken syntax is worse than no diagram: it looks
authoritative in the source file but renders as nothing (or a parse
error) for the actual human reader it was written for.

If you can't confirm every edge is valid, simplify the diagram (fewer
branches, plainer arrows) rather than ship something unverified.

## Semantic validation (separate from syntax — do both)

Syntax-valid Mermaid can still be **wrong**. A real example from this
workspace: a branch was labeled `today+14 < expiry < today` — a range
that can never be true (`today+14` is always greater than `today`),
when the actual intended condition (per the plan's own timeline table)
was `today < expiry < today+14`. The diagram rendered fine; it was just
factually inverted.

Before finalizing, cross-check each branch condition in the diagram
against section 4 / the timeline reference table it's illustrating —
line by line, not by re-reading the diagram in isolation:

- [ ] Every inequality direction matches the source table (`<` vs `>`,
      `<=` vs `>=`).
- [ ] Every range condition is actually satisfiable — plug in a
      concrete example date/value and check it lands where the diagram
      says it should.
- [ ] Boundary conditions (`==` cases) are drawn on the side the rules
      actually put them on, not the side that "looks" more natural.
- [ ] No two branches silently overlap or leave a gap the source table
      doesn't have.

A diagram is a restatement of logic that already exists in prose/table
form elsewhere in the plan — treat any mismatch as the diagram being
wrong, not the source table.