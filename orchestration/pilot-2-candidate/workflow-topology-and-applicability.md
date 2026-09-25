# Pilot #2 Candidate — Workflow Topology & Phase Applicability

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group B checkpoint only. This document records CRTV conclusions about workflow topology and applicability. It does not override canonical `workflow/` guidance.

## Purpose

Preserve a conservative default lifecycle without turning workflow phases into ceremony.

Core principle:

> Workflow phases are specialized mechanisms invoked when their owned concern remains applicable; they are not milestones to collect.

The default engineering lifecycle remains a safe routing baseline:

```text
Exploration
→ Techplan
→ Build
→ Code Review
→ Testing
```

Optional/conditional phases remain inserted where their trigger applies.

The existence of a default route does not mean every phase is universally applicable to every Work Unit or every re-entry.

## Two distinct decomposition layers

### Orchestration decomposition

```text
Parent Outcome
→ Work Units
```

Owned by the Orchestrator.

Purpose:

- separate bounded delivery outcomes;
- expose causal dependencies/rendezvous;
- enable parallel or independently schedulable work;
- make ownership/completion conditions explicit.

This is coordination topology.

### Techplan decomposition

```text
Approved Techplan
→ execution task slices
```

Owned by the canonical Techplan decomposition workflow.

Purpose:

- reduce active Build/review context where a real boundary exists;
- separate independently executable/reviewable chunks;
- preserve dependency/risk/blast-radius boundaries inside one approved plan.

This is an intra-plan execution-context optimization.

The two layers may both exist, but neither implies the other.

A Work Unit with a cohesive Approved Techplan may correctly skip Techplan decomposition even when the Parent Outcome was already decomposed into several Work Units.

## Techplan decomposition applicability

Evaluate after Techplan approval and before Build dispatch.

Resolve to:

```text
REQUIRED
NOT_APPLICABLE
```

Use the canonical decomposition gate.

Typical REQUIRED signals:

- multiple independently useful execution/review chunks;
- meaningful hard dependency sequence;
- clearly separable component/layer scope;
- risk/blast-radius isolation;
- substantial unrelated implementation detail would otherwise share one Build context.

Typical NOT_APPLICABLE signals:

- the Approved Techplan is cohesive/linear enough for one Build context;
- proposed splits are trivial or merely file-based;
- document length is the only reason to split.

The actual decomposition workflow remains authoritative for generated task files and their invariants.

## Phase applicability ownership

Phase applicability is a coordination decision owned by the Orchestrator, grounded in canonical workflow rules and current durable evidence.

Participants may recommend a next phase, but they do not self-waive independent phases.

Human approval is not required for ordinary applicability routing unless the proposed decision would establish/change material authority, security/risk acceptance, or another Human-owned concern.

## Applicability timing

Use a hybrid model:

### At Work Unit creation

Record only expected/default lifecycle posture or known constraints when useful.

Do not prematurely lock all future phases.

### At the phase frontier

Resolve actual applicability just-in-time from current evidence.

Inputs include:

1. Work Unit outcome/completion condition;
2. current-effective Techplan/prior artifacts;
3. actual implementation/evidence state;
4. canonical workflow applicability/routing guidance.

If applicability changes materially, record the event and rationale.

## Applicability semantics

Canonical policy may call a phase conditional.

For a concrete Work Unit at a concrete frontier, resolve to:

```text
REQUIRED
NOT_APPLICABLE
```

Do not leave a concrete route indefinitely at `CONDITIONAL`.

Prefer `NOT_APPLICABLE` over vague `SKIPPED` language because the phase is not being casually waived; its owned concern has been evaluated and found not applicable.

## Burden of justification

Applicability is intentionally asymmetric:

> REQUIRED follows the conservative default cheaply; NOT_APPLICABLE bears the burden of explicit rationale.

When uncertain, prefer the independent phase rather than silently omitting it.

Examples of acceptable N/A reasoning may include:

- documentation-only correction with no executable behavior;
- generated/non-semantic output where an authoritative mechanism already proves the relevant contract;
- verification-only Work Unit with no implementation mutation.

“Simple change” alone is not sufficient justification.

## Code Review and Testing remain distinct

### Code Review

Owns independent reasoning against the current implementation/diff:

- safety;
- quality;
- stack-specific correctness;
- target-repo consistency;
- contract conformance.

### Testing

Owns independent empirical/observable verification:

- executable behavior;
- final evidence;
- deferred Testing-owned verification;
- real-interface/runtime claims;
- target-repo required final checks.

Review does not substitute for Testing; Testing does not substitute for Review.

For material production implementation changes, both remain conservative defaults.

## Code Review applicability timing

Evaluate after Build completes, because actual diff/change class is now known.

A plan that looked small may produce a broad/security-sensitive implementation; applicability should use the real implementation evidence rather than only the prior estimate.

## Testing applicability timing

Evaluate after Code Review closure, or after Build when Code Review has explicitly resolved to NOT_APPLICABLE.

For a Work Unit claiming executable/observable product behavior, Testing is normally REQUIRED.

NOT_APPLICABLE should be rare and evidence-backed, such as documentation/static metadata work with no runtime/behavior claim.

## Remaining-obligation routing

The Orchestrator should not blindly advance a pipeline.

At each Run boundary:

```text
reconcile current evidence
→ is Work Unit completion condition satisfied?
  ├─ yes → milestone/Human gate as applicable
  └─ no
      → identify remaining concern/proof obligation
      → evaluate the phase that owns that concern
      → dispatch REQUIRED phase or record evidence-backed N/A
```

Default lifecycle remains the routing baseline; remaining obligations determine the actual next phase.

## Patch and re-entry routing

A patch normally returns to the phase that raised the finding.

Examples:

```text
Code Review finding
→ Build/Patch
→ targeted Code Review confirmation
```

```text
Testing finding
→ Build/Patch
→ targeted Testing re-entry
```

Do not restart the whole downstream pipeline merely because a patch occurred.

Broaden to full Review/Testing only when the patch materially expands scope/risk, invalidates prior evidence, or changes a contract/assumption that requires broader reconsideration.

## Loop interpretation

A loop is not itself evidence of poor planning.

Classify the underlying cause.

Candidate categories:

- `IMPLEMENTATION_DEFECT` — ordinary code/design defect discovered downstream;
- `EVIDENCE_GAP` — behavior may be correct but required proof/harness is missing;
- `PLAN_GAP` — material execution/testability decision was absent upstream;
- `AUTHORITY_GAP` — material product/security/interface meaning is unresolved;
- `ENVIRONMENT_GAP` — runtime/tooling capability prevents credible verification.

Interpretation:

```text
implementation defect
→ normal patch/re-entry

evidence gap
→ normal closure work; may also be a planning learning

plan gap
→ reopen/reconcile Techplan as needed

authority gap
→ route to Human/project authority

same unresolved cause repeatedly
→ STALLED; diagnose instead of mechanically looping
```

Loop count alone is not a quality metric.

## CRTV note on Testing whole-Techplan reread

Current Testing guidance intentionally retains a fresh end-to-end Techplan consistency read during initial workflow-v2 validation.

Treat this as a conservative validation-era rule to reevaluate after enough CRTV evidence exists. It should not silently become permanent broad-read pressure merely because it was useful during early validation.

## Pilot #2 success signals

This candidate topology is working when:

- Work Units do not mechanically collect phases;
- independent Review/Testing are preserved where their concerns materially apply;
- N/A decisions are rare, explicit, and evidence-backed;
- participants cannot self-waive independent verification;
- narrow patches receive proportional confirmation instead of full ritual reruns;
- repeated loops can be diagnosed by cause rather than raw count;
- Techplan decomposition is invoked for real intra-plan execution benefit, not because decomposition exists as a phase.
