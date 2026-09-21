# Template: techplan.md

Follow this structure with `rules.md` and `guardrails.md`. `techplan.md` is the **execution-grade authoritative spine** for the implementing agent and engineering review: complete, unambiguous, non-redundant.

At the Human approval gate, generate `report-techplan.md` from `report-template.md` after applicable planning review/resolution has converged. It is the sole human-facing digest; never add an embedded Summary back here.

```markdown
# Tech Plan: {Feature Name}

> Phase             : Techplan
> Ticket            : {ticket code or none}
> Author            : {human/agent identity}
> Model             : {exact model when agent-authored/exposed; otherwise omit/not exposed}
> Reasoning         : {when exposed; otherwise omit/not exposed}
> Session           : {session/thread id when useful and safe to persist}
> Created           : {YYYY-MM-DD or timestamp}
> Updated           : {when materially revised}
> Target revision   : {commit/ref if known}
> Workflow revision : {Harscode commit/ref if known}
> Status            : Draft / In Review / Approved / Implemented
> Approach          : {optional one-line orientation}
> Refs              : {source specs / target authority / related artifacts}

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
|---|---|---:|---:|---|
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

Preserve verification coverage for every Rules & Validation rule. Use one or more rows per rule when different evidence/owners are genuinely required.

| Rule | Verification / evidence | Primary owner | Why this is worth running / risk if skipped |
|---|---|---|---|
| R1 | ... | Build / Testing / Human | ... |
| R2 | ... | ... | ... |

Primary owner means who owns the authoritative evidence, not who is forbidden from ever running the check:

- **Build** — fast/focused edit-loop confidence or an artifact/test that must be executable as it is authored.
- **Testing** — independent final/broad verification.
- **Human** — subjective/product acceptance automation cannot decide.

Code Review is normally a reasoning phase, not the primary owner of a planned suite; it may run a targeted reproduction/check when needed to substantiate a suspected finding.

When a non-trivial verification tool/technique is named (for example browser automation, production build, race detector, load test, security scan, or human rendered acceptance), explain why it is appropriate and the meaningful risk if it is skipped. Do not prescribe a heavyweight tool merely for ceremony.

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

## Provenance rule

Do not invent unavailable model/session/revision metadata and do not persist credentials/account identifiers. Git history remains the default version history; do not add a manual semantic Techplan version unless an external artifact/contract genuinely requires one.

## Spine invariant

Optional decomposition may move scoped execution detail into `2-techplan/tasks/`, but this Techplan remains the authoritative spine. No material scope/rule, decision, risk, interface/data contract, verification obligation, or unresolved item may exist only in a child task file.

## Report rule

Generate `report-techplan.md` from `report-template.md` when the current-effective Techplan is ready for the Human approval gate under `rules.md` § Human Report. Regenerate it in full after a material revision changes the Human decision surface, including later material changes to an Approved Techplan. The report never overrides this file.
