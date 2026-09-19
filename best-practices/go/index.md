# Go Best-Practices Index

Use this subindex when the active concern is already known to be Go implementation work. Match the concrete risk/behavior and open only the relevant guidance.

## Core implementation

| Concern | Guidance |
|---|---|
| errors/results | [error-handling.md](error-handling.md), [error-wrapping.md](error-wrapping.md) |
| abstraction boundaries | [abstraction-boundaries.md](abstraction-boundaries.md) |
| naming/scope | [naming-and-scope.md](naming-and-scope.md) |
| context/cancellation | [context-propagation.md](context-propagation.md) |
| nil/zero values | [nil-and-zero-values.md](nil-and-zero-values.md) |
| defer/resource lifetime | [defer-pitfalls.md](defer-pitfalls.md) |
| interface/slice semantics | [interface-and-slice-semantics.md](interface-and-slice-semantics.md) |
| struct/time semantics | [struct-copying-and-time.md](struct-copying-and-time.md) |
| HTTP clients | [http-client-and-transport.md](http-client-and-transport.md) |
| panic/recover | [panic-and-recover.md](panic-and-recover.md) |
| goroutine lifecycle | [goroutine-lifecycle.md](goroutine-lifecycle.md) |

## Security / correctness boundaries

| Concern | Guidance |
|---|---|
| validation/injection | [input-validation-and-injection.md](input-validation-and-injection.md) |
| sensitive logging | [secrets-and-sensitive-logging.md](secrets-and-sensitive-logging.md) |
| JWT/token lifecycle | [jwt-and-token-lifecycle.md](jwt-and-token-lifecycle.md) |
| authorization/IDOR | [authorization-and-idor.md](authorization-and-idor.md) |
| roles/privilege separation | [role-and-privilege-separation.md](role-and-privilege-separation.md) |
| webhook signatures | [webhook-signature-verification.md](webhook-signature-verification.md) |
| secrets/key management | [secrets-and-key-management.md](secrets-and-key-management.md) |
| file upload | [file-upload-handling.md](file-upload-handling.md) |
| rate limiting | [rate-limiting.md](rate-limiting.md) |
| dependency/supply chain | [dependency-and-supply-chain.md](dependency-and-supply-chain.md) |

## Domain-sensitive implementation

| Concern | Guidance |
|---|---|
| decimal/money | [decimal-and-money.md](decimal-and-money.md) |
| concurrency testing | [testing-concurrency.md](testing-concurrency.md) |
| expensive test primitives | [expensive-primitives-in-tests.md](expensive-primitives-in-tests.md) |
| integration testing | [integration-testing-setup.md](integration-testing-setup.md) |
| feature lifecycle | [feature-lifecycle.md](feature-lifecycle.md) |

## Retrieval rule

Select by the actual implementation/risk trigger, not simply because the code is Go. Cross-cutting concerns such as PostgreSQL, REST API, money, or network-boundary security may require a sibling category routed from `../index.md`.
