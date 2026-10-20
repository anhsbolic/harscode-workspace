# Rules

These rules define what an execution-grade Techplan must preserve. They are semantic requirements, not a license to repeat source material verbatim.

## 1. Content → Section Mapping

Exploration artifacts vary in name/count. Classify evidence by the question it answers:

| Evidence answers... | Techplan section |
|---|---|
| Why does this change exist? | §1 Background |
| What is in/out? | §2 Scope |
| What conditions/requirements must hold? | §3 Requirements |
| What exact testable scenarios/invariants hold? | §4 Rules & Validation |
| What options were considered and what was chosen? | §5 Decision Log |
| What happens to old clients/data/contracts? | §6 Backward Compatibility |
| What could fail and how is it mitigated? | §7 Edge Cases & Risks |
| What persistence/API/layer contract changes? | §8 Interface Contract |
| What is the high-level execution flow? | §9 Architecture / Plan |
| What live-code anchors and scoped implementation direction matter? | §10 Implementation Details |
| What files are expected touched/untouched? | §11 Files Changed / NOT Changed |
| What verification traces to the rules? | §12 Testing Checklist + Test Focus Pointer |
| What remains unresolved, or was resolved and must remain recorded? | §13 Open Items |

A single Exploration file may feed several sections; one section may draw from several files.

## 2. Dedup & Reconciliation

When evidence overlaps, prefer the source that is more specific/current **only when meaning agrees**. A genuine contradiction becomes an Open Item; never silently choose a convenient version.

Do not copy the same rationale into multiple Techplan sections. Put the authoritative decision/risk/contract once and cross-reference it where needed.

## 3. Runbook vs Techplan

A sub-component with its own execution order, rollback/cleanup, monitoring, or independent lifecycle may deserve a separate linked Techplan/runbook. Keep it inside the parent only when it is inseparable from the parent feature's execution lifecycle.

## 4. Testing Checklist Is Derived From Rules

Every distinct §4 rule ID must have at least one §12 checklist entry. A checklist item with no source rule means §4 is incomplete; fix §4 rather than inventing an orphan test.

Before finalizing, count §4 rule IDs and confirm complete §12 coverage.

## 5. Decision Log Preserves Rejected Alternatives

Whenever more than one material option was considered, §5 records the chosen option and the rejected material alternatives with enough rationale that a later agent does not reopen the same decision by accident.

Do not force trivial local implementation choices into the Decision Log. Record choices whose reversal would change product/domain behavior, authority/security, architecture/ownership, interface/data contract, meaningful risk, or verification strategy.

## 6. Interface Contract Coverage

§8 covers every changed external or cross-layer contract relevant to the task. At minimum consider persistence/data shape, API/event/entry-point shape, and business-logic boundary, then follow the target repo's own authority for what else is required.

Do not fabricate a contract merely to fill a template subsection. Mark genuinely non-applicable parts clearly or omit optional detail where the template allows it.

## 7. Human Report Is Separate and Post-Approval

`techplan.md` has no embedded Summary/digest. Once the Techplan is **Approved**, generate `report-techplan.md` from `report-template.md`. The report is derived from the current Techplan and never becomes the execution source of truth.

If the approved Techplan later changes materially, regenerate the report in full; do not hand-patch the digest independently.

## 8. Open Items Lifecycle

An Open Item is exactly one of:

- **Active** — external input/verification still needed;
- **Resolved** — kept with the actual resolution and consequence.

When an item resolves, move it in the same edit and record what was decided (and who/when when known). Never delete a raised item merely because it is resolved.

## 9. Test Focus Pointer Comes From Exploration Evidence

The Test Focus Pointer carries only Exploration risks that need test classes outside the ordinary Build loop: concurrency/shared state, performance/expensive primitives, or security-sensitive boundaries such as auth/payment/PII.

Every pointer row records an **evidence anchor** to the exact Exploration artifact/heading that justified it:

```text
{TASK_PATH}/1-exploration/logs/<file>.md#<heading-or-stable-identifier>
```

The anchor is a coordinate, not copied evidence. Testing reopens that exact source when it needs the reason/detail.

If a flagged area no longer survives synthesis, mark it N/A with the reason/Decision Log pointer rather than silently dropping it. If synthesis discovers a new sensitive concern that Exploration missed, record the concern and flag the Exploration gap; do not pretend it was carried forward.

## 10. Techplan Spine and Decomposition Invariant

`techplan.md` remains the authoritative spine even when optional decomposition creates task files.

**No material scope/rule, decision, risk, interface or data contract, verification obligation, or unresolved item may exist only in a child task file.**

Task files may carry scoped execution detail, code anchors, sequencing, and local verification detail. They reference the parent spine and may not reinterpret it.

A Build agent executes from:

```text
Techplan spine
+ current task file (when decomposed)
+ declared dependency task only when genuinely required
+ current live code/spec authority
```

It does not need unrelated sibling task files merely because they exist.

## 11. Code Anchors, Not Cached Code Truth

§10 records implementation coordinates as `path + symbol/section + why relevant`. Full snippets are reserved for genuinely novel/non-obvious logic.

An anchor is not a frozen statement that the code still looks the same later. Build must reopen the live code at the anchor before editing. If the anchor moved, locate the current equivalent nearby; if the underlying material contract assumption changed, stop and report back.
