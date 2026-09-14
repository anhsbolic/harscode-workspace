# Template: techplan.md

Follow this structure with `rules.md` and `guardrails.md`. `techplan.md` is the **execution-grade authoritative spine** for the implementing agent and engineering review: complete, unambiguous, non-redundant.

After **Approved**, generate `report-techplan.md` from `report-template.md` as the sole human-facing digest. Never add an embedded Summary back here.

```markdown
# Tech Plan: {Feature Name}

> Ticket    : {ticket code}
> Author    : {name}
> Date      : {YYYY-MM-DD}
> Updated   : {when materially revised}
> Status    : Draft / In Review / Approved / Implemented
> Approach  : {optional one-line orientation}
> Refs      : {source specs / target authority / related artifacts}

---

## 1. Background

Why this change exists and the current problem. Keep it factual; do not repeat later implementation detail.

## 2. Scope

**In scope:**
- ...

**Out of scope (explicit):**
- ...

## 3. Requirements

| ID | Requirement | Source / evidence |
|---|---|---|
| Q1 | ... | ... |

## 4. Rules & Validation

Testable behavior/invariants. Give stable rule IDs.

- **R1** — Given ... when ... then ...
- **R2** — ...

## 5. Decision Log

Record material choices so a later agent does not reopen rejected approaches.

| ID | Decision / option | Status | Rationale / consequence |
|---|---|---|---|
| D1 | Option A | Chosen | ... |
| D1-alt | Option B | Rejected | ... |

## 6. Backward Compatibility

- Existing data: ...
- API/contracts/clients: ...
- Migration/deprecation compatibility: ...

## 7. Edge Cases & Risks

| ID | Risk / edge case | Likelihood | Severity | Mitigation / accepted exposure |
|---|---|---|---|---|
| RISK-1 | ... | ... | ... | ... |

## 8. Interface Contract

Follow the target repo's own authority; include only applicable contract surfaces.

**Persistence/data shape:** ...

**API/event/external interface:** ...

**Cross-layer/business boundary:** ...

## 9. Architecture / Plan

High-level execution/data/control flow. Include a diagram only for genuine branching, state transition, or multi-component ordering; when used, follow `diagram-guidelines.md`.

## 10. Implementation Details

Use code anchors instead of freezing routine code into prose.

| Anchor | Why relevant | Intended change / precedent |
|---|---|---|
| `path/to/file.ext` — `SymbolName` | ... | ... |

Full snippets only for genuinely novel/non-obvious logic that materially reduces ambiguity.

## 11. Files Changed / Files NOT Changed

| File / area | Change type | Description |
|---|---|---|

| File / area intentionally untouched | Why |
|---|---|

## 12. Testing Checklist

Derived 1:1 from §4 rule IDs.

- [ ] R1 — ...
- [ ] R2 — ...

### Test Focus Pointer

Only specialized concurrency/perf/security-sensitive evidence that belongs in the independent Testing phase.

| Area | Why sensitive | Evidence anchor from Exploration | Still relevant post-synthesis? |
|---|---|---|---|
| ... | ... | `1-exploration/logs/<file>.md#<heading>` | Yes / N/A — reason + Decision Log pointer |

This is a pointer, not the full test execution plan.

## 13. Open Items

### Active — needs external input or verification

1. ...

### Resolved — retained as decision history

1. ~~**{short title}**~~ **RESOLVED — {actual resolution}.** {who/when if known; consequence if any}.
```

## Spine invariant

Optional decomposition may move scoped execution detail into `2-techplan/tasks/`, but this Techplan remains the authoritative spine. No material scope/rule, decision, risk, interface/data contract, verification obligation, or unresolved item may exist only in a child task file.

## Report rule

When the Techplan first reaches Approved, and whenever an Approved report becomes stale because the source Techplan materially changed, regenerate `report-techplan.md` from `report-template.md` in full. The report never overrides this file.
