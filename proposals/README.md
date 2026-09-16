# proposals/

Single, continuously-numbered log of every proposal to change protected/shared guidance in this workspace, regardless of which area it targets.

This folder used to be two separate mechanisms: a root `proposals/` and a separate `workflow/2-techplan/proposals/`. Two independent sequences that occasionally needed to cross-reference each other produced colliding numbers, so the workspace now uses one folder, one shared sequence, and a Protection Tier field instead of separate numbering domains.

## Protection Tier field

Every proposal states its tier after Status/Date:

- **`techplan-protected`** — targets one or more of `workflow/2-techplan/{template.md, rules.md, guardrails.md, guidelines.md, diagram-guidelines.md, report-template.md}`. Higher threshold: use when friction repeats across 2+ tasks or the gap is genuinely structural.
- **`general`** — targets shared `product-design/`, `best-practices/`, `harness-optimization/`, or a lightweight `workflow/` phase when a formal proposal is warranted. A real incident, recurring pattern, or structural shared-guidance gap is sufficient justification.

Use `_proposal-template-general.md` or `_proposal-template-techplan-tier.md` as the starting shape.

## After human review

Update the `Status` field (`Proposed` → `Accepted` / `Rejected` / `Superseded`). If Accepted, apply the approved change to the target file(s) and leave the proposal in place as changelog evidence.

**No self-approval.** The actor that authors a proposal is not the approval authority for that proposal. Obtain explicit human-owner or independent authorized acceptance before merge. After that approval, an authorized implementation actor may mechanically apply/merge the accepted change; it does not turn authorship into approval authority.

## Numbering

Strictly sequential, one shared counter across all tiers and shared areas. Check the highest existing number before adding a new proposal; do not restart by area/tier.

## History note

Proposals 0001-0003 predate the root-folder consolidation. Proposals 0004 onward use the shared root sequence.

### Workflow-v2 integration renumbering

`workflow-v2` was developed from a baseline before `main` accepted `0030-upstream-product-design-guidance.md`. While the branch was isolated, its experimental workflow proposals used numbers `0030`–`0033`.

Before promotion, current `main` was merged into `workflow-v2`. The accepted product-design proposal keeps **0030** because it already landed on `main`; the experimental workflow-v2 proposals were mechanically renumbered to preserve one shared sequence:

```text
experimental 0030 → final 0031  workflow-v2 context efficiency and handoff
experimental 0031 → final 0032  pre-validation audit remediation
experimental 0032 → final 0033  provenance, handoff, and harness observability
experimental 0033 → final 0034  proportional Techplan and verification ownership
```

Historical audit files written before this reconciliation may cite the experimental numbers they observed at the time. Treat those citations as historical identifiers and use the mapping above to locate the final proposal file; do not rewrite historical audit evidence merely to make its old numbering look current.
