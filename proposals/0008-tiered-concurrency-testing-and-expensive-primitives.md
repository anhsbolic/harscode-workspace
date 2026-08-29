# 0008 — Tier race/concurrency testing out of the build loop; new file for expensive-primitive test cost

**Status:** Proposed
**Date:** 2026-08-27
**Triggered by:** Real incident — a Kencleng backend story with a concurrency test around bcrypt-based auth stalled the build/patch loop for ~2 hours. Root-caused to two compounding, independent gaps: (1) `testing-concurrency.md`'s existing Principle states `go test -race` should run "as part of the `make verify`/CI gate, not optional" with no scoping guidance on *when* in the lifecycle that gate fires, so it was firing inside the tight build-loop iteration; (2) the concurrent test exercised real bcrypt at production cost factor, and `-race`'s instrumentation overhead multiplied that cost across every parallel goroutine in the test.
**Target area:** best-practices
**Target file(s):**
- `best-practices/go/testing-concurrency.md` — amend Principle + Checklist (full replacement file attached, ready to drop in)
- New: `best-practices/go/expensive-primitives-in-tests.md` (full file attached, ready to drop in)
- `best-practices/index.md` — 1 new row + 1 summary edit (snippet below, not a full-file replacement since this file is large and frequently touched by other proposals)

## Gap found

Two distinct gaps, both real and both contributing to the same incident:

1. **No lifecycle scoping for `-race`.** `testing-concurrency.md`'s Principle says race testing is mandatory and should live in a CI/verify gate — correct as a mandate, but silent on *which* gate. Without that distinction, "mandatory" gets read as "run it every iteration," which is exactly the wrong place for something with `-race`'s overhead. This is the same shape of gap this workspace already named elsewhere (a correct rule stated without the scoping/tiering that makes it actually usable) — see `workflow/2-techplan/retro.md`'s general lesson that a rule without an explicit boundary gets applied maximally by default, not minimally.
2. **No guidance on deliberately-slow primitives inside tests.** Password hashing (bcrypt/argon2/scrypt), and similar work-factor-tunable primitives, are *designed* to be slow in production — that's the security property. Nothing in `best-practices/go/` currently says a test environment should use a different (minimal) cost factor than production. Combined with `-race`'s per-goroutine instrumentation cost, this is a multiplicative problem: N parallel goroutines × production bcrypt cost × race-detector overhead is a near-guaranteed multi-hour stall, and it will recur on any future auth-adjacent concurrency test until this is stated explicitly.

Neither gap is project-specific — any Go codebase with password hashing (or KDFs, or other deliberately-expensive primitives) and a concurrency test around that code will hit this.

## Proposed change

**`testing-concurrency.md`** — amend the Principle to add explicit lifecycle scoping (race testing stays mandatory, but scoped per-area and run in the testing-phase gate, not the fast build/patch iteration), and extend the Checklist with three new items covering scoping and expensive-primitive interaction. Full replacement file is attached — the existing Bad/Good code examples are kept as-is since they're still correct, only the Principle prose and Checklist change.

**New `expensive-primitives-in-tests.md`** — states the core rule (test cost factor is a speed knob, production cost factor is a security knob — never conflate them), shows a Bad/Good example using bcrypt cost, and calls out the specific compounding risk with `-race`/parallel test loops. Full file attached.

**`index.md`**:
```markdown
| go | [go/expensive-primitives-in-tests.md](go/expensive-primitives-in-tests.md) | bcrypt, argon2, scrypt, cost factor, kdf, slow test, hash cost, MinCost | no | Test environment must use a minimal work factor for password hashing/KDFs, never production cost — compounds badly with `-race` and parallel test loops |
```
And amend the existing `testing-concurrency.md` row's Summary column from:
`go test -race + invariant-asserting concurrent tests`
to:
`go test -race, scoped per-area and run in the testing-phase gate (not the build loop) + invariant-asserting concurrent tests`

## Rationale

Genuinely generic (applies to any Go codebase, no Kencleng-specific naming), and directly evidenced by a real incident rather than a hypothetical — meets the root `proposals/` threshold ("a pattern that caused a real bug/incident") on its own without needing a second story. The two files stay separate rather than merging the cost-factor guidance into `testing-concurrency.md` because the expensive-primitive problem isn't concurrency-specific — it applies just as much to a single-threaded test suite that's slow because every test case hashes a password at production cost; concurrency only makes the existing problem worse, it isn't the root cause.
