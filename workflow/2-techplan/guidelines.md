# Guidelines

Step-by-step process for synthesizing raw docs into techplan.md.

## Process

1. **Read every file** in `docs/story/<story-code>/`. Don't assume a
   fixed count or specific file names — treat everything as raw
   material, scan the content, not the filenames.

2. **Classify each piece of content by function**, using the mapping
   table in `rules.md` § 1. A single file can contribute to many
   sections at once (e.g. one exploration doc can have an executive
   summary for Background, a trade-off table for Decision Log, and a
   risk table for Edge Cases — all in one file).

3. **Dedupe overlaps/conflicts** between raw docs — follow
   `rules.md` § 2. Don't just take whichever doc you read first.

4. **Evaluate independent operational sub-components** (one-time
   script, cron, separate migration) — whether to fold them into the
   same techplan or make them a separate linked document. See
   `rules.md` § 3.

5. **Read the target repo's convention** (AGENTS.md/README in the
   destination service, NOT in this guidance folder) before filling in
   section 8, Interface Contract. See `guardrails.md` § 4.

6. **Write techplan.md** to `docs/story/<story-code>/techplan.md`
   following `template.md`. Calibrate tone and level of detail using
   `examples.md`.

7. **Generate the Summary last**, after sections 1-13 (and 14, Open
   Items) are complete. Condense per `rules.md` § 7 — don't write it as
   an independent draft, and don't introduce anything not already
   decided in sections 1-13 (`guardrails.md` § Summary Must Not
   Introduce New Decisions). Include a diagram only if the plan meets
   the branching/state-transition/multi-step-flow criteria in
   `rules.md` § 7 — and if you do, validate every edge for both syntax
   AND semantics against `diagram-guidelines.md` before finalizing
   (`guardrails.md` § 9). Run the full self-check in `rules.md` § 7
   before calling this step done — severity check, diagram semantic
   check, and Open Items sync check are not optional.

8. **Check retro.md** before finishing — if there's a relevant lesson
   for this story (e.g. a similar dedup case from before), apply it.

9. **If you find a structural gap in this guidance**, write a proposal
   (see Proposal Threshold below), don't edit the guidance directly
   (`guardrails.md` § 1).

10. **If you're revising an existing techplan mid-Draft** (not a fresh
    synthesis) and an Active Open Item has been resolved since the last
    pass, move it to Resolved with the resolution recorded
    (`rules.md` § 8, `guardrails.md` § 10) and regenerate the Summary
    in the same edit (`guardrails.md` § 11) — don't leave that for the
    next full synthesis pass.

11. **When populating section 12 (Testing Checklist), also populate the
    Test Focus Pointer table** (`rules.md` § 9) by cross-referencing the
    raw exploration docs' Sniffing Checklist Risk findings for this
    story. Don't silently drop a flagged area — mark it N/A with a
    reason if it didn't survive synthesis (`guardrails.md` § 12).

## Proposal Threshold

Write a proposal ONLY if:
- The same friction shows up across 2+ different stories, OR
- The gap is genuinely structural (changes a way of working/principle,
  not just a minor detail)

Example that DOES warrant a proposal: "the backfill-plan is genuinely a
different genre from a normal techplan, rules.md needs a new section on
Runbook vs Techplan" — this is structural, it affects decisions in other
stories too.

Example that does NOT warrant a proposal: "the section heading isn't
quite right for this case" — that's a one-off, just fix it manually
while writing that techplan, no need for a formal proposal.

For lighter-weight things (finding a good example, or a small lesson
that's still worth noting but isn't a rule change) — append directly to
`examples.md` or `retro.md`, no proposal process needed.