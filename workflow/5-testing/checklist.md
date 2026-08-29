# Checklist

## Test Coverage

- [ ] Happy path tested via the real interface
- [ ] Negative cases tested (missing fields, invalid input, dependency
      failure)
- [ ] Edge cases tested (empty/null/boundary values)
- [ ] Backward compatibility tested (old client behavior, existing data)
- [ ] Every rule in techplan § 4 (Rules & Validation) maps to at least
      one test

## Test Focus Pointer Execution (if techplan § 12 has any rows)

- [ ] Every "Y" row in techplan's Test Focus Pointer has a concrete
      Test Execution Plan (scope, tooling, threshold) — not just
      re-run generically
- [ ] Race/concurrency tests are scoped to the specific package(s),
      never a blanket `./...` sweep
- [ ] Any deliberately-slow primitive (bcrypt, other KDFs) exercised
      under load/concurrency uses a test-appropriate cost factor, not
      production settings
- [ ] An empty pointer table with a suspected sensitive area has been
      flagged back as a possible techplan drift, not silently
      resolved by adding a test unilaterally

## Error Verification

- [ ] Error category is correct (not generic when specific was expected)
- [ ] Error message is actionable for the caller
- [ ] Error propagates through the app's actual error-handling layer

## Before Marking Done

- [ ] Target repo's own build/lint/test commands pass
- [ ] Migration/schema version (if any) doesn't collide with anything
      landed since techplan was written
- [ ] Fresh end-to-end read of the techplan for gaps or contradictions
