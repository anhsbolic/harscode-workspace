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
| Product | NOT STARTED | — |

**Next step:** determined by Anhar. No automatic advance to the preceding stage.

## Sources and evidence standing

This snapshot captures **explicit discussion and working decisions from the 2026-11-03 experiment session**, not fresh empirical user research, code inspection, independent consumer verification, or proof that the model works. Its Git revision is the durable reference for this working artifact; historical conversation is not required to reconstruct its content.
