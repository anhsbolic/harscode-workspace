# Build / Patch Checklist

- [ ] Build target = Approved Techplan spine + current task slice when decomposed.
- [ ] Relevant live code/spec was reopened at recorded anchors before editing.
- [ ] No material contract assumption was silently reinterpreted; invalid assumptions were reported back.
- [ ] Fast edit-loop verification appropriate to the target repo ran clean (unit/component/mocked/API-contract/functional as applicable).
- [ ] Heavy independent race/perf/security-class verification was not pulled into the Build loop merely for extra confidence.
- [ ] Newly discovered specialized-risk area missing from the Techplan Test Focus Pointer was flagged for Techplan/Testing review rather than silently ignored.
- [ ] Expensive test primitives touched by this change use test-appropriate cost/work factors where applicable.
- [ ] Build report explicitly confirms the heavyweight verification boundary and records what changed, tests run, and any deferred/not-tested independent verification.
