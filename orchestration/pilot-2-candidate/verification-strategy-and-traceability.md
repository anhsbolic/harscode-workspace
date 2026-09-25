# Pilot #2 Candidate — Verification Strategy & Traceability

> Status: PILOT #2 CANDIDATE / NON-AUTHORITATIVE
> Scope: Group C checkpoint only. This document records CRTV conclusions about verification planning and traceability. It does not override canonical Techplan, Build, or Testing guidance.

## Purpose

Preserve Harscode's existing verification discipline while making execution evidence easier to trace and audit.

Core principle:

> Verification starts from a rule or risk, derives the evidence needed, assigns ownership, and only then selects the tool or technique.

```text
contract / risk
→ evidence obligation
→ primary owner
→ rationale / risk if skipped
→ tool / mechanism
```

A tool name is never sufficient authority by itself.

## Existing Harscode foundation

Current Techplan guidance already requires:

- every Rules & Validation rule to have verification coverage;
- a primary evidence owner: Build, Testing, or Human;
- a `Why this is worth running / risk if skipped` rationale;
- specialized concurrency/performance/security-sensitive Test Focus pointers with Exploration evidence anchors;
- non-trivial verification techniques to justify why they are appropriate.

Build and Testing guidance already separate fast edit-loop confidence from independent final/specialized evidence.

Pilot #2 should preserve and operationalize this structure rather than invent a second verification framework.

## Evidence ownership

### Build-owned evidence

Purpose:

> Make the implementation credible enough to hand off.

Typical characteristics:

- focused;
- low-cost enough for the edit loop;
- directly tied to the changed behavior;
- proves authored/changed tests are executable;
- avoids broad final-verification theater.

Build should not pull race/performance/security-class sweeps or broad final suites into every iteration merely for extra confidence.

### Testing-owned evidence

Purpose:

> Independently establish final/observable evidence that the approved contract is satisfied.

Typical characteristics:

- real-interface/runtime behavior;
- specialized risk verification;
- compatibility/migration/schema concerns;
- target-repo required final checks;
- gaps explicitly deferred from Build.

Testing should sweep current claims, not recreate equivalent coverage merely because it is independent.

### Human-owned evidence

Purpose:

> Preserve subjective/product/authority decisions that automation cannot legitimately decide.

Human-owned evidence remains external to agent verification and may not be auto-promoted to PASS.

## Specialized verification trigger

Specialized verification such as race/concurrency, performance/load, security scans, browser/rendered inspection, or other heavyweight techniques requires a concrete trigger.

Examples:

```text
shared mutable state / concurrency-sensitive behavior
→ scoped race or concurrency evidence
```

```text
material rendered/layout behavior
→ rendered/browser evidence
```

```text
latency/throughput requirement
→ concrete scenario + threshold + performance evidence
```

Do not reverse the relationship:

```text
Go project
→ therefore race test

frontend exists
→ therefore broad browser matrix

endpoint exists
→ therefore load test
```

## Traceability rule

A meaningful non-trivial verification command/check should be traceable to an approved obligation or current authoritative requirement.

Useful source coordinates include:

- Techplan Rule ID;
- Techplan Risk ID;
- Test Focus area/evidence pointer;
- target-repo required final verification;
- explicit current finding/gap requiring confirmation.

No additional verification-ID system is required for Pilot #2 unless real execution shows Rule/Risk/Test-Focus references are insufficient.

## Candidate execution evidence shape

For meaningful commands/checks, retain when practical:

```text
Command / check:
Purpose:
Obligation/source:
Authorization class:
Result:
Duration: <when useful>
```

Example:

```text
Command:
go test -race ./internal/domain/donation/...

Purpose:
verify shared-state behavior

Source:
Techplan Test Focus / RISK-4

Authorization:
PREAUTHORIZED specialized verification

Result:
PASS
```

Potential CRTV warning:

```text
Command:
go test -race ./...

Purpose:
extra confidence

Source:
none
```

## Verification expansion

A Verifier may discover that planned evidence is insufficient because the real implementation exposes a boundary or risk that lower-level evidence cannot prove.

When expansion is needed:

1. state what planned evidence cannot establish;
2. identify the concrete risk/observable claim requiring additional proof;
3. choose the smallest credible additional evidence;
4. record the expansion and its justification.

Routine, low-cost scoped expansion may remain inside Testing authority.

A material missing verification strategy, sensitive concern absent from the approved plan, or expansion that would effectively introduce a new risk/contract assumption should be reported as planning/authority drift rather than silently normalized.

## Missing-plan behavior

If Testing discovers an obviously material concurrency/performance/security-sensitive concern absent from the approved Test Focus/plan:

```text
do not invent planning history
→ report PLAN_GAP / Techplan drift
→ route through Orchestrator
→ reconcile upstream when material
```

Testing may still perform narrowly necessary diagnostic evidence when needed to establish the finding, but it must not hide the planning defect by silently converting the new strategy into ordinary Testing scope.

## Build vs Testing verification budget

No numeric budget is introduced.

Use semantic budgets:

```text
Build
→ focused edit-loop confidence

Testing
→ independent final/specialized evidence
```

Broad verification in Build requires a concrete reason such as target-repo authority, changed risk, or lack of any narrower credible proof.

## Re-entry

After a narrow patch:

- return first to the phase that raised the finding;
- verify the affected gap/finding first;
- broaden only when the patch changes scope/risk or invalidates wider evidence.

Do not replay unrelated expensive checks solely because a new Testing/Review Run exists.

## CRTV interpretation

Pilot #2 should evaluate verification quality from traceability, not from raw test count.

Useful questions:

- Did the command trace to a real rule/risk/repo requirement?
- Was the evidence owner appropriate?
- Was the chosen technique proportional?
- Did Testing expose a planning gap or silently compensate for one?
- Did broad verification materially improve proof, or merely increase ceremony?

A heavyweight check is not automatically wrong. An untraceable heavyweight check is a meaningful CRTV signal.
