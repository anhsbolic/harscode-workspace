# Retro

Living log. Each entry: what happened, why it was a problem, how it was
mitigated. Keep appending, don't delete (even once "solved" — the
history still has value).

---

## 2026-07-30 — Duplicate content across raw docs (GMRT-50941)

**What happened:** `implementation-plan.md` and
`registrar-migration-plan.md` both rewrote the same migration SQL, model
field, and service mapping. `registrar-migration-plan.md` was more
detailed (had specific line numbers, a current-state ✓/❌ checklist).

**Why it was a problem:** If content is taken from whichever file was
read first without comparison, you can end up with the less precise
version without realizing it.

**Mitigation:** Added `rules.md` § 2 (Dedup & Reconciliation) —
prioritize the most specific and most recent version, note it as an open
question if it's a genuine conflict (not just a difference in level of
detail).

---

## 2026-07-30 — Sub-component with a different-genre operational lifecycle (GMRT-50941)

**What happened:** `registrar-backfill-plan.md` had its own rollback,
cleanup checklist, execution order, and duration estimate — a different
genre from a techplan (it's a runbook, not a system-behavior spec).

**Why it was a problem:** If forced into a section of the main
techplan, the document gets bloated and mixes two genres (behavior
contract vs one-time execution procedure) into one file.

**Mitigation:** Added `rules.md` § 3 (Runbook vs Techplan) + an example
in `examples.md`.

---

## 2026-08-13 — Sections 1-7 weren't actually "human-readable" despite the label (GMRT-51524)

**What happened:** `template.md`'s own note claimed sections 1-7 are for
"the lead/team audience (no need to open code)." In practice, section 4
(Rules & Validation) for GMRT-51524 had 18 given/when/then rules with
exact boundary conditions and `TransactionID` formats — execution-grade
detail, not something a tech lead skims to approve scope.

**Why it was a problem:** the audience boundary comment existed but was
placed in the wrong spot (between 7 and 8) — the actual density gap
starts around section 3-4, not section 8. A tech lead reviewing the
plan for approval had to wade through rule-by-rule detail meant for the
execution agent.

**Mitigation:** added a Human Digest section at the very top of
`template.md` (`rules.md` § 7, `guardrails.md` § 8), generated last by
condensing sections 1, 2, 5, 7, and Open Items. The audience boundary
moved to sit between the digest and section 1. Sections 1-13 stay
exactly as detailed as before — nothing lost, just no longer mistaken
for the human-facing part. See `proposals/0001-human-digest-section.md`
for the full rationale.

---

## 2026-08-13 — First real-world digest from another model surfaced three gaps (GMRT-51524, second pass)

**What happened:** A different model regenerated the GMRT-51524
techplan under the new Human Digest guidance. Review found: (1) the
digest's Mermaid diagram used single-dash edges (`->`) on three lines —
invalid syntax, fails to render silently; (2) the digest included a
handful of parenthetical rule-ID references (e.g. "(R18)"), which
`rules.md` § 7 said to exclude entirely, but on review these read as
genuinely useful, not noisy; (3) the digest's Top Risks table included
one Medium-severity row alongside High-severity ones, against the
"High-severity only" instruction.

**Why it was a problem:** (1) is a silent failure mode — nothing in the
guidance would have caught a broken diagram before it shipped. (2)
revealed the original rule was stricter than useful once tested against
a real generated example. (3) was a plain compliance gap, not a sign
the rule was wrong.

**Mitigation:** added `diagram-guidelines.md` (Mermaid syntax reference
+ mandatory pre-finalize checklist) and `guardrails.md` § 9 to make
diagram syntax a hard-checked guardrail. Relaxed `rules.md` § 7's
rule-ID exclusion to allow parenthetical cross-references while still
banning full rule-by-rule tables. Left the severity-filtering
instruction as strict as written — that gap gets fixed by enforcement,
not by changing the rule. See
`proposals/0002-digest-diagram-and-rule-id-refinement.md`.

---

## 2026-08-13 — Same gaps recurred a third time; enforcement needed a checklist, not just prose (GMRT-51524, third pass)

**What happened:** A third pass at the GMRT-51524 techplan (a manual
edit by the workspace owner, after two model-generated passes) still
had: the testing checklist missing R18 (the same gap as pass one, which
pass two had actually caught and fixed); two Medium-severity risks in
Top Risks instead of High-only; a diagram branch with an inverted range
condition (`today+14 < expiry < today`, which can never be true) that
passed Mermaid syntax validation cleanly. Separately, during review the
owner confirmed 3 of 4 Open Items were already resolved, but the
Summary at the top of the same file still listed all 4 as active — the
full plan and the Summary had drifted out of sync mid-edit.

**Why it was a problem:** the rules already existed for all four issues
(severity filter, testing checklist traceability, diagram syntax
validation, Summary-is-derived-one-directionally) — restating them in
prose a third time wasn't going to fix a compliance gap that survived
two prior passes. The Open Items desync also exposed a real hole: the
existing guardrail for "don't silently change a locked contract" only
covered Approved/Implemented status, not a Draft being edited
iteratively.

**Mitigation:** converted the relevant rules into an explicit
self-check list in `rules.md` § 7 (run before calling the Summary
done) instead of leaving them as prose to remember. Added
`rules.md` § 8 (Open Items Lifecycle) and `guardrails.md` § 10-11 to
cover resolution/sync at any status, not just Approved/Implemented.
Extended the diagram guardrail (`guardrails.md` § 9,
`diagram-guidelines.md`) to require a semantic check against the
source table, not just Mermaid syntax. Also renamed "Human Digest" to
"Summary" throughout (owner preference, confirmed intentional) and
formalized Open Items as `template.md` section 14 — it had been an
informal, undocumented convention until now. See
`proposals/0003-summary-rename-and-open-items-lifecycle.md`.

---

## 2026-09-09 — `rules.md` § 7 and `guidelines.md` step 7 still describe the embedded-Summary design Proposal 0012 already removed (D01-04-pengaturan-profil, koperasiqu-web-app)

**What happened:** Read the guidance folder in the instructed order
(README, template, rules, guardrails, guidelines, examples, retro) for
a fresh techplan synthesis. `template.md`'s own Structural Note says
plainly that the file "has no Summary/digest section and no audience
boundary — see Proposal 0012, which supersedes the older
embedded-Summary design," and its Open Items section is numbered § 13,
not § 14. But `rules.md` § 7 ("Summary") and § 8 ("Open Items
Lifecycle" — the section number 8 is fine, but its prose points at
"the exact same items... as section 14's Active list") and
`guidelines.md` step 7 ("Generate the Summary last, after sections
1-13... are complete") still describe generating an embedded Summary
section and reference "section 14" for Open Items — both stale
relative to what `template.md` actually specifies today.

**Why it was a problem:** an agent that reads `rules.md`/`guidelines.md`
before `template.md`, or that skims rather than reads `template.md`'s
Structural Note carefully, would try to write a Summary section into
`techplan.md` itself and use the wrong Open Items section number —
directly contradicting the current template. This session avoided it
only because the read order happened to hit `template.md` first and
its Structural Note was read closely enough to notice the explicit
"supersedes" language.

**Mitigation:** no rule change made this pass (this is exactly the
kind of gap `guidelines.md`'s Proposal Threshold says to log here
first, not immediately propose a fix for — one occurrence, not yet
2+ stories). Noting it so a second occurrence is recognized as the
same root cause rather than rediscovered from scratch: if this shows
up again, `rules.md` § 7 and `guidelines.md` step 7 need to be
updated (via proposal) to point at `report-template.md`/
`report-techplan.md` instead of describing an embedded Summary, and
every "section 14" Open Items reference needs to become "section 13."

**Update, 2026-09-10 (D01-09-autentikasi-admin-pusat, same repo):**
second occurrence, exactly as predicted above — a fresh techplan
synthesis for a different task in the same repo hit the identical
stale `rules.md` § 7/8 and `guidelines.md` step 7 text on the
instructed read order. Threshold met; filed
`proposals/0023-rules-and-guidelines-stale-summary-references.md`.

---

## 2026-09-10 — A short AGENTS.md golden-rule summary undersold a fuller convention doc it pointed at, and the exploration phase didn't read the fuller doc (D01-09-autentikasi-admin-pusat, koperasiqu-web-app)

**What happened:** The target repo's `AGENTS.md` states a golden rule
in one line: any domain needing to trigger a notification before
Domain 8 is built must use the `NotificationDispatcher` contract.
Exploration (Stage 2/3, a separate raw-doc-producing phase before this
techplan) read that one line, found it contradicted by already-shipped
code for the closest analogous flow (a set-password-link email sent via
Laravel's native `->notify()`, bypassing the contract entirely), and
recorded a decision — confirmed by the human — to "follow the golden
rule" for this task's new email, without ever opening the fuller
document `AGENTS.md` itself points at
(`.agents/knowledge/architecture/notification-stub-contract.md`).

While filling in this techplan's Interface Contract/Implementation
Details (where the actual mechanics of "how does dispatch() cause an
email to send" had to be specified concretely), reading that fuller doc
in full revealed two things the one-line summary didn't convey: (1) its
own scope is explicitly Domain 8's N1-N26 business-event catalog, not
core per-domain auth mail — its own worked examples are cross-domain
business events ("reassignment Stokis, reaktivasi Anggota"), not
transactional credential emails; (2) its current bound implementation
is a pure log-only stub that **explicitly does not send real email
until Domain 8** — using it for this task's email would have silently
produced zero real email sent, breaking the feature's own acceptance
criterion, while looking "compliant" with the golden rule's one-line
text.

**Why it was a problem:** a human-confirmed decision, made in good
faith from the one-line convention summary, turned out to be based on
incomplete information — and nothing in the raw exploration docs flagged
that the summary might not be the full story. The techplan-synthesis
guardrail that caught it (`guardrails.md` § 4, "read the target
convention first") is scoped to "before filling in section 8"; this
case shows the same principle applies just as much to *any* golden-rule
line an exploration phase treats as sufficient on its own, whenever
that line points at a fuller doc by name.

**Mitigation:** no rule change proposed this pass — this looks like a
single incident (one convention doc, one repo) rather than a recurring
or structural gap in this guidance folder itself; the existing
`guardrails.md` § 4 principle already covers it in spirit, it just
wasn't triggered early enough. Logging the pattern for now: when a raw
exploration doc records a decision resting on a short rule/summary line
that itself names a fuller doc ("see `X.md`" / "per `Y.md`"), techplan
synthesis should open that fuller doc before treating the exploration
doc's recorded decision as final — not just before filling in section 8
specifically — and should be prepared to flag a correction (Decision
Log + Open Item, not a silent override) if the fuller doc changes the
picture. If this exact shape (a golden-rule summary undermining a
recorded decision once the doc it points at is actually read) recurs on
a different repo/convention doc, that's the signal to promote this into
an explicit `guardrails.md` addition.

---

## 2026-09-10 — A raw exploration doc's "no contract exists yet" claim was wrong; the contract existed but was stale (D01-06-assignment-stokis-penanggung-jawab, koperasiqu-web-app)

**What happened:** The raw exploration docs for this task asserted, based on the feature spec's own "detail endpoint diturunkan ke api/openapi/... setelah dokumen ini dikonfirmasi" scope note, that no OpenAPI contract existed yet for this feature — and a Decision Log entry (route vocabulary: English `members`/`stockist`, confirmed by the human) was made on that basis. While filling in this techplan's Interface Contract (`guardrails.md` § 4, "read the target convention first"), the actual OpenAPI file was opened directly and turned out to already have a fully-drafted section for this exact feature — using a *different*, Indonesian-vocabulary route/field naming (`/admin/anggota/{anggota_id}/stokis`, `stokis_id_baru`) that directly contradicted the human-confirmed decision. Reading the OpenAPI file's own header note resolved this cleanly: it explicitly documented that earlier-numbered feature sections had already been rewritten to match actually-shipped code, while later ones (including this task's) still carried old, pre-shipped-code placeholder text meant to be revised "once that domain starts being built" — i.e. now.

**Why it was a problem:** the raw exploration doc's claim ("no contract exists") was taken as settled fact and used as the basis for a human-confirmed decision, without anyone actually opening the contract file to check. Had the techplan stage also skipped opening it (e.g. trusted the raw doc's claim without independent verification, since `guardrails.md` § 4 is about reading the *target repo's convention file*, and it's easy to read that narrowly as "the AGENTS.md-style convention doc" rather than "any contract file the Interface Contract section might need"), this techplan would have built against a genuinely different, wrong wire contract — a much harder mistake to catch after code review than during synthesis.

**Mitigation:** no rule change proposed this pass — this looks like a one-off gap in how thoroughly the *exploration* phase (a separate, earlier phase from techplan synthesis) verified an absence claim, not a structural gap in the techplan guidance itself. Logging the pattern: when a raw exploration doc asserts "X doesn't exist yet" as the basis for a naming/contract decision, and the techplan stage is about to fill in Interface Contract detail for that same X, actively search for X (by feature name/domain, not just by the path the raw doc already checked) before trusting the absence claim — an OpenAPI/contract file can exist under a domain-level filename covering many features, with per-feature sections at very different states of freshness, so "the file exists" and "this feature's section in it is current" are two different facts that both need checking. If this shape (a raw doc's negative claim about a shared multi-feature file turning out wrong, once the techplan stage actually opens that file) recurs on a different repo, promote it into an explicit `guardrails.md` addition alongside § 4.