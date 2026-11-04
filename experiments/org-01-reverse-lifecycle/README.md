# ORG-01 — Reverse Lifecycle Experiment

> **Status:** WORKING EXPERIMENT / NOT CANONICAL / NOT VERIFIED AS A LIFECYCLE.
> **Repository scope:** Harscode-Workspace, branch refactor/harscode-foundation (research only; main remains operational).
> **Decision owner:** Anhar. **Collaboration:** Anhar × ChatGPT.
> **Example case:** Kencleng ORG-01, used only to reason about a lifecycle through one actor, not to optimize or replace its current implementation.
> **Started:** 2026-11-03.

## Purpose

Make the candidate Product → UX Design (Lo-Fi) → Rancang → UI Design (Hi-Fi) → Engineering (Builder) lifecycle tangible through one simple, real-world scenario. Test whether inputs, work and results at each stage form a coherent chain. This sequence is a **working hypothesis**, not an approved Harscode lifecycle, a mandatory waterfall or an execution plan.

**Chosen actor:** calon pembentuk organisasi — someone who wants to create an organization context and become its first internal Owner on successful creation.

## Experiment method

1. **Work backwards, one stage at a time.** Start with the Engineering — Builder target **Output & Outcome**, then list its **Process**, then the concrete **Inputs**. Move to the preceding stage only when Anhar directs it.
2. Use **Input → Process → Output → Outcome** for each stage. Keep descriptions high-level and concrete (e.g. API Contract, Hi-Fi screens, web assets, functional frontend), not abstract capability descriptions.
3. For inputs, distinguish **Wajib** from **Nice to have** for the chosen case. Required information need not mean one separate document per item.
4. Discuss one stage or one substantive question at a time. Capture the current working result, including assumptions and unresolved decisions; do not treat conversational agreement as project-level approval. **Persist repository updates only after a stage is completed and Anhar explicitly authorizes the write.**
5. Follow **decision-specific sufficiency, proportional to consequence** (working decision): hypotheses may support bounded exploration if marked; consequential downstream choices need relevant authority/approval proportional to risk. Do not demand completion of all Product Definition for an unrelated next decision.
6. Keep **Product consequential sequence** distinct from **Design interaction sequence**. Concrete UI and technical mechanics are not silently promoted into Product policy.
7. Only after this illustrative chain is understood should Anhar decide whether to compare it with existing Harscode/Kencleng artifacts or run real execution evidence. No such comparison or audit is part of the current step.

## Boundaries

- This directory is an **experiment log**, not an authority domain, Product Contract, Design approval, Rancang revision, Engineering assignment, new Space, or authorization to implement.
- No inspection-driven reconciliation, audit, comparison, replacement, or update of existing ORG-01 documents is claimed here. The example is deliberately **defined without using existing ORG-01 files as a template**.
- Nothing here cancels existing Human acceptance, changes Kencleng authority, changes Harscode main, or establishes browser/backend/runtime evidence.
- Keep one actor in view. Do not expand to Reviewer, Staff, fundraising, or other outcomes without a new scoped decision.
- The experiment may revise its working model as learning progresses; a meaningful canonical change would require separate authority and approval.

## Progress

| Stage in candidate sequence | Experiment standing | Record |
| --- | --- | --- |
| Engineering — Builder | WORKING SNAPSHOT: input, process, output and actor outcome drafted | [engineering-builder.md](engineering-builder.md) |
| UI Design — Hi-Fi | FINAL WORKING EXPERIMENT MODEL APPROVED BY ANHAR (2026-11-03): input, process, output & outcome; reusable UI components and Anti-AI Slop included; NOT canonical Design authority | [ui-design-hifi.md](ui-design-hifi.md) |
| Rancang — Engineering Solution | FINAL WORKING EXPERIMENT MODEL APPROVED BY ANHAR (2026-11-03): input, process, output & outcome; API/navigation boundary; no required Hi-Fi input; NOT canonical Engineering authority | [rancang-engineering-solution.md](rancang-engineering-solution.md) |
| UX Design — Lo-Fi | FINAL WORKING EXPERIMENT MODEL APPROVED BY ANHAR (2026-11-03): input, process, output & outcome; webpage map/paths as Design contract for Hi-Fi; NOT canonical Design authority | [ux-design-lofi.md](ux-design-lofi.md) |
| Product — Product Definition | FINAL WORKING EXPERIMENT MODEL APPROVED BY ANHAR (2026-11-03): input, process, output & outcome; Actor vs Domain Role and Product authority boundaries; NOT canonical Product authority | [product-definition.md](product-definition.md) |

**Reverse-stage modeling coverage:** all five stages now have a persisted working snapshot; Builder remains a working snapshot and the other four stages are Anhar-approved experiment models. This is **not** approval, validation, or operational promotion of the full lifecycle. **Next step:** determined by Anhar; no automatic audit or comparison.

## Candidate Input–Source Mapping (2026-11-04)

[**Five-stage Input–Source Mapping — Mermaid diagrams**](input-source-mapping.md) records reverse mappings from the 10 Builder, 13 Hi-Fi, 13 Rancang, 11 UX Lo-Fi, and 13 Product inputs to candidate phase outputs, project-level sources, and Human/external evidence. The mapping permits **non-linear and multi-source** relationships. The lightweight coherence review (approved by Anhar on 2026-11-04) reconciles the previous gaps for Lo-Fi's Webpage Map into Hi-Fi and Product-to-Lo-Fi Content & Information Requirements, and clarifies consumed artifact revision/acceptance standing for Builder.

**Standing:** candidate mapping **recorded** and internally reconciled for three approved clarifications; 60 candidate inputs mapped in total. Not independently verified against actual project sources, not a deep cross-stage audit, and not authorization to promote a lifecycle. No assumption that candidate project-level sources actually exist or are authoritative.

## Research branch — candidate reference and foundation audit (2026-11-04)

At source checkpoint `refactor/harscode-foundation@96b479c1a4e1ead77bb1614ef49bf09aca435c0d`, Anhar authorized a new isolated research branch: `research/cross-stage-mapping`. All new work in this section belongs **only** to that branch; the source branch and operational baseline were not changed.

- [Candidate Reference Model](candidate-reference-model.md) — one audit-facing synthesis of the five experiment concerns, 60 candidate information inputs, source/authority boundaries and ORG-01 illustrative test. Not canonical, not a lifecycle/workflow engine.
- [Foundation Gap Assessment — First Pass](foundation-gap-assessment.md) — checkpoint-wide file inventory, targeted source-depth checks of foundation guidance and Engineering Space definitions, source-linked gaps/alignments, and explicit evidence limits. No audit of an operational branch or current Kencleng artifacts.

**Standing:** initial research formalization and first-pass structural audit recorded; not source-to-runtime validation, formation revision or authority promotion. Next deep-dive decisions belong to Anhar.

## Sequential audit and revision plan (2026-11-04)

[**Audit & Revision Plan / Progress Tracker**](audit-revision-plan-and-tracker.md) is the active research planning and tracking entrypoint on `research/cross-stage-mapping`. Anhar agreed to evaluate and reconcile one concern at a time: **A1 Product → A2 UX Lo-Fi → A3 UI Hi-Fi → A4 Rancang → A5 Builder → A6 final cross-stage coherence**. This is **audit order only**, not operational waterfall or mandatory Space sequence.

**Initial standing:** setup completed; **0/6 audit units settled**. The first-pass foundation assessment remains candidate findings, not an A1–A6 deep-audit PASS. All Product/Design/Engineering/Space owning guidance remains unchanged pending scoped review/approval. `main` is neither inspected nor edited; `refactor/harscode-foundation` remains an unchanged source checkpoint.

## Sources and evidence standing

This snapshot captures **explicit discussion and working decisions from the 2026-11-03 experiment session**, not fresh empirical user research, code inspection, independent consumer verification, or proof that the model works. Its Git revision is the durable reference for this working artifact; historical conversation is not required to reconstruct its content.
