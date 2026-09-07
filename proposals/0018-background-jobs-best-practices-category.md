# New category: background-jobs/

**Status:** Proposed
**Date:** 2026-09-07
**Protection Tier:** general
**Triggered by:** locking the scheduled-job design for a monthly batch calculation on a new project, surfacing a locking/idempotency pattern that doesn't fit any existing category
**Target area:** best-practices
**Target file(s):**
- `best-practices/background-jobs/idempotent-scheduled-jobs.md` — new file
- `best-practices/index.md` — new `background-jobs` category row

## Gap found

`kafka/` and `pubsub/` exist but are both scoped to event-streaming delivery semantics (offsets, acks, ordering, dead-letter). Neither covers the much more common case of a periodic/scheduled batch job (cron-style, framework scheduler, or an external scheduler triggering an HTTP/CLI entrypoint) that computes something over a time window and must not run twice for the same window. Concretely: a scheduler misfire, an overlapping retry, or a manual re-trigger during an incident can all cause the same job execution to run concurrently or a second time — and a batch job that mutates balances/statuses based on "did I already process this period" is exactly the kind of thing that silently double-processes if idempotency isn't designed in from the start, at the database level, not just at the scheduler level.

## Proposed change

Add a new `best-practices/background-jobs/` folder with one file (full content below), plus a new row in `best-practices/index.md`.

### `index.md` addition

New row in the main trigger-keyword table:

| Category | File | Trigger keywords | Security-critical | Summary |
|---|---|---|---|---|
| background-jobs | [background-jobs/idempotent-scheduled-jobs.md](background-jobs/idempotent-scheduled-jobs.md) | scheduled job, cron, batch job, withoutOverlapping, idempotent job, double-run, partial failure | no | Application-level "don't overlap" locking on a scheduler is not sufficient alone; pair it with a database-level uniqueness constraint per period, and design for safe resume after partial failure |

No Security Concern Map entry — this is a correctness/reliability concern (double-processing), not itself an authn/authz/PII/injection concern; if a specific job touches money or PII, that's already covered by the relevant domain file (e.g. `postgresql/financial-invariant-enforcement.md`), cross-referenced from the new file.

### New file

See attached file content (`idempotent-scheduled-jobs.md`) — full text ready to paste into `best-practices/background-jobs/`.

## Rationale

The principle is framework- and language-agnostic: it applies equally to a cron job, a framework scheduler (Laravel Scheduler, Celery beat, etc.), or an external orchestrator triggering a batch entrypoint — none of the guidance is tied to a specific scheduler's API beyond an illustrative example. It's a distinct concern from `kafka/`/`pubsub/` (message-delivery idempotency) and from `postgresql/transactions-and-locking.md` (general locking mechanics) — this file is specifically about the "did this scheduled unit of work already run for this period" problem, which needs both an application-level overlap guard *and* a database-level uniqueness constraint as a second, independent line of defense, a combination worth stating explicitly since either one alone is insufficient.

---

*After human review: update the Status above. If Accepted, merge into
the target document and leave this proposal in place (don't delete
it) — it serves as this folder's changelog. See `proposals/README.md`
for the Protection Tier distinction and numbering convention.*
