# Guidelines

This stage produces the raw docs that live in `docs/story/<story-code>/`
— before techplan synthesis begins. Output here is intentionally
freeform in count and naming: don't force a fixed template onto raw
docs (see `workflow/techplan/guidelines.md` § 1 for why).

The process has three stages. Each stage has a different purpose and a
different rule about whether solutions are allowed to appear yet.

## Stage 1: Plan Announcement (blocking)

Before reading anything, the agent states:
- Which areas it intends to explore
- In what order
- Why that order (dependency, risk, or just logical grouping)

**This is a hard stop.** The agent waits for confirmation before
proceeding to Stage 2. This is the cheapest, highest-leverage point to
redirect — no work has been done yet, so a wrong area or wrong order
costs nothing to fix here versus discovering it three files in.

## Stage 2: Gap Analysis (one area at a time, not blocking between areas)

For each area, in the announced order:

1. Explore that area **fully** before moving to the next. Don't explore
   everything shallowly then write one combined summary — that's where
   detail gets lost. One area, one complete pass, one document.
2. Document, for that area only:
   - **Current state** — what exists today, concretely (not "there's
     some validation logic" but which function, what it actually
     checks)
   - **Requirement** — what the new requirement expects of this area
   - **Gap** — the specific difference between the two
   - **Sniffing findings** — see `sniffing-checklist.md`. This runs on
     every area, not as a separate pass at the end.
3. **Do not propose solutions or options here.** If a fix or approach
   occurs to you while exploring, note it as a bare observation (e.g.
   "possible fix: X" as one line), but do not develop it, compare it
   against alternatives, or write a Decision-Log-shaped section. That
   happens in Stage 3, deliberately later, after the gap itself has been
   reviewed and confirmed accurate.
4. Report progress after each area (not blocking, just visible) so
   there's a natural point to redirect if something looks off — but
   don't wait for explicit go-ahead to continue to the next area unless
   asked to.

## Stage 3: Solutioning (starts only after Stage 2 is reviewed)

Only after the gap analysis has been read and confirmed does trade-off
exploration, option comparison, and Decision-Log-shaped material get
written. This is a separate, later activity — don't let it bleed
backward into Stage 2's output.

## Why the Split Matters

Mixing gap analysis and solutioning in one pass means the agent commits
to a solution frame before its understanding of the current state is
even validated. A wrong or incomplete gap analysis quietly poisons every
option comparison built on top of it. Keeping them separate means a
wrong gap analysis gets caught and fixed *before* any solutioning effort
is spent on top of it.

## What NOT to Do Here

- Don't try to produce something techplan-shaped at this stage — that's
  a separate synthesis step done later.
- Don't hardcode project-specific conventions into the raw docs'
  structure — the codebase's own conventions belong in that repo's own
  convention file, referenced, not duplicated.
- Don't compress Stage 2 output to save space. Detail is the point of
  this stage — compression happens later, during techplan synthesis,
  not here.