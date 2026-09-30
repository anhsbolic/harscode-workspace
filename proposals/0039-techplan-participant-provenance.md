# Proposal: Clarify Participant provenance in Techplan artifacts

> Status: Accepted
> Date: 2026-09-30
> Triggered by: Kencleng Pilot #2 `WU-S2-002` / `TP-S2-002-012` (generated report used the harness-style label "Codex Planner" where an orchestrated Participant/Profile identity already existed)
> Target: `workflow/2-techplan/template.md` provenance header and `workflow/2-techplan/report-template.md` provenance header/checklist

## Friction Found

Pilot #2 already assigns a concrete Run Participant identity and Participant Profile, but the protected Techplan/report templates only ask for a generic human/agent identity. In `TP-S2-002-012/report-techplan.md`, that ambiguity produced `Codex Planner` as the source/generator identity even though the Run had a distinct Participant ID, Profile, and Role.

This is structural rather than a one-off wording typo: any orchestrated Techplan or report can repeat the same ambiguity because harness/model identity, Profile identity, Role, and concrete Participant identity are different semantics.

## Proposed Change

For orchestrated agent-authored Techplan/report artifacts:

- keep the human/author field for ordinary/non-orchestrated use;
- when a Run Participant exists, record the concrete Participant ID separately;
- record Participant Profile and Role separately when applicable;
- do not use a harness/vendor/model label such as `Codex Planner` or `ChatGPT Reviewer` as the Participant/author identity merely because that harness executed the Run;
- keep model provenance in the existing Model field.

The templates remain usable outside orchestration by omitting Participant/Profile/Role fields when they do not apply.

## Rationale

Harscode already distinguishes Role, Participant, Participant Profile, Session, and model/runtime. Provenance should preserve those boundaries instead of collapsing execution identity into the harness name. This improves reconstructability without creating a new identity object or requiring extra workflow ceremony.

The Human approved this bounded correction on 2026-09-30 together with the Pilot #2 dispatch-boundary corrections.

---

*Accepted by explicit Human review on 2026-09-30. Apply the approved change to the protected target files and retain this proposal as changelog evidence.*
