# Proposal 0005 — Split `template.md` into Agent-only `techplan.md` + Mandatory `report-techplan.md`

**Status:** Draft (pending owner review/merge) · **Date:** 2026-08-27 · **Triggered by:** GMRT-51542 + owner-asserted recurring single-document inefficiency (see caveat)

**Supersedes:** Proposal 0001's embedded-Summary design (Summary section is removed from `techplan.md`, not just condensed).
**Folds in:** Proposal 0004 (`report-techplan.md` becomes the mandatory report artifact, not an optional additive superset — 0004 can be marked Superseded once this merges).

---

## Friction found

`template.md` has served two audiences in one document since it was created: the implementing agent/engineer (needs execution-grade rules, file/line pointers, full code) and the human reviewer (needs to understand and sign off, not implement). Proposal 0001 mitigated this with an embedded Summary section + audience boundary — but didn't eliminate the redundancy:

1. Decisions, risks, and scope end up explained **twice in the same file** — once in full (Decision Log, Edge Cases & Risks) and again, paraphrased, in Summary. Working through GMRT-51542 end to end made this concrete: nearly every Summary bullet was a shortened restatement of a section further down.
2. A reviewer who only needs to sign off still opens a document containing code, file paths, and line numbers to get to the two paragraphs relevant to them.
3. Owner reports this is not a one-off observation from this story alone — the single-document format has caused recurring process inefficiency across prior techplans, independent of the Summary-drift issues proposals 0002/0003 already fixed.

This is judged **genuinely structural** (per `guidelines.md`'s proposal threshold — either 2+ stories or a structural gap): the redundancy is inherent to serving two audiences from one document, not a compliance gap that a checklist can fix (which is what 0002/0003 were).

## Decision

Split into two protected templates, each with exactly one audience and one owner of content:

1. **`template.md` → `techplan.md`** (unchanged file name, changed shape): **Agent-only.** Remove the Summary section and the audience-boundary comment entirely. Every section is execution-grade — for the implementing agent, the engineer, and code review. No content is written specifically "for a reviewer" anymore; that job moves entirely to the second document.

2. **`report-template.md` → `report-techplan.md`** (new, mandatory): **The sole human-facing artifact.** Sourced entirely from the approved `techplan.md` — Background/Scope condensed, Decision Log condensed to plain-language "why," Top (High-severity only) Risks, Open Items needing a decision — **plus** two sections validated during GMRT-51542 that Summary never covered: a simplified Architecture/Plan (diagram only if the flow has genuine branching — same rule already in `guidelines.md`) and a simplified Interface Contract with representative JSON examples, when the story has an external-facing interface.

**Sequencing rule (carried over from Proposal 0004, now enforced, not optional):**
- `report-techplan.md` is generated **only after** `techplan.md` reaches `Approved` status. Never drafted in parallel with an in-progress techplan.
- If `techplan.md` changes after `report-techplan.md` was generated — including the Approved→Implemented loop, or a reopened Draft — `report-techplan.md` **must be regenerated in full** before it's considered current. No hand-patching a paragraph to match; regenerate the whole file from the current techplan.

This sequencing is what makes the split safe: it's the same "single source, regenerate rather than hand-maintain" principle Proposal 0001 already used for Summary, just applied across two files instead of within one.

## Rule/guardrail migration

Proposals 0001-0003 built real machinery around the in-file Summary. That machinery needs a new home, not a deletion:

| Existing rule | Current target | New target |
|---|---|---|
| `rules.md` §7 — Summary self-check (severity re-check, diagram semantic re-check, Open Items sync, testing-checklist count-check) | Summary section in `techplan.md` | Becomes `report-template.md`'s own generation checklist — same four checks, run when generating `report-techplan.md` instead of when finalizing an in-file section. |
| `guardrails.md` §9 — diagram syntax + semantic validation | Any diagram in `techplan.md` | **Unchanged, and now also applies to `report-techplan.md`'s diagram** if one is included — both are validated independently, since they may differ (report's is simplified, techplan's — if it has one — is full detail). |
| `guardrails.md` §10 — resolved items must be recorded, not deleted | Open Items section in `techplan.md` | **Unchanged** — this was never about Summary, stays exactly where it is. |
| `guardrails.md` §11 — Summary must stay in sync with the plan, including mid-Draft edits | In-file Summary vs. rest of `techplan.md` | **Retargeted**: `report-techplan.md` must be regenerated whenever `techplan.md` changes post-generation. Arguably stronger than before — regenerating the whole file avoids the exact failure mode that caused the original gap (a partial, in-place edit missing a sub-part). |
| *(new)* | — | **New guardrail**: do not generate or hand-edit `report-techplan.md` while the source `techplan.md` is not yet `Approved`. |

## Rejected alternative

**Keep Summary embedded in `techplan.md` AND add `report-techplan.md` as a pure additive superset** (Proposal 0004's original framing). Rejected now: it reproduces the exact redundancy that triggered this proposal — background/decisions/risks would be written out in full in `techplan.md`'s Decision Log, paraphrased again in `techplan.md`'s Summary, and paraphrased a third time in `report-techplan.md`. Cleaner to have exactly one file own human-facing content.

## Caveat — evidence strength

Documented evidence is one story (GMRT-51542). The "recurring inefficiency across prior techplans" claim is owner-asserted from experience, not logged in `retro.md` with specific instances. Recommend that the next 1-2 techplans built under this new format get a retro note if the split does or doesn't hold up in practice — particularly whether reviewers ever want to see architecture *before* a techplan is Approved, which would conflict with the post-Approval-only generation rule this proposal depends on.

## Targets

- `template.md` — remove Summary section and audience-boundary comment; section numbering 1-14 unaffected (Summary was never a numbered section).
- `report-template.md` — update from Proposal 0004's draft: remove "optional/additive" framing, make explicit this is the sole and mandatory human artifact, sourced directly from `techplan.md` (not from an in-file Summary that no longer exists).
- `rules.md` — relocate §7 (Summary self-check) into `report-template.md`'s own checklist; mark old §7 as moved, not deleted (retro trail).
- `guardrails.md` — retarget §11; add new pre-Approval generation guardrail; §9-10 otherwise unchanged per table above.
- `proposal-index.md` / retro equivalent — mark Proposal 0004 as **Superseded by 0005**.