# Pilot #2 Candidate — Group D CRTV Notes

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: concise Pilot #1 observations motivating the Group D candidate model.

## Note D1 — Parallel work was milestone-independent, not lockstep

Pilot #1 Backend, Frontend, and Topology Work Units all derived from the same CONTRACT_READY boundary.

They could reach separate milestones independently:

- BACKEND_VERIFIED
- FRONTEND_MOCK_VERIFIED
- TOPOLOGY_VERIFIED

When one sibling finished earlier, no evidence required reopening or blocking it solely because another sibling remained active.

## Note D2 — Integration correctly waited on verified milestones

The integration Work Unit required all three downstream milestone conditions before dispatch.

This was healthier than using weaker signals such as:

- Build complete;
- branch exists;
- agent says done;
- implementation files are present.

Integration readiness should remain milestone/evidence-driven.

## Note D3 — Contract-faithful MSW enabled real parallel frontend work

Kencleng Frontend used MSW at the network boundary while consuming the reconciled API shape/generated types.

This removed unnecessary runtime scheduling dependency on Backend/Topology while preserving the production request path.

The reusable lesson is not “use MSW.”

It is:

> use a contract-faithful substitute boundary when it removes an unnecessary scheduling dependency without creating a second semantic truth.

## Note D4 — Frontend mock verification was intentionally not an integration claim

FRONTEND_MOCK_VERIFIED explicitly described the evidence boundary.

It did not claim:

- real proxy correctness;
- real backend correspondence;
- private storage/media delivery;
- cache/header preservation;
- end-to-end failure timing.

Those claims remained for real integration.

## Note D5 — Integration must not close local verification debt

Pilot #1 integration scope explicitly rejected using integration to hide missing Backend/Frontend/Topology verification.

This separation should be preserved as a reusable orchestration invariant.

## Note D6 — Soft dependencies were useful but require truthful classification

Backend had a coordination relationship with Topology, while still being able to prove backend-owned behavior independently.

Frontend did not require real Backend/Topology for mock-parallel development.

The reusable rule is:

> dependency strength follows the evidence required for the Work Unit's own completion condition.

## Note D7 — Semantic parallelism did not yet require unsafe simultaneous mutation

Pilot #1 had logically parallel Backend/Frontend/Topology delivery but Human-controlled session execution avoided an aggressively concurrent shared-worktree mutation model.

Pilot #2 Automated Visible Fleet may expose this concern more directly.

Keep semantic readiness separate from runtime scheduling and gather evidence before introducing a generic worktree/branch isolation architecture.

## Note D8 — Material contract changes must invalidate only affected work

Because parallel Work Units rely on a shared rendezvous contract, a material contract amendment may make some downstream artifacts/evidence stale.

The Orchestrator should identify affected Work Units and reconcile them without turning every contract adjustment into a project-wide stop.
