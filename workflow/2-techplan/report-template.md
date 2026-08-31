# Report Template

> Protected file (per proposal 0005, folding in 0004) — sibling to `template.md`. Not edited directly by the agent; changes go through the proposal process.
>
> **This is the sole human-facing artifact.** `techplan.md` no longer contains a Summary section or audience boundary (per proposal 0005) — all reviewer-facing content lives here instead, sourced from the approved techplan.
>
> **Generation rule (enforced):**
> - Generate this file only after the source `techplan.md` reaches `Approved` status. Never draft in parallel with an in-progress techplan.
> - Always regenerate in full from the current `techplan.md` — never hand-patch this file. If `techplan.md` changes after this file was generated (including the Approved→Implemented loop, or a reopened Draft), regenerate before treating this file as current.
>
> **Generation checklist** (relocated from `rules.md` §7 — run every time this file is generated or regenerated):
> - [ ] Top Risks includes High-severity rows only (no Medium/Low leaking in)
> - [ ] Any diagram included has been syntax- and semantic-validated (`guardrails.md` §9)
> - [ ] Open Items here match the current Active/Resolved state in `techplan.md` exactly
> - [ ] Every rule ID or decision referenced still exists in the current `techplan.md` (no stale references from a prior version)
>
> Audience: reviewers/stakeholders who need to understand and sign off, not implement.

---

```
# Report: {Story/Task Title}

> Ticket    : {TICKET-CODE} · **Status: {techplan status at generation time — should be Approved}**
> Author    : {author}
> Version   : report v{n} — generated from techplan v{n}, {date}
> Source    : {path to approved techplan.md} — regenerate this file if the source changes. Do not hand-edit independently.

---

## What & why
{1 short paragraph — plain language, no jargon. What is this for and why does it matter.}

## Scope
**Included**
- {bullet list, plain language}

**Explicitly not included this round**
- {bullet list, plain language — mirror the techplan's out-of-scope list but drop internal file/function references}

## Architecture / Plan
{Include a diagram ONLY if the flow has genuine branching, multiple steps, or state transitions —
same rule as `guidelines.md`'s diagram guidance. If the flow is simple/linear, a one-line prose flow is
enough; do not force a diagram that doesn't add clarity over text.}

{If diagram: prefer Mermaid flowchart, kept simple — no more detail than a reviewer needs to
follow the shape of the flow. No file paths, no line numbers, no internal function names.}

**Components touched:**
| Component | Purpose |
|---|---|
| {component, plain name} | {what it does, in one line} |

**Not touched:** {one line confirming blast radius — e.g. "no schema changes, no changes to existing APIs"}

## Interface Contract
{Only include this section if the story/task adds/changes an external-facing interface (API, webhook, event contract).
Omit entirely for internal-only changes.}

| | |
|---|---|
| **Endpoint / Contract** | {method + path, or event name} |
| **Authentication** | {plain description} |
| **Triggered by** | {who/what calls this} |

**Request:**
| Field | Description |
|---|---|
| {field} | {plain-language description} |

```json
{representative example with realistic sample values, not placeholders}
```

**Response:**
| Field | Description |
|---|---|

```json
{representative example}
```

**Error handling:** {plain-language description of error cases and why, e.g. when 200 vs 400 vs 500 is returned}

```json
// {error case}
{example}
```

## Key decisions
{Pull from the techplan's Decision Log — plain-language "why," not the full rejected-alternatives table.
Only decisions a reviewer would actually need to weigh in on or should be aware of.}

| Decision | Why |
|---|---|

## Risk requiring sign-off
{Only High-severity risks from the techplan's Edge Cases & Risks — same filtering rule as before.}

| Risk | Exposure | Status |
|---|---|---|

## Open item(s) — needs your decision
{Only Active Open Items that need a reviewer/lead decision, described in plain language —
not the full best-practice citation from the techplan.}

## Sign-off
- [ ] Scope confirmed
- [ ] {risk} accepted for this release
- [ ] Open item(s) above decided (or deferred with owner noted)

---
*Full technical detail, rules, and implementation notes: see {path to techplan.md}.*
```