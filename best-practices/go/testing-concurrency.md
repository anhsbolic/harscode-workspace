# go/examples.md

> Real-world references for files in `go/`. Kept separate from the principle
> files themselves so those stay project-agnostic — this file is where the
> concrete, implementation-level detail lives instead.
>
> Entries added only via `proposals/` review (see `proposals/README.md`) —
> not agent-appendable directly, unlike `techplan/examples.md`.

---

## For: `testing-concurrency.md`

**Context:** Kencleng backend, account domain, MFA TOTP task (#06).
Testing-phase report comparing a full-package `-race` run against a
scoped one, same package, same session.

**What happened:** `go test -race ./internal/domain/account/...` — the
full account package, unscoped — took **319 s (5.3 min)**. The account
package's non-MFA tests are a heavy bcrypt-backed unit suite
(registration/login run real `bcrypt.GenerateFromPassword`/
`CompareHashAndPassword` at production-equivalent cost, and the
register timing-parity tests deliberately burn comparable bcrypt on
every branch to defend against timing attacks) — the race detector
roughly doubles all of that instrumentation cost on top.

The same MFA-specific race coverage, scoped with `-run 'TestMfa'`
against the exact same package, took **17 s** — roughly 19x faster,
for tests that themselves hadn't changed at all. The slowdown was
entirely attributable to unscoped `-race` picking up every other test
in the package, most of which had nothing to do with what was actually
being verified.

**Generalizable takeaway:** `-race`'s cost isn't fixed per test — it's
proportional to everything caught in scope, and scope is controllable
two ways, not just one. Package-level scoping (`./internal/x/...` vs
`./...`) is the coarse lever; `-run` scoping by test name is the fine
one, and the two compound — a package that's slow for reasons entirely
unrelated to the code actually under test (here: bcrypt cost in
sibling tests) is exactly where `-run` scoping earns back the most
time. This is concrete evidence for `testing-concurrency.md`'s
checklist item on scoping race runs to areas with genuine
shared-state/concurrency risk: scope to the *tests*, not just the
package, when a package mixes concurrency-relevant code with
unrelated, independently-slow tests.
