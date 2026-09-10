# Proposal: Fix `rules.md` § 7/8 and `guidelines.md` step 7 — Still Describe the Embedded-Summary Design Proposal 0012 Removed

> Status: Proposed
> Date: 2026-09-10
> Triggered by: D01-09-autentikasi-admin-pusat (koperasiqu-web-app, backend track) — second occurrence, first logged 2026-09-09 (D01-04-pengaturan-profil, same repo) in `retro.md`
> Target: `workflow/2-techplan/rules.md` § 7 (Summary), § 8 (Open Items Lifecycle); `workflow/2-techplan/guidelines.md` step 7

## Friction Found

`template.md`'s own Structural Note says plainly: the file "has no Summary/digest section and no audience boundary — see Proposal 0012, which supersedes the older embedded-Summary design," and its Open Items section is numbered § 13.

`rules.md` § 7 ("Summary") still describes generating an embedded Summary section "at the top of `template.md`, above the audience boundary" with a full self-check list for it. `rules.md` § 8's prose still says an Open Item must match "the exact same items... as section 14's Active list" — section 14 doesn't exist; Open Items is § 13. `guidelines.md` step 7 still says "Generate the Summary last, after sections 1-13 (and 14, Open Items) are complete" and repeats the § 7 self-check as something to run "before calling this step done."

This is the exact gap already logged in `retro.md` under 2026-09-09 (D01-04-pengaturan-profil), which explicitly said: "if this shows up again, `rules.md` § 7 and `guidelines.md` step 7 need to be updated (via proposal)... and every 'section 14' Open Items reference needs to become 'section 13.'" This session (D01-09, same repo, different task) hit the identical stale text on a fresh read of the guidance folder in the instructed order — meeting the 2+-occurrence threshold for a techplan-protected proposal (`README.md` § Fundamental Rules #4, `guidelines.md` § Proposal Threshold).

Both occurrences avoided producing a broken techplan.md only because the agent happened to read `template.md` closely enough to notice its Structural Note's explicit "supersedes" language before trusting `rules.md`/`guidelines.md`'s stale prose. That's not a guaranteed mitigation — a different read order, or a skim of `template.md`, would reproduce the bug this fix prevents.

## Proposed Change

**`rules.md` § 7** — replace the entire "Summary" section (the generation/condensation rules, the Include/Exclude lists, the diagram criteria, the self-check list) with a short pointer to `report-template.md`/`report-techplan.md`:

> ## 7. Summary — Generated Separately, After Approval
>
> `techplan.md` itself has no embedded Summary/digest section (Proposal 0012 superseded that design — see `template.md`'s Structural Note). Once a techplan reaches **Approved** status, generate `report-techplan.md` from `report-template.md` instead — that file draws from this document's sections 1, 2, 5, 7, and 13 (Open Items), condensed for a reviewer. See `report-template.md` for the condensation rules, Include/Exclude lists, diagram criteria, and self-check that used to live in this section.

**`rules.md` § 8** — change "the exact same items... as section 14's Active list in the full plan" to "as section 13's Active list in the full plan" (only the section number is stale; the rest of § 8's content about Open Items Lifecycle is otherwise still accurate for `techplan.md` itself).

**`guidelines.md` step 7** — replace:

> 7. **Generate the Summary last, after sections 1-13 (and 14, Open Items) are complete.** Condense per `rules.md` § 7 — ...

with:

> 7. **`techplan.md` itself ends at section 13 (Open Items) — there is no Summary/digest step here.** Once the techplan reaches Approved status, generate `report-techplan.md` from `report-template.md` separately (see that file's own generation checklist) — don't fold Summary generation into this synthesis pass.

## Rationale

Two independent sessions, same repo, different tasks, both hit this on a fresh read — meeting the workspace's own recurrence bar for a proposal rather than a one-off retro note. The fix is mechanical (delete stale content, point at the doc that actually owns it now, fix one wrong section number) and removes a trap that currently depends on an agent noticing a Structural Note buried in `template.md` rather than trusting the two files whose entire job is to state the process accurately.

---

*After human review: update the Status above. If Accepted, merge into the target document and leave this proposal in place (don't delete it) — it serves as the only changelog since this folder isn't git-tracked as its own repo.*
