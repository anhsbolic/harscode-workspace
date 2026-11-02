# Independent Evidence Review, Frontend Security, and SOP Compliance

> **Applicable when:** assurance is required by risk or assignment, testing is delegated, identity/private data is involved, or final quality claims are being assessed. Use proportional scrutiny; do not create a permanent security Agent or a universal testing mandate.

## Independence is observable

Have direct access to current originals and exact output code; separate assessment context from production authorship when independence is required. A different Agent label inside the same biased summary is not evidence of independent challenge. If actual isolation, access, or expertise is insufficient, mark `INDEPENDENCE UNVERIFIED` and explain consequence instead of issuing a PASS.

## Testing evidence and project SOP

First establish what project testing SOP requires, prohibits and assigns to manual QA. Review actual commands/test cases/results or documented manual observation; a lint/build pass, screenshot, mocked component, skipped/zero-test runner or type generation proves only its own limited property. Do not run prohibited automation and do not demand default test count, coverage or Playwright. If high-risk behavior is insufficiently observable under existing SOP, propose a specifically bounded Human-approved exception—never self-authorize.

Keep evidence labels accurate: `MOCK-VERIFIED` ≠ `REAL-API-INTEGRATED`; rendered layout check ≠ keyboard/accessibility assessment; implementation reviewed ≠ externally accepted; pending manual QA ≠ failed or passed QA. Verify that every material required check has one named accountable owner, even if outside this Space.

## Security and risk triage

For affected frontend trust concerns, examine server/client secret bundling; private data in hydration, URL, cache, logs, telemetry and accessible labels; XSS or dangerous HTML; cookie/session/CSRF behavior based on project policy; account/tenant switch; result/replay safety; and frontend role gating not replacing backend enforcement. Do not select an authentication implementation from generic assumptions. For a material issue beyond review competence, request authorized targeted specialist assessment rather than declaring the whole frontend secure.

## Disposition

Report exact source, implementation and evidence revisions; scope of tested/observed conditions, found severity and consequences; unresolved blockers, prohibited/deferred/manual-owned checks, residual risk and next owning action. Reviewer-owned findings are not rewritten by Coordinator. Re-review material fixes at changed edges. No blanket `SECURITY VERIFIED`, `RELEASE READY` or `TESTED` assertion without corresponding evidence and acceptance authority.
