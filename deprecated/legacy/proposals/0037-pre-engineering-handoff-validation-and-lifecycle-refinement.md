# Refine pre-engineering handoff validation, scoped authority, and lifecycle tracking

**Status:** Accepted
**Date:** 2026-10-08
**Protection Tier:** general
**Triggered by:** Final C1 reconciliation after the first complete Kencleng pre-engineering route exposed four distinctions that the initial pre-engineering guidance did not state sharply enough: handoff preparation vs independent cold-start consumption, commitment-scoped binding authority vs whole-product authority, end-to-end commitment tracking without inventing post-engineering stages, and dashboard statuses that must be owned outside the dashboard.
**Target area:** pre-engineering
**Target file(s):**
- `pre-engineering/AGENTS.md` — add hard rules for scoped binding authority, cold-start validation distinction, and dashboard ownership discipline.
- `pre-engineering/README.md` — clarify authority model and validation/lifecycle semantics.
- `pre-engineering/commitment-route.md` — refine handoff exit so route completion means prepared + human-approved handoff, while independent cold-start consumption remains later validation evidence.
- `pre-engineering/control-tower.md` — allow end-to-end lifecycle observation without extending the pre-engineering stage model, and prohibit dashboard-only readiness/dependency status.

## Gap found

The first accepted `pre-engineering/` guidance correctly established that:

- route complete is not implementation or delivery;
- durable artifacts should remove dependency on remembered chat;
- a Control Tower is a derived dashboard, not Product Authority;
- downstream dependencies are not satisfied merely because an upstream handoff exists.

A final reconciliation of Kencleng C1 exposed four remaining ambiguities.

### 1. Handoff completion could be read as already empirically cold-start validated

Current `commitment-route.md` says the route is complete when a fresh engineering reader can begin without reconstructing the original chat.

That wording collapses two different facts:

```text
handoff prepared + human-approved
≠ independent cold-start consumption actually observed
```

Pre-engineering must be able to finish its packaging work before the next independent engineering session exists.

### 2. “Not canonical Product Authority” can be misread as non-binding

A project may deliberately keep whole-product Product Authority compact while approving commitment-specific product behavior and requirements that are binding for downstream work in that bounded commitment.

Shared guidance should permit:

```text
whole-product Product Authority
+
approved commitment-scoped behavior / requirements
→ downstream binding within scope
```

without requiring every commitment-specific detail to be promoted into whole-product canonical truth.

### 3. A Control Tower may need end-to-end commitment visibility

The current Control Tower guidance is framed primarily around the pre-engineering route.

A project may legitimately want to continue observing the same commitment through engineering and verified real-product behavior. This must not create artificial “Stage 8 / Stage 9” extensions to pre-engineering.

Engineering / verification state must come from owning engineering artifacts or evidence.

### 4. Dashboard-only statuses can become accidental authority

A dashboard can accidentally label future work BLOCKED, WAITING, ELIGIBLE, or dependent even when no owning artifact actually established that state.

The safer generic rule is:

> a dashboard may only reflect readiness / dependency states that have an owning artifact or evidence source; otherwise show PARKED / UNRESOLVED or omit the claim.

## Proposed change

### A. Scoped binding authority

Add to pre-engineering hard rules and scope guidance:

```text
Human-approved commitment-specific product behavior / requirements may be
binding for downstream work within that bounded commitment without becoming
whole-product canonical Product Authority.

The target project must make the scope and precedence explicit.

“Not whole-product canonical” must not be interpreted as “optional for engineering.”
```

This does not let Harscode create project Product Truth. It only preserves an authority shape a target project may explicitly establish.

### B. Separate handoff completion from cold-start validation

Refine the route:

```text
Durable handoff prepared + human-approved
→ PRE-ENGINEERING ROUTE COMPLETE

later:
fresh engineering session independently consumes handoff
→ COLD-START HANDOFF VALIDATION EVIDENCE
```

Cold-start validation is **not another pre-engineering stage**.

Route completion should require that the packet itself contains enough durable information for a fresh reader **by design**. The actual fresh engineering session then validates the claim empirically.

If that validation exposes a material missing decision or unusable handoff gap, feed the evidence back upstream and reopen only what is necessary.

### C. End-to-end lifecycle observation without new stages

Allow a Control Tower to show lifecycle fields beside the Stage 1–7 / commitment route, for example:

```text
overall commitment
pre-engineering route
engineering
cold-start handoff validation
verified real-product behavior
overall completion
```

These are lifecycle observations, not additional pre-engineering stages.

Rules:

- `ROUTE COMPLETE` means pre-engineering handoff complete only.
- `IN PROGRESS` may describe an overall commitment even when no phase is currently ACTIVE.
- engineering status is derived from engineering task artifacts / current workflow evidence;
- verified behavior status is derived from testing / delivery / real-product evidence;
- the dashboard never invents those states.

### D. Dashboard ownership discipline

Strengthen `control-tower.md`:

```text
owning artifact / evidence
→ persisted status
→ dashboard reflects
```

For readiness / dependency signals:

- ELIGIBLE requires an owning readiness decision;
- BLOCKED requires an owning blocker;
- WAITING requires an owning dependency state;
- dependency rails require an owning dependency relation;
- if a future commitment has not been re-gated / sequenced, use PARKED / UNRESOLVED or omit the stronger claim.

### E. Validation claim discipline

Add a conservative generic rule:

```text
one complete pre-engineering route
demonstrates pre-engineering route execution

it does not by itself prove:
- independent cold-start consumption;
- implementation / delivery correctness;
- real-product behavior preservation;
- universal validity of every exact artifact / stage mechanism.
```

## Rationale

These refinements preserve the original `pre-engineering/` model while tightening authority and validation semantics discovered by a real C1 reconciliation.

They avoid two opposite errors:

1. weakening commitment-specific approved behavior merely because it is not whole-product canonical authority;
2. overstating pre-engineering completion as engineering or end-to-end validation.

The Control Tower remains useful across lifecycle boundaries without becoming a new workflow owner.

No new artifact type, post-engineering stage model, or mandatory document consolidation is introduced.

---

*Human approval was given explicitly before creation of this proposal. Apply the accepted changes to the target guidance and keep this proposal as changelog evidence.*
