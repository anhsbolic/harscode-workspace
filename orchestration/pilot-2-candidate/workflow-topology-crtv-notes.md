# Pilot #2 Candidate — Group B CRTV Notes

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: concise observations from Pilot #1 that motivate the Group B candidate model.

## Note B1 — Missing Techplan decomposition was not proven to be a defect

Pilot #1 decomposed Slice 1 at the orchestration layer into Backend, Frontend, Topology, and Integration Work Units.

Each delivery Work Unit then received its own Techplan.

No evidence showed that those individual Approved Techplans still required a second intra-plan decomposition for Build/review context.

Conclusion:

- distinguish Parent Outcome → Work Unit decomposition from Approved Techplan → task decomposition;
- absence of the second layer is correct when the Techplan is cohesive.

## Note B2 — Code Review and Testing were default because current workflow says so

Current Harscode lifecycle treats Code Review and Testing as standard downstream independent concerns, while independent Techplan Review and Techplan Decomposition already have explicit conditional gates.

This explains Pilot #1 behavior; it was not participant improvisation.

The open design gap is generalized phase applicability, not the existence of Review/Testing.

## Note B3 — Participant self-skipping is unsafe

Allowing a Builder/Reviewer/Verifier to decide that its downstream independent phase is unnecessary creates a structural incentive to under-verify.

Candidate direction:

- Orchestrator resolves applicability;
- participants may recommend;
- NOT_APPLICABLE requires explicit workflow-grounded rationale;
- uncertainty resolves conservatively toward the independent phase.

## Note B4 — Pilot #1 loops were mixed, not uniformly bad

Examples showed multiple causes:

- frontend review findings were ordinary implementation defects;
- backend Testing exposed missing integration/evidence closure;
- topology review/testing exposed executable verification and runtime closure gaps.

Therefore raw loop count is insufficient to judge Exploration/Techplan quality.

Track cause class and repeated underlying cause instead.

## Note B5 — Targeted confirmation was valuable

Pilot #1 frequently used:

```text
finding
→ narrow Build/Patch
→ targeted confirmation
```

rather than replaying a full independent review from scratch.

This proportional re-entry should be preserved.

## Note B6 — Conservative Testing reread creates known retrieval pressure

Current Testing guidance requires a fresh whole-Techplan consistency read during early workflow-v2 validation.

This is intentional today, but it contributes to broad-read pressure and should be reevaluated with Pilot #2 observability evidence rather than normalized indefinitely.
