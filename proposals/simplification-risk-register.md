# Harscode Simplification Risk Register

> Status: NON-AUTHORITATIVE / EVIDENCE HOLDING AREA
> Scope: Global Harscode
> Purpose: preserve promising simplification ideas that may reduce complexity, ceremony, artifact overhead, execution cost, or coordination friction, but are not yet proven safe for correctness or quality.

## Governing principle

**Simplification is subordinate to correctness.**

Do not adopt a simplification merely because it reduces files, Runs, prompts, handoffs, or coordination steps.

A candidate simplification may advance only when available evidence gives sufficient confidence that it preserves the properties that matter for the actual problem, including:

- semantic correctness;
- authority integrity and explicit decision ownership;
- durable reconstructability;
- verification and review quality;
- failure/blocker visibility;
- output and outcome quality;
- provenance needed for later reconciliation.

When the safety case is uncertain, keep the safer current mechanism and gather more evidence.

This register is not canonical guidance, not an approved implementation backlog, and not permission to weaken existing safeguards. An item becoming attractive or repeatedly discussed does not promote it automatically.

## Status

Use one of:

- `OBSERVED` — real cost/friction is evidenced, but the simplification is still loosely framed;
- `EXPERIMENT_CANDIDATE` — a bounded reversible experiment can test the simplification;
- `TESTING` — an experiment is active;
- `SAFE_TO_ADOPT` — evidence is sufficient to propose/adopt through the applicable Harscode change path;
- `DEFERRED` — worth retaining, but not worth testing now;
- `REJECTED` — evidence shows the simplification weakens required quality/correctness or does not pay for itself.

## Candidate template

### SR-XXX — <title>

**Status:** `OBSERVED`

**Observed cost**  
What real overhead, ritual, duplication, or coordination friction has been observed?

**Candidate simplification**  
What could be reduced, collapsed, removed, or made optional?

**Expected benefit**  
What concrete value should improve?

**Correctness / quality risk**  
What could become less correct, less reconstructable, less reviewable, less visible, or lower quality?

**Safety conditions**  
What invariants/evidence must remain true before adoption is safe?

**Cheap reversible experiment**  
How can the idea be tested without committing Harscode broadly?

**Evidence**  
Pointers to CRTV observations, Runs, artifacts, or other concrete evidence.

---

## Bounded CRTV experiment — current-state simplification

The three current `EXPERIMENT_CANDIDATE` items below share one evidence
question:

> Can Harscode reduce duplicated current-state/readiness narrative while a fresh
> Orchestrator still reconstructs the same current frontier, blockers, authority
> state, and next action without hidden conversational context?

Do **not** test all removals at once. Use staged ablation so any quality loss can
be attributed to a specific simplification.

### Experiment comparison boundary

The experiment is **revision-bound and non-blocking**.

A baseline must record the target project revision/state it reconstructed.
Subsequent ablation stages compare against that same revision/state, even if
normal Pilot work has already moved the live branch forward.

Conceptually:

```text
target project @ revision X
├── Stage A — normal artifact set
├── Stage B — same revision X, readiness artifact excluded
├── Stage C — same revision X, one convenience projection excluded at a time
└── Stage D — same revision X, compact derived Work Unit representation
```

Do not regenerate Stage A merely because normal project state changed after the
baseline was captured. A new baseline is justified only when deliberately
starting a new experiment cohort on a new revision.

The simplification experiment must not become a critical-path gate for ordinary
Pilot work. Normal orchestration may continue after the baseline is captured;
ablation stages may later inspect the immutable prior revision/state.

### Experiment sequence

**Stage A — Baseline reconstruction**

Run a fresh Orchestrator reconstruction against the current project state using
the normal current artifact set.

Capture only the observable result needed for comparison:

- current Parent Outcome / active Slice;
- active Work Unit and current execution/scheduling/horizon;
- current Run or next runnable route;
- active blockers and exact affected scope;
- authority gaps / Human decisions actually needed now;
- current-effective contract / milestone posture;
- next action;
- any uncertainty or artifact conflict encountered.

This is the control. Record the exact target project revision/state used for the reconstruction. Do not mutate project artifacts merely for the baseline.

**Stage B — Readiness-artifact ablation (`SR-004`)**

Repeat fresh reconstruction without relying on a dedicated
`readiness-reconciliation.md`-like artifact.

The Orchestrator must reconstruct readiness from the actual current owners:
Authority Map, Profile Registry/definitions, runtime config, Work Graph, Work
Unit current state, Events, and current-effective workflow/project artifacts.

Pass only if the result is materially equivalent to Stage A and no important
readiness gap becomes ambiguous.

**Stage C — Projection ablation (`SR-002`)**

Repeat reconstruction while treating one convenience projection at a time as
unavailable/stale, starting with the projection that has the least unique
semantic ownership.

Do not remove the semantic owner. Test examples one at a time:

- project tracker detailed current-Slice narrative unavailable while its coarse
  cross-slice state remains available;
- Control Surface unavailable while Work Graph + Work Unit current state +
  open Decisions/Blockers remain available.

Pass only if current orchestration truth remains reconstructable and Human
situational awareness is not materially degraded.

**Stage D — Slim Work Unit representation (`SR-005`)**

Create a **derived experiment-only** compact representation of one current Work
Unit. Do not replace the authoritative project artifact during the test.

The compact form should retain:

- stable identity / outcome / scope / completion condition;
- current execution/scheduling/horizon;
- current Run or next route;
- active Human gate / authority sync;
- active blockers with affected scope;
- current-effective milestone/contract pointers;
- minimum evidence pointers needed to justify current state.

It should omit completed-Run narrative and long historical artifact inventories
that are already owned by Events / Run evidence.

Give the fresh Orchestrator the compact representation instead of the verbose
one and compare with Stage A.

### Pass criteria

A simplification candidate passes its stage only when all of these remain true:

1. **semantic equivalence** — no materially different current-state conclusion;
2. **authority integrity** — no owner/scope/decision is invented or lost;
3. **blocker fidelity** — exact affected scope and safe unaffected work remain
   discoverable;
4. **frontier fidelity** — the same next runnable route / Human gate is derived;
5. **provenance sufficiency** — the current truth can still be justified from
   durable pointers without broad historical archaeology;
6. **Human usability** — the result can still be explained concisely without
   needing the Human to reconstruct missing orchestration state;
7. **failure visibility** — ambiguity/staleness/conflict becomes visible rather
   than silently guessed.

### Failure criteria

Treat the experiment as failed for that simplification when any of these occurs:

- fresh reconstruction produces a materially different frontier or blocker;
- a valid Decision/authority context becomes difficult to locate or is
  mis-scoped;
- the Orchestrator must scan large historical Run sets merely to understand
  current truth;
- Human situational awareness materially worsens;
- a supposedly redundant artifact turns out to carry unique current semantics;
- the Orchestrator needs remembered chat/history to compensate for the removed
  surface.

On failure, keep the safer existing mechanism and record the missing capability.
Do not compensate by adding a new mirror/projection unless the evidence points to
a real owner gap.

### Evidence discipline

- Keep project canonical/current artifacts unchanged for the tested revision;
  use read-only/derived experiment inputs for ablation.
- Bind Stage A/B/C/D comparisons to the same target project revision/state.
- Do not regenerate a baseline solely because normal Pilot work advanced the live
  branch after Stage A.
- Do not block ordinary Pilot execution while waiting for later ablation stages.
- Use fresh-session reconstruction; prior chat memory must not be part of the
  test.
- Run one ablation at a time.
- Record the smallest useful comparison evidence; the experiment itself must not
  create another large artifact ecosystem.
- Passing one project/Work Unit is evidence, not universal proof. Promotion to
  `SAFE_TO_ADOPT` requires enough CRTV evidence for the actual scope of the
  proposed Harscode change.

## Current candidates

### SR-001 — Reduce default Run artifact count

**Status:** `OBSERVED`

**Observed cost**  
Pilot #2 produced Runs where invocation, multiple stage-evidence files, resolution/decision briefs, and terminal handoff repeat overlapping context and outcomes.

**Candidate simplification**  
Test a smaller default durable Run package, potentially `invocation.md` plus one structured terminal result/handoff, with extra evidence files created only when materially useful.

**Expected benefit**  
Lower documentation burden, less duplicated prose, easier reconstruction, and less synchronization work.

**Correctness / quality risk**  
Collapsing artifacts may hide evidence provenance, weaken phase-specific accountability, or make later review/reconstruction harder.

**Safety conditions**  
Assignment truth, execution evidence, decisions, blockers, verification status, provenance, and next-route evidence must remain deterministically reconstructable.

**Cheap reversible experiment**  
Use one low-risk bounded Run with a compact result artifact while preserving all required semantic fields, then compare reconstruction/review quality against existing multi-file Runs.

**Evidence**  
Kencleng Pilot #2 `WU-S2-002` artifact growth and repeated Run-local summaries.

### SR-002 — Reduce duplicate current-state projections

**Status:** `EXPERIMENT_CANDIDATE`

**Observed cost**  
The same coordination changes are repeatedly reflected across Work Unit manifest, Control Surface, Work Graph, Events, and project tracker, creating update cost and drift opportunities.

**Candidate simplification**  
Identify one owning current-state source per concern and make convenience views explicitly derived/optional where possible.

**Expected benefit**  
Less synchronization ceremony and fewer stale competing summaries.

**Correctness / quality risk**  
Removing or weakening a projection may reduce Human situational awareness or make fresh-session reconstruction harder if the supposedly owning source is not actually sufficient.

**Safety conditions**  
Current state and history must remain unambiguous; Human-facing continuation must remain easy to understand; every removed projection must have a verified replacement path.

**Cheap reversible experiment**  
For one Work Unit, classify each current file as authority/current-state/history/projection and test reconstruction without relying on one candidate redundant projection.

**Evidence**  
Kencleng Pilot #2 repeated updates to `manifest.md`, `control-surface.md`, Work Graph, Events, and `kencleng-development-tracker.md`. A current artifact audit found that the project tracker has a defensible unique coarse cross-slice role, but its detailed Slice-2 Run/frontier narrative substantially overlaps the Work Unit manifest, Control Surface, Work Graph, and Events. After `OIR-S2-002-006`, one Orchestrator reconciliation updated Event, manifest, Work Graph, Control Surface, Parent Outcome, and tracker; the observed end-to-end handoff took roughly 20 minutes, with tool/network latency not isolated. Treat the duration as supporting friction evidence, not proof of a model/runtime performance defect. Current candidate guidance now defines explicit ownership boundaries; the remaining safety question is whether thinner projections preserve fresh-session and Human situational awareness in real use.

### SR-003 — Allow related decision surfaces to remain in one Run longer

**Status:** `OBSERVED`

**Observed cost**  
Some simple or tightly related issues were split across multiple Explorer/Planner Runs and Human handoffs even when the same bounded objective, context, and authority owner remained available.

**Candidate simplification**  
Permit one execution occurrence to resolve multiple closely related concerns while Role, scope, authority, context fitness, and independence requirements remain valid.

**Expected benefit**  
Fewer context resets, fewer handoffs, faster resolution of straightforward issues, and better Human pairing flow.

**Correctness / quality risk**  
Over-combining work can blur Role boundaries, hide meaningful scope expansion, reduce independent review, or make decision provenance ambiguous.

**Safety conditions**  
Meaningful scope changes, Role changes, independent-review obligations, authority mismatches, or degraded context must still force an appropriate boundary.

**Cheap reversible experiment**  
Run a bounded related decision cluster in one Participant Session and compare clarity, provenance, and outcome quality with prior split-run patterns.

**Evidence**  
Kencleng Pilot #2 repeated O2/O3 and adjacent Open-Item routing.

### SR-004 — Make dedicated readiness artifacts optional

**Status:** `EXPERIMENT_CANDIDATE`

**Observed cost**  
A dedicated readiness-reconciliation artifact was useful during Pilot #2 transition, but could become a repeated ceremony if treated as mandatory for every Slice.

**Candidate simplification**  
Treat readiness reconciliation as required behavior/invariant while allowing the evidence to live in existing durable state/events unless a dedicated artifact adds material value.

**Expected benefit**  
Avoid a new per-Slice documentation ritual.

**Correctness / quality risk**  
Without a dedicated record, authority/profile/readiness gaps may become harder to audit or reconstruct.

**Safety conditions**  
The resulting readiness state, gaps, decisions, and next frontier must remain durably discoverable.

**Cheap reversible experiment**  
On a later bounded Slice, perform readiness reconciliation without a dedicated file and test fresh-session reconstruction.

**Evidence**  
Kencleng Pilot #2 bounded Slice-2 `readiness-reconciliation.md` was valuable as transition evidence: it proved reuse of the existing foundation, bounded authority mapping, and the five-profile baseline. After readiness, however, the same artifact also restated Authority Map, Profile Registry, Work Unit/frontier, and projection-sync state that have narrower current owners. This supports treating readiness as behavior/invariant and any dedicated file as a one-time checkpoint rather than a live projection. The no-dedicated-file path still needs a later fresh-session reconstruction test before `SAFE_TO_ADOPT`.

### SR-005 — Slim Work Unit manifest historical narrative

**Status:** `EXPERIMENT_CANDIDATE`

**Observed cost**  
The current Work Unit manifest has accumulated long summaries of completed Run outcomes already represented by Run artifacts and Events.

**Candidate simplification**  
Keep Work Unit manifest focused on stable definition plus concise current state and pointers; leave chronology/detail to Events and Run-owned evidence.

**Expected benefit**  
Smaller current-state surface, less duplication, and easier fresh reconstruction.

**Correctness / quality risk**  
Over-thinning the manifest may force expensive traversal across many historical artifacts to understand why current state is valid.

**Safety conditions**  
The manifest must still expose enough provenance/pointers to reconstruct current truth without ambiguity.

**Cheap reversible experiment**  
Produce a compact derived version of one existing manifest and test whether a fresh Orchestrator can reconstruct the same frontier and blockers.

**Evidence**  
Kencleng Pilot #2 `WU-S2-002/manifest.md` is ~16 KB and includes a long current-effective prior-artifact inventory plus completed-Run routing narrative already recoverable from Run evidence and Events. Current candidate guidance now defines the manifest-like record as concise current truth with enough provenance. A bounded slim-manifest reconstruction test is now well-defined; safety is not yet proven, so this remains below `SAFE_TO_ADOPT`.

### SR-006 — Compress stage-specific Explorer evidence

**Status:** `OBSERVED`

**Observed cost**  
Explorer Runs can produce separate Stage 2/Stage 3 evidence plus a decision brief and handoff, sometimes with overlapping context.

**Candidate simplification**  
Allow stage evidence to share one structured artifact when the distinction does not require separate durable ownership/provenance.

**Expected benefit**  
Less writing and fewer files while preserving the reasoning trail.

**Correctness / quality risk**  
Stage boundaries, Human gates, unresolved Findings, or evidence-to-recommendation provenance may become less visible.

**Safety conditions**  
Stage completion, Human confirmation, findings, evidence, recommendations, decisions, and unresolved blockers must remain explicit.

**Cheap reversible experiment**  
Use a single structured Explorer result on a low-risk bounded decision surface and audit it against canonical stage requirements.

**Evidence**  
Kencleng Pilot #2 OIR Run artifact patterns.
