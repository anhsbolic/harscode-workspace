# Report Template

Protected sibling of `template.md`.

**This is the sole human-facing Techplan digest.** Generate it only from an **Approved** `techplan.md`; regenerate in full whenever the source materially changes. Never hand-maintain it as a second contract.

Generation checklist:

- [ ] Top Risks contains High-severity rows only.
- [ ] Any diagram is warranted by the source flow and validated for syntax + semantics (`guardrails.md` §9; `diagram-guidelines.md`).
- [ ] Open Items match current Techplan §13 Active/Resolved state.
- [ ] Referenced rule/decision IDs still exist in the current Techplan.
- [ ] No new decision/risk/contract was invented during condensation.

```markdown
# Report: {Story/Task Title}

> Ticket  : {TICKET-CODE}
> Status  : {Approved source status}
> Author  : {author}
> Version : report v{n} — generated from techplan v{n}, {date}
> Source  : {path to approved techplan.md}

## What & why
{short plain-language purpose/problem}

## Scope

**Included**
- ...

**Explicitly not included**
- ...

## Architecture / Plan

{One-line flow for simple/linear work. Use a diagram only for genuine branching, state transitions, or multi-component ordering; validate via `diagram-guidelines.md`.}

**Components touched**

| Component | Purpose |
|---|---|
| ... | ... |

**Not touched:** {blast-radius confirmation}

## Interface Contract

{Include only when an external-facing/cross-boundary contract materially changes.}

| Concern | Contract |
|---|---|
| Endpoint/event/interface | ... |
| Authentication/authority | ... |
| Trigger/caller | ... |

**Representative request/input:**
```json
{}
```

**Representative response/output:**
```json
{}
```

**Error behavior:** ...

## Key decisions

| Decision | Why |
|---|---|
| ... | ... |

## Risk requiring sign-off

{High-severity only.}

| Risk | Exposure / mitigation | Status |
|---|---|---|
| ... | ... | ... |

## Open item(s) — needs decision

{Active items that need reviewer/lead input.}

## Sign-off
- [ ] Scope confirmed
- [ ] High risks accepted/mitigated as recorded
- [ ] Active decision items resolved or explicitly owned/deferred

---
*Execution detail: see the Approved source Techplan.*
```
