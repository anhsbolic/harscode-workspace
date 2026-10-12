# Testing Guidelines

Testing independently verifies observable correctness after implementation/review. It is a final sweep, not a replay of Exploration and Build.

## 0. Start from current claims

Read the latest build/patch report first.

- Spot-check named tests/coverage; do not duplicate equivalent tests.
- Close `Deferred / not tested here` and `Flagged` items first.
- Execute verification whose Techplan primary owner is Testing.
- Then cover what independent Testing uniquely proves: real interface/observable behavior, specialized risk classes, compatibility, migration/schema collisions, and final whole-contract consistency.

Use the Techplan Testing Checklist's `Why / risk if skipped` rationale to choose the minimum credible independent execution. A named tool is not a ritual by itself.

When Testing re-enters after a narrow patch, verify the affected finding/gap first. Re-run broad/final suites when the Techplan or target repo assigns them to Testing, when the patch materially changes the relevant risk/scope, or when a broader suite is required to establish final compatibility. Do not replay unrelated expensive checks solely because another Testing round began.

## Verification prerequisites and environment readiness

Verification readiness is scoped to the intended verification outcome.

Before final or real-interface verification, identify only the material
execution prerequisites declared by the Techplan and target-repo authority:
tool/runtime availability, required services/data, test-owned fixtures,
credential/account presence, external connectivity/provider setup, and
Human-performed interaction where applicable.

A known missing prerequisite that makes the intended verification outcome
impossible must not be discovered only after dispatch if it was already
durably knowable. Resolve the prerequisite first or explicitly narrow the
Testing assignment.

Do not require every environment prerequisite to exist before any Testing can
run. A bounded Testing Run may proceed on executable verification while
carrying unavailable scenarios forward, provided it does not claim the broader
acceptance those scenarios are required to establish.

Testing may create bounded, reversible, test-owned fixtures/environment when
authorized. Durable, shared, or security-sensitive provisioning and external
account configuration remain with their owning project/Human authority.

Unknown availability may be probed early when safe and cheap. Known missing
prerequisites are not equivalent to implementation failure. Do not persist
secret values merely to establish readiness.

## Test Focus Pointer

Read the Techplan Test Focus Pointer. Each relevant specialized row must include an Exploration evidence anchor.

Open **only that exact evidence source/heading** to recover the concrete reason/details. Do not scan all raw Exploration logs merely because one risk needs historical evidence.

Then choose appropriate verification:

- concurrency/race — scope to the relevant unit/package rather than blanket execution where possible;
- performance/load — concrete scenario + threshold;
- security — vulnerability/authority class relevant to the actual boundary;
- expensive primitives — test-appropriate work factor before load/concurrency execution.

Matching stack best practices are conditional authorities discovered through `best-practices/index.md` clue-map routing.

If a sensitive area is clearly present but absent from the pointer, flag Techplan drift instead of silently rewriting planning history inside Testing.

## Rule coverage

Every Techplan Rules & Validation rule needs meaningful coverage. Existing passing coverage can be confirmed rather than recreated. Focus new work on:

- missing coverage;
- failing/stale coverage;
- negative/edge/backward-compatible behavior not already proven;
- real-interface behavior a lower-level test cannot establish;
- Testing-owned final evidence not already supplied by an authoritative equivalent mechanism.

Build-owned rows may be spot-checked according to risk rather than blindly rerun in full. Human-owned rows remain explicit external gates; agent automation cannot mark them passed.

## Human-performed verification

Verification ownership and execution mode are distinct.

A Testing-owned verification may be performed by the Human when faithful
execution materially depends on private credentials or account control,
interactive browser/provider/device behavior, Human-only consent/MFA, or
another interface the agent cannot safely and faithfully exercise.

Do not use Human-performed verification merely to avoid practical agent
verification that is safe, representative, and required.

For a Human-performed verification, Testing must:

- define the bounded scenario, prerequisites, expected observable behavior, and
  PASS/FAIL criteria before execution;
- tell the Human not to provide passwords, tokens, authorization codes,
  secrets, or other unnecessary sensitive material;
- ask the Human to execute and report only the relevant observation/result;
- record the result explicitly as Human-attested evidence;
- not claim that the agent independently executed or verified the scenario;
- not infer unreported sub-results from a broader Human PASS;
- treat ambiguous, incomplete, or materially conflicting evidence as not
  established.

Human-attested evidence may satisfy an obligation only when its owning contract
permits Human-performed evidence for that obligation. It does not replace
required automated, agent-executed, specialist, or independent evidence.

This is distinct from a Human-owned rule or decision: a verification may remain
Testing-owned while its faithful execution is Human-performed.

If a contracted rule cannot be exercised through any real observable entry point, report the mismatch.

## Error verification

Where relevant, verify expected error category, actionable external behavior/message, and propagation through the target repo's error boundary. “An error happened” is insufficient.

## Final verification

Before Pass:

- run target-repo required final build/lint/test commands;
- verify migration/schema collision where applicable;
- verify backward compatibility where applicable;
- run the broader suite when the target repo/risk requires it for cross-cutting changes;
- fresh-read the current Techplan end-to-end for contradictions/gaps.

The fresh Techplan read is intentionally retained during the initial workflow-v2 validation runs. Remove/narrow it only with evidence that quality is preserved.

If a broad check is intentionally not rerun because its evidence remains current and another phase/authoritative mechanism already owns it, record that omission and why it is safe. Verification economy is explicit evidence selection, not silent skipping.

## Findings and patches

Testing may write a patch plan; production code fixes return to Build/Patch authority. Re-run affected verification after the patch according to the proportional re-entry rule above.

The handoff should tell the operator whether to return to the existing healthy Build session or start a fresh Build/Patch session; `BUILD authority` alone is not a complete human instruction.

## Recurring patterns

Consult/add `examples.md` only when a defect represents a reusable category, not every ticket-specific bug. Examples are cold calibration/history, not mandatory startup context.
