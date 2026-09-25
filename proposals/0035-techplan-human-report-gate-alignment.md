# Proposal: Align Techplan Human report gate timing and ownership

> Status: Accepted
> Date: 2026-09-25
> Protection Tier: techplan-protected
> Triggered by: Kencleng Orchestrator Pilot #1 CRTV review (Human Techplan report timing/ownership contradiction)
> Target: workflow/2-techplan/guardrails.md §8; workflow/2-techplan/report-template.md Human review wording

## Friction Found

Pilot #1 exposed a direct contradiction inside protected Techplan guidance.

The current-effective sources mostly agree that `report-techplan.md` is generated when the Techplan has converged enough to **enter the Human approval gate**, after applicable independent review/resolution has converged and before the Human decides whether to approve/revise/reject the Techplan:

- `workflow/2-techplan/rules.md` §7;
- `workflow/2-techplan/template.md` Report rule;
- `workflow/2-1-techplan-synthesis-prompt.md`;
- `workflow/2-techplan/report-template.md` Generation rule.

However, `workflow/2-techplan/guardrails.md` §8 currently says:

> `report-techplan.md` is generated only after Approval from `report-template.md`.

That stale sentence reverses the gate ordering.

Pilot #1 also exposed a related ownership ambiguity: the Human-facing report was at one point authored by the Orchestrator rather than by the planning workflow participant that owns the source semantics. The report template's current `## Sign-off` heading can further suggest that the report is a separately approved authority object, even though existing rules correctly state that the Techplan remains authoritative.

This is structural rather than a one-off wording issue because the contradiction affects every Techplan that reaches a Human approval gate and can change Run routing, artifact ownership, and approval semantics.

## Proposed Change

### 1. Replace guardrails.md §8

Replace:

```markdown
## 8. Human Report Cannot Introduce Decisions

`report-techplan.md` is generated only after Approval from `report-template.md`. If the report needs a fact/decision/risk that is absent or ambiguous in the Techplan, fix/reopen the Techplan instead of inventing the answer in the report.
```

with:

```markdown
## 8. Human Report Cannot Introduce Decisions

Generate `report-techplan.md` from `report-template.md` only when the current-effective Techplan has converged enough to enter the Human approval gate, after applicable planning review/resolution has converged. The report is derived Human-review evidence; it is not a separate authority object and is not generated as a post-approval artifact.

The planning workflow participant that owns the current Techplan semantics generates or regenerates the report. The Orchestrator may dispatch that work but must not silently author the report as a substitute for the planning participant.

If the report needs a fact/decision/risk that is absent or ambiguous in the Techplan, fix/reopen the Techplan instead of inventing the answer in the report.
```

### 2. Clarify report-template.md approval semantics

In the report template purpose/generation wording, make explicit that:

- the report is presented **before** the Human approval decision;
- the Human approves/rejects/requests revision of the current-effective `techplan.md`, using the report as a derived review aid;
- there is no separate report approval lifecycle or status.

Rename the report section:

```markdown
## Sign-off
```

to:

```markdown
## Human review checklist
```

and add one short sentence before the checklist:

```markdown
This checklist helps the Human review the current-effective Techplan; completing it does not create a separate approval object for this report.
```

### 3. Preserve existing regeneration rules

No change to the existing rule that a material Techplan revision which changes the Human decision surface requires the report to be regenerated before the next Human approval decision.

No change to the precedence rule:

```text
techplan.md > report-techplan.md
```

when they disagree.

## Rationale

The Human report exists to make the **Techplan approval decision** easier. Generating it only after approval defeats that purpose and conflicts with the majority of current protected guidance.

Keeping report generation owned by the planning workflow participant preserves role boundaries:

```text
Planner / planning participant
→ owns Techplan semantics
→ generates derived Human report

Orchestrator
→ dispatches / routes
→ does not become hidden Planner

Human
→ reviews report + current-effective Techplan
→ approves / rejects / requests revision of Techplan
```

Removing separate “sign-off” semantics also prevents the derived report from becoming an accidental second authority or approval lifecycle.

The change is intentionally narrow: it fixes one contradiction and ownership ambiguity without redesigning Techplan lifecycle, report content, or Human approval policy.

---

*After human review: update the Status above. If Accepted, merge the approved changes into the protected target documents and leave this proposal in place as changelog evidence.*
