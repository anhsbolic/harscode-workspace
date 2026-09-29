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

**Status:** `OBSERVED`

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
Kencleng Pilot #2 repeated updates to `manifest.md`, `control-surface.md`, Work Graph, Events, and `kencleng-development-tracker.md`.

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

**Status:** `OBSERVED`

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
Kencleng Pilot #2 bounded Slice 2 readiness reconciliation.

### SR-005 — Slim Work Unit manifest historical narrative

**Status:** `OBSERVED`

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
Kencleng Pilot #2 `WU-S2-002/manifest.md` growth.

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
