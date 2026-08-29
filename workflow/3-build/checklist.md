# Checklist

- [ ] Only unit, mocked-service, and API-contract tests run in this
      loop's iterations — no `-race`, no perf/load, no security-class
      test, regardless of what the techplan's Test Focus Pointer says
- [ ] Any new or touched fixture/helper that hashes a password or runs
      a KDF uses a minimal test-time cost factor, not the production
      default
- [ ] A genuinely concurrency/perf/security-sensitive area discovered
      mid-implementation, and not already reflected in the techplan's
      Test Focus Pointer, is flagged back for techplan review — not
      silently tested here, and not silently skipped
- [ ] The change satisfies its assigned scope from techplan § 4,
      confirmed via the real interface — not just code reading
- [ ] If a contract assumption from the techplan turned out wrong
      during implementation, that's reported, not silently worked
      around