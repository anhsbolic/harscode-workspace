# 0032 — Workflow-v2 pre-validation audit remediation

**Status:** Accepted - Anhar
**Date:** 2026-09-14
**Protection Tier:** general
**Triggered by:** `audits/workflow-v2-audits.md`, followed by an independent verification pass against `main@fbeb2e657e1258c5c45dc5f70518acd7f915baa8` and the frozen workflow-v2 checkpoint `6edc1a6c9be10d54b3e37cc0c477c28790fcd81c`.
**Scope:** `workflow-v2` only. `main` remains untouched as the proven comparison baseline.

> Renumbering note: this proposal was `0031` on the isolated experimental branch and became final proposal `0032` when current `main` (which already owned proposal `0030`) was reconciled before promotion.

## Why this remediation exists

The pre-validation audit found a small set of semantic regressions introduced during context-efficiency compression. Independent verification confirmed the important defect classes but corrected two parts of the original severity assessment:

- hardcoded Techplan section numbers in runtime phase guidance were a real regression and had spread beyond the original review prompt;
- the Build report lost a useful forcing function, but the underlying heavyweight-test boundary still survived in Build checklist/guidelines, so the defect was auditability/enforcement weakening rather than total rule deletion;
- removal of `model-routing.md` pointers from generic phase prompts was largely intentional under accepted proposal 0028; what must remain mandatory is independent reviewer/actor context, while named model/client selection stays execution configuration;
- the proposal separation-of-duties rule genuinely disappeared and needed a single canonical owner.

This is a correctness-preservation remediation, not a new context-optimization pass.

## Changes

### 1. Runtime Techplan references use semantic anchors

Canonical phase guidance that consumes `techplan.md` now refers to stable concepts such as:

- Rules & Validation;
- Decision Log;
- Implementation Details;
- Testing Checklist;
- Test Focus Pointer;
- Open Items.

It no longer depends on remembered template ordinals such as `§4`/`§12`/`§13` as runtime locators. When a human-facing review report needs section numbers, the review prompt resolves the current mapping from `template.md` at runtime.

Root `AUTHORING.md` records this as a general authoring rule, including the proven section-drift failure mode that justifies keeping the rule.

### 2. Independent Techplan review remains genuinely independent

`workflow/2-2-techplan-review-prompt.md` now requires an independent reviewer/actor context from primary synthesis. It does not require named models in phase policy. Exact model/client choice remains owned by execution configuration per proposal 0028.

### 3. Build report forcing function restored

`workflow/3-build-prompt.md` once again requires explicit report-level confirmation that race/concurrency, performance/load, and security-class tests were not executed inside the tight Build loop. If any were run, the report must name them and flag the scope deviation.

The existing Build checklist/guidelines boundary remains in place; this restores audit evidence rather than creating a new testing rule.

### 4. Historical workflow heading anchor restored

`workflow/README.md` again exposes `## What's Explicitly Out of Scope Here` as an addressable compatibility anchor for accepted historical proposals. The content stays compact and points at the current layering model rather than restoring old long-form prose.

### 5. Proposal separation of duties centralized

`proposals/README.md` now owns the rule once:

- a proposal author is not the approval authority for that proposal;
- explicit human-owner or independent authorized acceptance is required before merge;
- after approval, an authorized implementation actor may mechanically apply/merge the accepted change.

This replaces duplicated scoped wording while preserving the no-self-approval boundary.

## Explicit non-goals

This remediation does **not**:

- restore model-routing pointers to every generic phase prompt;
- redesign `best-practices/model-routing.md`;
- revert workflow-v2 progressive disclosure;
- re-expand compressed Techplan rules/guardrails that retained their semantics;
- restructure unrelated historical/example material;
- change `main`;
- modify Kencleng.

## Verification gate

Before treating workflow-v2 as frozen again:

1. compare the remediation result against the pre-remediation branch state;
2. confirm the intended runtime Techplan consumers no longer use drift-prone ordinal section references;
3. confirm the Build report contains the explicit heavyweight-verification scope confirmation;
4. confirm Techplan review requires independent actor/context without reintroducing phase-level model routing;
5. confirm the historical out-of-scope heading resolves again;
6. confirm proposal no-self-approval has one canonical owner;
7. confirm no unrelated workflow/context architecture was changed.

If those checks pass, the remediation commit becomes the new workflow-v2 validation baseline and supersedes `6edc1a6c9be10d54b3e37cc0c477c28790fcd81c` for future validation runs. Proposal 0031 remains the experiment design; this proposal records the pre-run correctness repair that reopened and then re-froze its original checkpoint.
