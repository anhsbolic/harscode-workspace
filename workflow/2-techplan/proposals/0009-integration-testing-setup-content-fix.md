# 0009 — Fix content mismatch in `integration-testing-setup.md`; add real-task examples

**Status:** Proposed
**Date:** 2026-08-27
**Triggered by:** Testing report from account #06 (MFA TOTP) — while validating `proposals/0008`, found `best-practices/go/integration-testing-setup.md`'s actual content is a stray copy-paste of `workflow/5-testing/guidelines.md` (word-for-word, including its "Read the latest implementation report first" process steps), not integration-test-setup guidance at all. `best-practices/index.md`'s row for this file already describes the *intended* topic correctly ("Gate DB-dependent tests behind `//go:build integration`; reserve for constraint/transaction/query-validity checks a fake repo can't prove") — the file body just never matched it. The MFA TOTP report independently surfaced the exact real-world content this file should have had: a transaction-leak bug that exhausted the DB connection pool and hung a test run past a 240 s timeout, plus an orphan test process that then made an unrelated chained `build && vet && test` command time out at 180 s.
**Target area:** best-practices
**Target file(s):**
- `best-practices/go/integration-testing-setup.md` — full replacement (content mismatch fix)
- New: `best-practices/go/examples/integration-testing-setup.md`
- New: `best-practices/go/examples/testing-concurrency.md` (the `-run`-scoping evidence from the same report, distinct enough from the tx-leak finding to warrant its own example entry against a different principle file)
- `best-practices/index.md` — 1 summary-row tweak (snippet below)

## Gap found

Two separate but related things:

1. **Content mismatch, not just a missing file.** `integration-testing-setup.md` currently contains testing-*phase* process guidance (read the implementation report, cover four test categories, verify error responses) — content that already correctly lives in `workflow/5-testing/guidelines.md`. It contains nothing about build tags, DB pool behavior, transaction lifecycle in test helpers, or timeout discipline — the actual subject its own index.md entry promises. Anyone matching on this file's trigger keywords (`integration test, build tag, real database, DATABASE_URL, live Postgres, testcontainers`) gets workflow-phase prose instead of the technical guidance those keywords imply.
2. **Real evidence for what the file should say was just produced.** The MFA TOTP integration suite hung because a test helper called `BeginTx` and never committed or rolled back (`tx, _ := svc.tx.BeginTx(ctx); _ = tx`) — a leaked `pgx.Tx` holds a pooled connection in transaction state, and the next `BeginTx` call blocks forever once the pool is exhausted. Because the run had no explicit `-timeout`, it hung 240+ seconds instead of failing fast with a clear signal. Worse, the hung `account.test` binary stayed alive afterward and silently contended for the same DB connections in a *later, unrelated* chained command, which then also timed out (180 s) for a reason that had nothing to do with what that command was actually testing — a confusing failure mode to debug blind.

## Proposed change

**`integration-testing-setup.md`** — full rewrite to match its own index.md promise:
- Principle: gate DB-dependent tests behind `//go:build integration`, reserve for what a fake/mocked repository genuinely cannot prove (constraint violations, real transaction behavior, concurrent-DB behavior under an actual connection pool) — not a blanket substitute for unit tests.
- New: transaction lifecycle discipline in test helpers — every `BeginTx` needs a guaranteed `Commit`/`Rollback` via `defer`, never a bare `_ = tx`. A leaked transaction is a pool-exhaustion bug that presents as a hang, not an obvious error.
- New: explicit `-timeout` on any DB-backed test run, especially ones involving concurrency — a hang with no timeout blocks the whole run indefinitely instead of failing fast with a stack dump pointing at the stuck call.
- New: orphan process hygiene — after any interrupted/timed-out test run (especially integration/DB-backed), confirm no leftover test binary is still holding connections before running anything else against the same database. An orphaned process contending for the same pool produces misleading, unrelated-looking failures in later commands.
- Bad/Good example lifted directly from the MFA TOTP incident (leaked `tx` vs `defer`-guarded commit/rollback).

**`examples/integration-testing-setup.md`** (new) — real-task entry: the tx-leak → pool-exhaustion → hang → orphan-process chain, with the actual numbers (240 s hang, 180 s unrelated chained-command timeout).

**`examples/testing-concurrency.md`** (new) — real-task entry: the same report's `-race` full-package run at 319 s vs the same tests scoped with `-run 'TestMfa'` at 17 s — concrete evidence for scoping race runs by test name, not just by package, extending what `testing-concurrency.md`'s checklist already says (per `proposals/0008`).

**`index.md`** — minor summary tweak on the existing row (adds the timeout/leak angle, keyword list unchanged since it was already accurate):
```
| go | [go/integration-testing-setup.md](go/integration-testing-setup.md) | integration test, build tag, real database, DATABASE_URL, live Postgres, testcontainers | no | Gate DB-dependent tests behind `//go:build integration`, reserved for constraint/transaction/query-validity checks a fake repo can't prove; guard every test-helper `BeginTx` with a deferred commit/rollback and run with an explicit `-timeout` — an unguarded tx leak presents as a pool-exhaustion hang, not an obvious error |
```

## Rationale

This is a content-correctness fix to an existing, already-cataloged file — squarely inside the root `proposals/` threshold ("an existing file's Bad/Good example turns out wrong, outdated, or contradicted by a real case," extended here to "the file's entire body doesn't match its own index entry"). The example entries are genuinely generic (transaction leak → pool exhaustion is a universal Go/SQL-driver failure mode, not project-specific), sourced from a real incident rather than constructed, and directly complementary to `proposals/0008`'s scoping fix without duplicating it — 0008 is about *when/how narrowly* expensive tests run, this is about *why DB-backed tests specifically hang* and how to fail fast instead.
