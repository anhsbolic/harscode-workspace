# Checklist

Run through before considering implementation done. Not every item
applies to every change — skip what's genuinely not relevant, don't
skip what is.

## Safety

- [ ] Every dereferenced pointer/optional has a nil/null check where the
      value can legitimately be absent
- [ ] Concurrent code (goroutines/async tasks/threads) has no shared
      mutable state without synchronization
- [ ] No error is caught and silently discarded — every error is either
      returned, logged with enough context to act on, or explicitly
      justified why it's safe to ignore
- [ ] Calls to external services propagate context/cancellation
      correctly
- [ ] Resources (connections, locks, file handles) are released on
      every return path, including early errors

## Quality

- [ ] No duplicated logic that should be a shared helper
- [ ] Function/variable names describe what they do, not just what type
      they are
- [ ] Logging exists at points that matter for future debugging
- [ ] No leftover unused parameters or dead code from refactoring
      (static analysis often misses unused *parameters*, only unused
      *variables* — check manually)

## Stack-Specific Best Practices (requires reading best-practices/index.md)

- [ ] Checked `best-practices/index.md`, matched trigger keywords against
      the technology/area(s) touched by this diff (Go, PostgreSQL,
      GraphQL, REST API, Kafka, Pub/Sub, Redis)
- [ ] Applied the checklist from each matching file (e.g. a Kafka
      consumer change → `kafka/consumer-and-offset-management.md`; a new
      GraphQL resolver → `graphql/resolver-n-plus-one.md`)

## Consistency (requires reading the target repo's own convention file)

- [ ] Error handling matches existing convention in this repo
- [ ] Logging format matches existing convention
- [ ] New constants/messages follow existing naming pattern
- [ ] Validation approach matches how it's done elsewhere in this
      codebase