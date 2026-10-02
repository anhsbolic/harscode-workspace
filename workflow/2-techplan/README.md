# Techplan Guidance

This folder owns the portable rules for turning Exploration evidence into an execution-grade `techplan.md`.

## Runtime file map

| File | Role | Context class |
|---|---|---|
| `template.md` | Required output structure | **Required** |
| `rules.md` | What the Techplan must preserve and how evidence maps into it | **Required** |
| `guardrails.md` | Hard stops / no-assumption boundaries | **Required** |
| `guidelines.md` | Process reference for synthesis/revision | Routing / conditional when using the canonical prompt |
| `diagram-guidelines.md` | Mermaid syntax/semantic rules | Conditional — only when a diagram is warranted |
| `examples.md` | Tone/detail calibration | Cold — open only when shape/detail is ambiguous |
| `techplan-example.md` | Full finished example | Cold |
| `retro.md` | Historical failures and lessons | Cold — do not load every run; recurring lessons belong in stable rules |
| `report-template.md` | Human-approval-gate digest template | Conditional — only when the exact Techplan artifact/revision is ready to enter the Human approval gate |
| `report-techplan-example.md` | Human-report example | Cold |

The canonical synthesis entrypoint is `../2-1-techplan-synthesis-prompt.md`. It already carries the execution process; do not recursively read every file in this folder before synthesis.

## Fundamental rules

1. `template.md`, `rules.md`, `guardrails.md`, `guidelines.md`, `diagram-guidelines.md`, and `report-template.md` are protected. Change them through the root `proposals/` mechanism.
2. `examples.md` and `retro.md` are append-only exceptions. Add only reusable calibration/learning; do not use them as a shadow rule system.
3. Stable rules win over examples/retro history. If history reveals a recurring structural gap, promote the lesson through a proposal instead of requiring future agents to reread the history.
4. Proposal threshold for this protected tier: recurring friction across 2+ tasks or a genuinely structural gap.

## Output model

```text
Exploration durable evidence
        ↓
Techplan synthesis / revision
        ↓
techplan.md — Draft/In Review for the first approval lifecycle
        │
        ├─ material successor after an existing approval
        │  → techplan.candidate.md while the Approved predecessor remains current-effective
        │
        ↓
exact Techplan artifact/revision reaches Human approval gate
        ↓
report-techplan.md — derived human-facing digest generated before the Human approval decision
        ↓
Human approval + bounded lifecycle reconciliation
        ↓
techplan.md — current-effective Approved execution-grade spine
        ↓ optional after Approval
2-techplan/tasks/* — scoped execution slices; never a replacement for material spine decisions
```

`techplan.md` is the stable execution spine once current-effective; a material post-Approval candidate is a proposed successor to that same logical Techplan, not a second independent contract. The separate report is the reviewer digest for the exact revision at the Human gate; do not add an embedded Summary back into the Techplan and do not treat the report as a separate approval object.
