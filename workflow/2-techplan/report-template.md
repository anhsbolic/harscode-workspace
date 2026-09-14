# Report Template

Protected sibling of `template.md`.

**Purpose:** `report-techplan.md` is the human-facing digest of an **Approved** `techplan.md`. It helps reviewers understand scope, architecture, material decisions, high risks, and open decisions without replacing the execution contract.

**Audience:** reviewer/lead/stakeholder who needs to understand or sign off, not the Build agent implementing the full technical detail.

## Generation rule

- Generate only after the source Techplan reaches **Approved**.
- Generate from the current Techplan; do not draft this report in parallel with an unresolved Draft/In Review plan.
- Regenerate the report in full after a material Approved-Techplan change. Do not hand-maintain it as a second contract.
- If this report and the Techplan disagree, the Techplan wins and this report is stale.

## Generation checklist

- [ ] Scope reflects the current Approved Techplan, including explicit out-of-scope boundaries.
- [ ] Architecture/plan is reviewer-readable and does not leak unnecessary implementation detail.
- [ ] Interface Contract appears only when a materially reviewer-relevant external/cross-boundary contract exists.
- [ ] Key Decisions come from the Techplan Decision Log; no new decision is invented during condensation.
- [ ] Risk requiring sign-off contains High-severity risks only, using the current Techplan severity/status.
- [ ] Open items shown as needing a decision match the current **Active** Open Items. Resolved items are never presented as still needing action.
- [ ] Any diagram is warranted by the source flow and validated for syntax + semantics via `diagram-guidelines.md` and current Techplan rules/contracts.
- [ ] Every referenced rule/decision/risk ID still exists in the current Techplan.

```markdown
# Report: {Story/Task Title}

> Ticket  : {TICKET-CODE}
> Status  : {Approved source status}
> Author  : {author}
> Version : report v{n} — generated from techplan v{n}, {date}
> Source  : {path to approved techplan.md}

---

## What & why

{One short plain-language paragraph: what changes, why it matters, and the outcome this work is meant to enable. Do not restate implementation detail.}

## Scope

**Included**
- {reviewer-relevant behavior/outcome}
- ...

**Explicitly not included this round**
- {material boundary or deferred outcome}
- ...

## Architecture / Plan

{For a simple linear change, use a short prose flow. Use a diagram only when genuine branching, state transition, or multi-component ordering makes it clearer than prose. Validate any diagram via `diagram-guidelines.md`.}

**Components touched**

| Component | Purpose / change |
|---|---|
| {plain component name} | {one-line reviewer-level description} |

**Not touched / blast-radius boundary:** {important areas deliberately unchanged, e.g. no schema change / no existing API change, when material to reviewer confidence}

## Interface Contract

{Include this section only when the Approved Techplan adds/changes a reviewer-relevant API, event, webhook, external interface, or cross-boundary contract. Omit it for purely internal work.}

| Concern | Contract |
|---|---|
| Endpoint / event / interface | {method + path, event name, command, or other contract identity} |
| Authentication / authority | {who may invoke / relevant authority boundary} |
| Trigger / caller | {who or what initiates it} |

**Request / input**

| Field / input | Meaning / requirement |
|---|---|
| {field} | {plain-language description} |

```json
{representative example when JSON is the actual contract format; otherwise use the appropriate concise example format}
```

**Response / output**

| Field / output | Meaning |
|---|---|
| {field} | {plain-language description} |

```json
{representative example when applicable}
```

**Error behavior:** {reviewer-relevant error categories/conditions and consequence. Do not invent detail absent from the Approved Techplan.}

## Key decisions

{Include material choices a reviewer should know or might otherwise re-open. Keep rejected alternatives in the Techplan unless the rejection itself matters for sign-off.}

| Decision | Why / consequence |
|---|---|
| {chosen material decision} | {plain-language rationale} |

## Risk requiring sign-off

{High-severity risks only. If there are none, say `No High-severity risk requiring sign-off identified in the Approved Techplan.` Do not promote Medium/Low risks just to fill the section.}

| Risk | Exposure / mitigation | Status |
|---|---|---|
| {risk} | {plain-language exposure/mitigation} | {accepted / mitigated / open} |

## Open item(s) — needs your decision

{List only current Active Open Items that genuinely need reviewer/lead input. If none, say `None.` Resolved Open Items remain in the Techplan history and must not be presented as active.}

## Sign-off

- [ ] Scope confirmed
- [ ] Material interface/authority change understood, if applicable
- [ ] High-severity risks accepted/mitigated as recorded, if any
- [ ] Active decision items resolved or explicitly owned/deferred, if any

---
*Full execution detail, rule IDs, implementation anchors, and complete risk/decision history: see the Approved source Techplan.*
```

## Notes

- Reviewer readability is the reason this artifact exists; do not compress it into cryptic labels merely to save tokens.
- Do not copy full rule tables, implementation anchors, or low-level test detail from the Techplan unless a specific reviewer decision depends on them.
- This report is derived evidence, not a second place to resolve ambiguity. If condensation exposes a missing material fact, reopen/fix the Techplan first.
