# Proposal: Separate orchestration current state, history, and projection

> Status: Proposed
> Date: 2026-09-25
> Protection Tier: general
> Triggered by: Kencleng Orchestrator Pilot #1 CRTV review (state/projection drift)
> Target: orchestration/protocol-v0.1.md; orchestration/AGENTS.md

## Friction Found

Pilot #1 exposed a structural ambiguity in Orchestrator Protocol v0.1: the protocol says current state must be reconstructable and that the Control Surface is only a projection, but it does not define a single durable ownership model for current Work Unit state versus historical transitions.

In the Kencleng Pilot #1 Harscode Space this produced contradictory durable records:

- Work Unit manifests retained early header values such as `Status: NOT_STARTED` while later appended sections said the same Work Unit was `DONE`;
- the Control Surface contained both stale `NOT_YET_APPROVED` wording and the later `SLICE_FINALIZED` state;
- one Work Unit used `Scheduling: DONE`, even though `DONE` is not a valid scheduling enum;
- readers and a future Orchestrator would need to infer current truth from prose chronology instead of reading one current value.

This is not a copy-editing issue. A dedicated Pilot #2 Orchestrator must be able to reconstruct current state deterministically without chat history or manual interpretation.

## Proposed Change

### 1. Add `Work Graph` as an orchestration object

Add to `protocol-v0.1.md` Core objects:

```markdown
- **Work Graph** — current cross-Work-Unit coordination topology: known Work Units, canonical HARD/SOFT dependency edges, and produced milestone/rendezvous conditions. It coordinates outcomes; it does not own implementation detail.
```

Cross-Work-Unit dependency topology has one canonical owner. A Work Unit record may display a derived dependency summary, but it must not become an independently maintained second dependency truth.

### 2. Separate Work Unit Definition from Current State

Clarify the Work Unit contract conceptually as:

```text
Work Unit
├── Definition
│   ├── ID / title / type / parent
│   ├── outcome / scope
│   ├── completion condition
│   └── coordination ownership
└── Current State
    ├── execution status
    ├── scheduling state when active/applicable
    ├── horizon / readiness
    ├── current Run / milestone
    ├── Human gate / authority sync
    └── active blocker
```

Definition describes what the Work Unit is. Current State describes what is true now.

### 3. Add the single-current-value invariant

Add a hard semantic rule:

> For every current-state field there is exactly one current value. Updating current state replaces that field's prior current value; historical values must not remain as competing current-state sections in the same record.

The concrete storage format remains project-defined.

### 4. Make Events the history boundary

Clarify that material historical transitions belong in append-only Events, for example:

- Run dispatched/completed/failed;
- Work Unit state transition;
- Human Decision recorded;
- Blocker opened/closed;
- milestone promoted;
- Work Graph structurally amended.

Events explain how current state was reached. Events are not the current state themselves.

Detailed command/read telemetry remains Run-local rather than being copied into the global Event history.

### 5. Tighten Control Surface semantics

Clarify:

```text
Work Graph + Work Unit Current State + open Decisions/Blockers
→ Control Surface
```

The Control Surface is a regenerable cache/projection for Human/operator use. If it conflicts with the underlying current state, the projection is stale and must be regenerated; it does not win by recency or wording.

### 6. Resolve terminal scheduling ambiguity without adding a new enum

Keep the existing active scheduling enum:

```text
PARKED | QUEUED | DISPATCHED | RUNNING
```

Clarify that scheduling describes active scheduling posture only. When a Work Unit is terminal (`DONE` or `CANCELLED`), it has no active scheduling posture in the semantic model. A concrete representation may omit/null/mark the field non-applicable, but must not invent a terminal scheduling value such as `DONE` unless the protocol later explicitly adds one.

This deliberately avoids prematurely adding another scheduling enum during P0 remediation.

### 7. Strengthen the orchestration router hard rule

Update `orchestration/AGENTS.md` hard rules to make the reconstruction boundary explicit:

```markdown
- Keep Work Unit definition, current state, append-only history, and Control Surface projection semantically separate. Current-state fields have one active value; historical transitions belong in Events.
- Cross-Work-Unit dependency topology is owned by the Work Graph; do not create a second independently maintained dependency truth inside Work Unit records.
```

## Explicitly Not Proposed

This proposal does **not** standardize:

- a mandatory `.harscode-spaces/` directory layout;
- `manifest.md`, `events.md`, YAML, JSON, or database serialization;
- exact field names for Pilot #2 files;
- a state database or schema engine;
- launcher/process state representation;
- a new scheduling enum.

Those remain Pilot #2 implementation hypotheses until real execution provides evidence.

## Rationale

The protocol already requires current state to be reconstructable and the Control Surface to be derived. Pilot #1 showed that those principles are insufficient without a durable state/history ownership boundary.

The minimum reusable invariant is:

```text
Definition ≠ Current State
Current State ≠ Event History
Event History ≠ Projection
Projection ≠ Authority
```

Adding Work Graph ownership also prevents dependency truth from being duplicated across sibling manifests and a coordination map.

This is the smallest semantic promotion that makes a dedicated Orchestrator deterministic while leaving exact Pilot #2 storage mechanics open to CRTV.

---

*After human review: update the Status above. If Accepted, apply the semantic changes to the target orchestration guidance and retain this proposal as changelog evidence.*
