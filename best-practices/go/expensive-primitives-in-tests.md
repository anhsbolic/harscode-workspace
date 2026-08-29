# expensive-primitives-in-tests.md

**Location:** `go/expensive-primitives-in-tests.md`

**Principle**
Password hashing (bcrypt, argon2, scrypt) and other work-factor-tunable primitives are deliberately slow — that slowness is the security property in production. A test environment has a different, unrelated goal: fast, deterministic feedback. These are two independent knobs; never let the production cost factor leak into test fixtures by default (e.g. copy-pasting a real `NewUser` helper that calls `bcrypt.GenerateFromPassword(pw, bcrypt.DefaultCost)` straight into test setup).

Set an explicit, minimal cost factor for tests — driven by config/env, not a hardcoded constant duplicated between prod and test code. The risk compounds badly under two common conditions: (1) any test that creates many users/hashes in a loop (fixtures, table-driven cases, seed data), and (2) `go test -race` or genuine concurrency tests, where per-goroutine instrumentation overhead multiplies an already-slow call across N parallel executions. A single slow call is a few hundred milliseconds; the same call under `-race`, looped across a fixture of 50+ users, or fanned out across 50 goroutines, is where a 2-second test becomes a multi-hour stall — this is exactly the failure mode `testing-concurrency.md` warns about.

This isn't limited to bcrypt — the same principle applies to any deliberately-expensive primitive: PBKDF2/scrypt/argon2 KDFs, artificial rate-limit backoff sleeps, or any "slow by design" security control. If it's slow on purpose in production, it needs an explicit fast-path setting in tests.

**Bad**
```go
func newTestUser(t *testing.T, email string) *User {
    hash, err := bcrypt.GenerateFromPassword([]byte("password123"), bcrypt.DefaultCost) // cost 10 — production setting, reused unchanged in every test
    require.NoError(t, err)
    return &User{Email: email, PasswordHash: hash}
}

// Called in a loop to seed 50 users for a pagination test, or fanned out
// across 50 goroutines in a concurrency test — either way, cost 10 × N
// calls, made worse again if run under `-race`.
```

**Good**
```go
// bcryptCost resolves from config/env, defaulting to a minimal value in
// test builds — production config sets its own real value separately.
// Never hardcode two different literals for the same constant in prod
// vs test code; make it one configurable value with a test-time override.
func bcryptCost() int {
    if v := os.Getenv("BCRYPT_COST"); v != "" {
        if n, err := strconv.Atoi(v); err == nil {
            return n
        }
    }
    return bcrypt.DefaultCost // production default
}

func newTestUser(t *testing.T, email string) *User {
    t.Helper()
    hash, err := bcrypt.GenerateFromPassword([]byte("password123"), bcrypt.MinCost) // cost 4 — test-only, explicit
    require.NoError(t, err)
    return &User{Email: email, PasswordHash: hash}
}
```

**Checklist**
- [ ] Test fixtures/helpers that create password hashes use `bcrypt.MinCost` (or an equivalent minimal setting for the KDF in use), not `bcrypt.DefaultCost` or a hardcoded production value
- [ ] The cost/work factor is a single configurable value with a test-time override, not two independently-hardcoded literals that can drift out of sync
- [ ] Any fixture/seed helper that creates N users/hashes in a loop has been checked for this — the cost multiplies linearly with fixture size even outside concurrency tests
- [ ] Concurrency tests (`testing-concurrency.md`) exercising this code path are double-checked for cost factor — this is the specific combination that causes multi-hour build stalls
- [ ] Any other deliberately-slow primitive in the codebase (KDFs, rate-limit backoff sleeps) has an equivalent fast-path test setting, not just bcrypt
