# Engineering Production and Verification

> **Status:** WORKING / RESEARCH-ONLY. A responsibility model, not a mandatory universal workflow.

## Start from binding inputs

Any engineering work needs a current project baseline, approved/authoritative outcome or defect, relevant Design constraints, real environment facts, explicit scope and intended consumer. Check source revisions, existing implementation and protected paths before selecting a mechanism.

Do not conflate:
- Product commitment with one implementation task or one Space invocation.
- Solution design with implementation approval.
- Approved artifact with implemented behavior.
- Passed unit test with independent system verification.
- Specified prerequisite with actual prerequisite behavior in the product.

## Bounded responsibilities

| Responsibility | Output/quality obligation |
| --- | --- |
| Investigation | Reproducible observed problem, real code anchors, uncertainty, relevant current constraints |
| Solution design | Shared decisions and interface/state/security/experience contracts; traced acceptance and consumer compatibility limits |
| Implementation | Changes conforming to approved effective input, scoped permissions, and current project code; revisioned implementation evidence |
| Integration | Shared interfaces and result/error/identity/transaction semantics agree across actual producers and consumers |
| Review | Independent critical challenge of source conformance, correctness, security, regression and changed contracts where required |
| Testing | Executed, reproducible results for acceptance, negative paths and specialty risks; failed/unrun checks explicitly reported |
| Delivery | Exact target commit/PR/deployment state, verified evidence, remaining risks and explicit Human decision when required |

These are **concerns**, not eight required sequential agents or mandated directories. One appropriately scoped Space may address several; separate assurance when risk requires true independence.

## Implementation discipline

- Inspect live code and effective API/schema/security constraints before changing anything. Existing code is factual baseline, not Product/Design authority by mere presence.
- Prefer the smallest solution sufficient for the actual requirement; preserve transaction, authorization, identity, idempotency and error semantics when applicable. Prefer reversible exploration for uncertain high-impact changes.
- Define and check compatibility at FE/BE/state boundaries, including unauthorized, failure, partial and ambiguous outcomes; do not invent endpoint contracts or DB schema as Product Truth.
- Treat protected auth/token/security/money and sensitive writes as explicit higher-scrutiny gates. Native workspace permissions alone never authorize them.
- After findings requiring code changes, return to the implementation owner and independently verify the revised output when required.

## Completion claims

`DESIGN REVIEWED`, `IMPLEMENTED`, `TESTED`, `HUMAN ACCEPTED`, and `DELIVERED` are distinct claims, each backed by its own owning artifact/evidence. A Space may truthfully return PARTIAL/BLOCKED. No global state machine is required to preserve these distinctions.

A fresh consumer should be able to identify the exact accepted inputs, output revision, producer, verification owner, security limits and unresolved dependencies without chat recall. If critical information is missing, report the gap to its owner rather than editing product meaning inside engineering.
