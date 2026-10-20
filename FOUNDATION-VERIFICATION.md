# Harscode Foundation Refactor — Integrated Verification

> **Status:** PARTIAL — **SOURCE-LEVEL VERIFIED**, independent consumption and runtime execution **NOT TESTED**.
> **Date:** 2026-10-20
> **Evaluator:** Same-session source inspection; **not** independent fresh-context consumption or a separate runtime reviewer.
> **Harscode subject:** `anhsbolic/harscode-workspace@5e3beb74e4c1231993924cd39a2df47654eab59a` (`refactor/harscode-foundation`).
> **Kencleng operational source:** `anhsbolic/kencleng@e32916b597412094976e3e6263095e861ec18391` (`main`).
> **Historical pilot source:** `anhsbolic/kencleng@91fad854301265357ba69e76182eb5c82ae71049` (`pilot/station5-c1-space-only`).
> **Scope:** Read-only verification of current source semantics, routing and cross-domain contract boundaries. No Kencleng edits; no Engineering Space invoked.

## Verdict

The reconstructed foundation is **coherent enough for further research evaluation**, but not approved as an operational Harscode replacement. No source-level contradiction was found across the five domain boundaries tested. This does **not** establish independent comprehension, current-project adoption, runtime permission enforcement, reviewer independence or Engineering Space output quality.

| Verification | Result | Evidence / limitation |
| --- | --- | --- |
| Repository integrity and historical isolation | **PASS — structural** | Active tree: 29 Markdown sources; 68 relative Markdown links resolved; 257 archived legacy files preserved in `deprecated/legacy/` |
| Product vs Design vs Engineering ownership | **PASS — source-level** | [Product](product/handoff.md) preserves product experience/invariants; [Design](design/authority-and-handoff.md) owns expression; [Engineering](engineering/production-and-verification.md) owns technical implementation/assurance |
| Collaboration vs Space vs Harness authority | **PASS — source-level** | [Balad](collaboration/pairing.md) advisory only; [Space formation](engineering/space-formation.md) requires separate Human authorization; [runtime binding](harness/runtime-binding.md) distinguishes capability and native enforcement |
| Specialist-local engineering knowledge | **PASS — structural** | Scoped [architect](engineering/spaces/feature-solution-design/specialists/solution-architect.md) and [reviewer](engineering/spaces/feature-solution-design/specialists/solution-reviewer.md) guidance; no new centralized best-practices library |
| Current Kencleng authority selection | **PASS after documentation correction** | `main` Product Authority and MVP scope differ from experimental C1 pilot (finding F1) |
| Historical C1 semantic handoff | **PASS — source-level**, **consumer use unverified** | Approved pilot B1–B7 and XR/ER remain distinguishable from Stage 4 exploration and from Rancang candidate output |
| Fresh-session / independent consumer | **NOT TESTED** | Same-session analysis cannot prove independent reconstruction |
| Engineering Space formation, runner, gates and output | **NOT TESTED / NOT AUTHORIZED** | New Rancang package is `NOT FORMED`; no new Human formation/invocation approval |
| Operational promotion | **NOT REQUESTED / NOT APPROVED** | Harscode `main` remains unchanged |

## Cross-domain scenario probe — historical C1

This probe uses **historical pilot evidence**, not current MVP authorization.

1. **Product source.** The pilot's [product intent](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/product-intent.md), [C1 commitment](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-3b-commitment-sequencing.md), and [Stage 4 experience exploration](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-4-c1-interaction-exploration.md) are distinct in scope. Stage 4 is supporting evidence, **not** a competing product authority.
2. **Binding pilot behavior.** [Stage 5](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-5-c1-confirmed-behavior.md) B1–B7 and [Stage 6](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/product/pilot-3-stage-6-c1-requirements.md) protect: no false external authority, pre-effect explanation, attributable Organization + initial Owner success together, later inspection, no upgrade of Organization-provided truth, truthful incomplete result, and safeguards for **known** unresolved representation conflict. Recovery is optional; conflict detection/settlement, IAM implementation, API shape and transaction mechanism are not approved product commitments.
3. **Design consumer.** [Design guidance](design/exploration.md) requires understandable consequence, truthful success/incomplete/uncertain states and preservation of provenance. It does not dictate screens or silently authorize product decisions.
4. **Engineering candidate.** [Rancang input](engineering/spaces/feature-solution-design/contracts.md) I1–I4 requires approved source, current project constraints and concrete Human authorization. Proposed O1–O5 would need cross-boundary identity, API/result/state/experience and verification obligations. **This is an inspectable proposed mapping, not an actual accepted solution bundle.**
5. **Pilot outcome.** The [C1 interim closeout](https://github.com/anhsbolic/kencleng/blob/91fad854301265357ba69e76182eb5c82ae71049/docs/project/station5-c1-s1-interim-closeout.md) reported unresolved coupling and no accepted implementation-consumable solution. A single coherent C1 product outcome does **not** imply one Rancang invocation or already-ready implementation.

### Current Kencleng main authority (separate test)

[Product authority router](https://github.com/anhsbolic/kencleng/blob/e32916b597412094976e3e6263095e861ec18391/docs/product/README.md) identifies [Product Overview](https://github.com/anhsbolic/kencleng/blob/e32916b597412094976e3e6263095e861ec18391/docs/product/product-overview.md) as **canonical whole-product authority**. [MVP Scope](https://github.com/anhsbolic/kencleng/blob/e32916b597412094976e3e6263095e861ec18391/docs/product/mvp-scope.md) and [MVP Delivery Slices](https://github.com/anhsbolic/kencleng/blob/e32916b597412094976e3e6263095e861ec18391/docs/product/mvp-delivery-slices.md) own approved initial delivery scope/sequence. The initial MVP prioritizes public campaign understanding → guest donation → truthful state → closure → continued accountability; **full Organization self-service is deferred by default**, not disproven or permanently forbidden.

The pilot C1 branch is therefore **valuable experimental evidence, not current Kencleng MVP scope or automatic binding authority on `main`**. A future Kencleng Product Authority revisit must start at current `main`, reconcile newer effective revisions and obtain its own Human decision for any actual change.

## Findings and corrections

**F1 — Moderate: historical C1 checklist wording could be mistaken for current Kencleng authority.** Prior Phase 3 wording said pilot `product-intent.md` owned whole-product truth without stressing the **pilot-only** context. Because current Kencleng `main` has a different canonical Product Overview/MVP boundary, following the old text without checking branch could prioritize a deferred C1 self-service capability. **Corrected** the [Refactor Checklist](REFACTOR-CHECKLIST.md) to label the pilot-only claim explicitly and identify current `main` sources. No Kencleng changes.

**F2 — Evidence limitation, not a design contradiction: downstream readiness is unproven.** Proposed source-level I/O and review obligations are coherent, but no active Rancang candidate has Human formation approval, native runtime proof or accepted output. **Leave `NOT FORMED / NOT RUNTIME READY`; do not authorize execution through this verification.**

**F3 — Validation limitation: same-session review is not independent consumption.** Link audits, source traces and correct prose do not prove real reader performance. The next natural evidence can be a fresh real Product/Design discussion or an independently authorized bounded Engineering assignment; do not impose a Product CLI test.

## Remaining gates

- Inspect the reconstructed domains in genuine fresh-context use with current owning sources when the next real Product/Design work begins; record meaningful misunderstandings rather than forcing a ritual.
- Revisit Kencleng Product Authority **starting from `main`**, treating the C1 pilot as external experimental evidence; record proposed changes separately before any project write.
- Review/approve a revised Engineering Space definition on its exact revision **only if** a real engineering task justifies it; verify tool permission, Reviewer independence and actual output then.
- Make separate Human decisions for research baseline replacement and any promotion to operational Harscode `main`.

**Scope conclusion:** Structural/source integrity PASS; overall integrated verification **PARTIAL** until real-use evidence. No automatic promotion.
