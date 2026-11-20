# Harscode Open Items — Research Discovery Index

> **Standing:** RESEARCH FOLLOW-UP DISCOVERY INDEX, 20 November 2026. This is **not** a canonical phase process, additional policy, approval ledger, workflow engine, automatic dispatch queue or replacement for the owning research tracker. Current operational baseline is `main`; this file is research-branch navigation only.
> **Purpose:** Help a fresh session find **actionable deferred work**, **candidate improvements**, and **evidence-dependent questions** without remembering chat history or reading every experiment checkpoint.

## How to use

An item appears here only when there is a **specific unfinished decision or useful future action**, with a verifiable owning reference and **revisit trigger**. The owning document remains authoritative for underlying findings, actual standing, decision authority, scope and closure. This index is a **pointer**, not a second source of truth: if a summary conflicts with the owning artifact, verify and correct the pointer; do not silently change the owning decision. No item authorizes repository changes or operational use.

Kinds:
- **Improvement candidate:** justified proposed change; not yet accepted as new guidance.
- **Awaiting evidence:** action depends on a material observation or verification not yet available.
- **Deferred research debt:** identified work intentionally postponed, with existing ownership and explicit conditions for resuming.

Do not list completed/retained principles as new debt, or automatically convert every observation into a task. A project-local issue stays with the owning project; it is not a new Harscode obligation merely because a Harscode experiment encountered it.

## Discoverable open follow-ups

| ID | Concern / open question | Kind / current disposition | Revisit trigger and useful next action | Owning reference |
| --- | --- | --- | --- | --- |
| **HI-001** | Product P3/P4 — separate legitimate consequential decision criteria, evidentiary judgment and what must be known at a material decision point | **IMPROVEMENT CANDIDATE**; narrow clarification proposed, **not approved/implemented** | After actual receiving-UX findings or independently material counterexample: check whether ambiguity affected decisions; if justified, propose **one generic, minimal P3/P4 wording change** for Human content review; no universal approval stage or scoring framework | [Product retro triage — #3 + #4](../experiments/product-v2/po-01-product-retro-improvement-triage-2026-11-20.md#2-eight-recommendations--research-disposition) · [Selected Product Definition](../product/product-definition.md) |
| **HI-002** | Product completion vs consumer-specific information sufficiency vs downstream implementation authorization | **IMPROVEMENT CANDIDATE**; non-normative clarity example proposed, **not approved/implemented** | Review actual fresh UX receiving interpretation; if confusion recurs or a concrete consumer risk is established, consider **one compact project-neutral example** in Consumer Handoff, not a mandatory status quartet | [Product retro triage — #2](../experiments/product-v2/po-01-product-retro-improvement-triage-2026-11-20.md#2-eight-recommendations--research-disposition) · [Consumer Handoff](../product/consumer-handoff.md) |
| **HI-003** | Product working-decision persistence and approval overhead — whether specific checkpoints/revisions duplicate work without improving authority or reconstructability | **AWAITING EVIDENCE**, **no edit justified yet** | Obtain specific Product-session process examples: repeated decisions, redundant files, extra approval cycles, Human time/friction and the loss-risk of consolidation. Only then test a cheap reversible simplification without weakening exact-revision approval or durable state | [Product retro triage — #6](../experiments/product-v2/po-01-product-retro-improvement-triage-2026-11-20.md#2-eight-recommendations--research-disposition) · [Authority & Approval](../product/authority-and-approval.md) |
| **HI-004** | Engineering Builder — deferred deeper Go/backend specialization after applicable horizontal responsibility/coherence assessment | **DEFERRED RESEARCH DEBT**; remains owned by existing Engineering research tracker, **not newly scheduled** | Reassess only when owning cross-stage research scope/dependencies justify vertical specialization; first inspect actual owner-tracker standing and bounded closure criteria. Do not assume conceptual research equals formation/runtime readiness | [Owning cross-stage research tracker](../experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md) · [Engineering deferred-depth criteria](../experiments/org-01-reverse-lifecycle/a5-engineering-builder-horizontal-coherence-and-vertical-depth-debt.md) |

## Current Product retro follow-up plan

- **Now:** Keep selected Harscode Product and UX guidance unchanged while the bounded receiving-UX experiment is in progress. Preserve exact experimental inputs and their observed revisions.
- **On actual UX receiving evidence:** Evaluate **HI-001** and **HI-002** against observed source interpretation, consequential mistakes, and consumer decisions. Prepare only evidence-justified minimal candidate diffs; obtain legitimate Human content review before changing the selected Product sources. A fresh UX intake can inform Product handoff without proving broad Harscode Product robustness.
- **Separately:** Investigate **HI-003** only from actual Product-session cost/friction examples. Do not infer waste from commit/file counts.
- **Project-local authority-routing cleanup:** Identified in [retro triage #7](../experiments/product-v2/po-01-product-retro-improvement-triage-2026-11-20.md#2-eight-recommendations--research-disposition); it belongs in the **owning target project**, after preserving the fresh UX consumer baseline. **Not duplicated as Harscode open debt**.
- **Already covered, no open item:** Retro #1 (decision-specific completion), #5 (Product semantic probes vs UX), #8 (affected-edge blocking) remain research evidence in [the triage](../experiments/product-v2/po-01-product-retro-improvement-triage-2026-11-20.md), absent new material failure evidence.

## Reconcile and close

When revisiting an item, read its owning source first; decide whether it is still relevant, needs new evidence, is intentionally deferred, was implemented at a reviewed exact revision, or should be **closed without change**. Update this index to point to the actual decision/commit/evidence and remove the item from the open table or label it closed in a short closure note **only after the owning decision is recorded**. Do not mark a proposal completed because a related session started, a draft exists, or a checkpoint says "promising".

There is **no automatic recurring review, SLA, milestone, approval gate or numbering standard** implied. IDs are local navigation keys for this discovery index, not Harscode runtime entities or mandatory project IDs.
