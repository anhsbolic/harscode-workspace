# Testing Checklist

## Sweep

- [ ] Latest build/patch report read first; named coverage spot-checked rather than blindly recreated.
- [ ] Build report Deferred/Flagged items were addressed or explicitly carried forward.

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
