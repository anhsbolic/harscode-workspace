# Guidelines

## Source of Truth per Section

PR descriptions are written at the end of the cycle — after techplan.md
exists and after the implementation is done. Don't treat techplan.md as
a single source you copy wholesale; different sections have different
sources of truth:

| Section | Source | Why |
|---|---|---|
| Background | techplan.md § 1 (Background) | Stable — this doesn't change during implementation |
| Solution | techplan.md § 5 (Decision Log) + § 1 | The "why this approach" reasoning is already there, just condense it |
| Changes | **Final diff/commit**, not techplan.md § 10-11 | Implementation Details in techplan is the part most likely to have drifted from what was actually built (see techplan/guardrails.md § 7) |
| Demo | **Final diff/commit + manual verification**, not techplan.md | Must reflect what the code actually does now, not what was planned |

**Rule of thumb: Background and Solution can be condensed from techplan.
Changes and Demo must be verified against the actual diff — never copied
from the plan without cross-checking.**

## When to Include the Changes Section

Include it only if the change touches multiple separate files or points
that a reviewer would otherwise need to hunt for. Signal: 3+ distinct
files/functions, or changes spread across layers (constant + service +
multiple test files).

Omit it if the change is a single conceptual change already fully
explained by Solution — adding Changes in that case is redundant, not
additive.

## Demo Is Not Optional

Demo is the highest-value section for a reviewer — it lets them
understand the impact without reading code. Always write it as a
concrete Before/After, not an abstract description. If the change has
no user-visible or observable-behavior difference (pure refactor), state
that explicitly rather than omitting the section.