# go/examples.md

> Real-world references for files in `go/`. Kept separate from the principle
> files themselves so those stay project-agnostic — this file is where the
> concrete, implementation-level detail lives instead.
>
> Entries added only via `proposals/` review (see `proposals/README.md`) —
> not agent-appendable directly, unlike `techplan/examples.md`.

---

## For: `integration-testing-setup.md`

**Context:** Kencleng backend, account domain, MFA TOTP task (#06).
Testing-phase report on the DB-backed integration suite for enroll/
confirm/disable MFA.

**What happened:** an integration test helper
(`TestMfaBackupCode_SingleUseAndDisabledInvalid_RealDB`) opened a
transaction as a no-op probe — `tx, _ := svc.tx.BeginTx(ctx); _ = tx` —
and never committed or rolled it back. That single leaked `pgx.Tx` held
a pooled connection in transaction state for the rest of the test
binary's life. Combined with a genuinely long, separate concurrent-DB
test (100 goroutines confirming MFA against the same real Postgres
instance), the pool was exhausted quickly enough that a subsequent
`go test -tags=integration -run 'TestMfa...'` run **hung past a 240 s
timeout** with no explicit `-timeout` set to fail it fast.

It got worse from there: the hung test binary didn't fully exit when
the run was aborted. A later, entirely unrelated chained command
(`go build && go vet && go test ...`, 180 s budget) also timed out —
not because build/vet/the new test run were themselves slow, but
because the orphaned `account.test` process from the earlier hang was
still alive and still contending for connections against the same
database. Only after that orphan process was manually killed did
ordinary unit runs return to their normal ~7 s.

**Disposition:** the tx leak was fixed (explicit deferred
rollback/commit) but, notably, the fix itself was **not re-verified by
execution** in the same session — it was compile-checked only, per
direction to skip the integration/race runs rather than risk another
hang. The fix landed in the codebase carrying an explicit "unverified"
flag in the testing report until a follow-up run confirms it.

**Generalizable takeaway:** a leaked transaction in test code doesn't
fail loudly — it fails as a hang, and specifically as a hang that gets
worse over the life of a test binary (each additional leaked tx eats
one more pooled connection) and can bleed into completely unrelated
later commands if the process isn't confirmed dead. The fix isn't just
"remember to commit" — it's structural: guard every test-helper
`BeginTx` with `defer`, always run DB-backed suites with an explicit
`-timeout` so a leak fails fast and visibly instead of hanging
silently, and treat "confirm no orphan test process before the next
DB-backed run" as a real step, not an edge case.
