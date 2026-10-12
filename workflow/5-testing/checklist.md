# Testing Checklist

## Sweep

- [ ] Latest build/patch report read first; named coverage spot-checked rather than blindly recreated.
- [ ] Build report Deferred/Flagged items were addressed or explicitly carried forward.

## Verification readiness

- [ ] Material prerequisites for the intended verification scope were checked.
- [ ] Known missing prerequisites were resolved or explicitly excluded from the
      Run's claimed outcome before execution.
- [ ] Ephemeral test-owned setup is distinguished from durable/shared/security-
      sensitive provisioning.
- [ ] Missing environment evidence is not reported as implementation failure.
- [ ] Secret values were not persisted merely to prove configuration readiness.

## Rule coverage

- [ ] Every Techplan Rules & Validation rule has meaningful verification.
- [ ] Applicable happy, negative, edge, and backward-compatibility behavior covered.
- [ ] Contracted behavior that cannot be exercised through an observable interface is flagged.

## Test Focus Pointer

For every relevant/`Yes` Techplan Test Focus Pointer row:

- [ ] Opened the exact recorded Exploration evidence anchor, not the entire Exploration corpus.
- [ ] Built a concrete specialized execution plan (scope/tooling/threshold or security class as applicable).
- [ ] Concurrency/race scope is targeted where possible rather than an unjustified blanket sweep.
- [ ] Deliberately expensive primitives use test-appropriate cost/work factors.
- [ ] A suspected sensitive area missing from the pointer is reported as Techplan drift, not silently retrofitted into planning history.

## Human-performed verification

- [ ] Human-performed mode is used only where faithful verification materially
      requires Human interaction/account control or the agent cannot safely
      exercise the interface.
- [ ] The scenario and observable PASS/FAIL criteria were defined before asking
      the Human to execute it.
- [ ] No password, token, authorization code, secret, or unnecessary sensitive
      data was requested or persisted.
- [ ] Human-reported results are labeled Human-attested and are not represented
      as agent-independent execution.
- [ ] No unreported sub-result was inferred from a broader Human PASS.
- [ ] The owning contract permits Human-performed evidence for any obligation
      treated as satisfied.

## Errors

- [ ] Applicable error category/external behavior is correct.
- [ ] Error is actionable at the appropriate caller/UI boundary.
- [ ] Propagation follows target-repo convention.

## Final verification

- [ ] Target repo's required build/lint/test commands pass.
- [ ] Migration/schema collision checked when applicable.
- [ ] Backward compatibility explicitly verified when applicable.
- [ ] Broader suite run when target authority/risk requires it for cross-cutting changes.
- [ ] Fresh end-to-end Techplan read completed for contradictions/gaps.
