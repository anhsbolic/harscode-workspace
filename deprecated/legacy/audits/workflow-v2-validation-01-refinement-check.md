# Workflow-v2 Validation #1 Refinement Check

> Date: 2026-09-15
> Scope: post-Validation-#1 refinements applied after `workflow-v2@07a51a93100afeb4e78b5124d64decae62679f6f`
> Evidence source: `audits/workflow-v2-validation-01-retrospective.md`
> Accepted proposals: `0032`, `0033`
> Purpose: targeted consistency check before freezing the next workflow-v2 validation candidate

## Result

**PASS — no blocking consistency issue found in the accepted refinement scope.**

This check is not a second broad pre-validation audit. It verifies that the evidence-backed changes preserve the existing workflow-v2 architecture instead of accidentally creating new lifecycle machinery or weakening independence/correctness boundaries.

## Scope check

Changed areas are limited to:

- workflow artifact provenance / phase handoff;
- Techplan synthesis/template/report routing and verification metadata;
- Build/Review/Testing verification ownership boundaries;
- Codex session/permission/benchmark translation;
- retrospective/proposal evidence.

No target-project product behavior is encoded into portable runtime guidance. Kencleng-specific facts remain in retrospective/proposal evidence only.

Harscode `main` remains untouched at `fbeb2e657e1258c5c45dc5f70518acd7f915baa8`.

## Invariant checks

### 1. No new lifecycle phase

PASS.

Patch remains Build/Patch authority. No creative-design phase, benchmark phase, or mandatory Techplan-review/decomposition phase was introduced.

### 2. Techplan remains the execution-grade authoritative spine

PASS.

The template gains provenance and verification ownership/rationale but retains Rules & Validation, Decision Log, risks/contracts, Testing Checklist/Test Focus Pointer, Open Items, and the existing decomposition spine invariant.

The proportional-planning language explicitly preserves the rule that material product/domain, authority/security, architecture/ownership, interface/data, irreversible-operation, risk/verification, and blocking human decisions must be resolved before Build.

### 3. Techplan review/decomposition remain optional

PASS.

Synthesis now emits early `Skip | Recommend/Consider` routing so the operator need not invoke a mechanism merely to discover it adds no value.

The independent review prompt retains its own Complex gate and remains Draft. Decomposition retains its post-Approval gate and no-split-by-size rule.

### 4. Review and Testing independence remain intact

PASS.

Code Review remains a fresh independent four-pass inspection and cannot edit production code. The new verification posture allows targeted repro to substantiate a finding but rejects blanket final-suite replay by default.

Testing remains independent final verification, retains `SWEEP, DON'T REDO`, exact Test Focus evidence anchors, final target-repo commands, backward-compatibility checks, and the deliberately conservative fresh whole-Techplan read during initial workflow-v2 validation runs.

### 5. Build still verifies implementation without becoming final Testing

PASS.

Build still runs ordinary fast verification and must prove newly authored/changed tests are executable. Broad Testing-owned or heavyweight race/perf/security verification is no longer encouraged as confidence theater; it can still run when target-repo authority, changed risk, or credible evidence requires it.

Patch re-entry returns to the requesting phase and reruns affected verification first. This narrows repetition without suppressing final verification.

### 6. Phase handoff preserves durable routing and improves human actionability

PASS.

The standard handoff now separates:

- `Human decision` — action a person must decide now;
- `Open / deferred` — non-blocking unresolved/deferred state;
- `Session transition` — plain-language continue/fresh/return-to-Build action + reason.

Portable CONTINUE/FRESH/BUILD-authority semantics remain defined in context management; only the human-facing rendering changed.

### 7. Provenance does not become a second policy/version system

PASS.

Workflow-generated artifacts record known author/phase/time and optional safe harness metadata. Unknown values are not invented. Account/credential identifiers are excluded. Git history remains the default version history.

The externally hosted PR-description template was intentionally not burdened with duplicate harness provenance in this refinement: GitHub already owns PR author/time/history and model/session telemetry remains task/harness observability unless a project explicitly requires it in the PR body. Internal workflow task artifacts are the provenance target validated here.

### 8. Benchmark telemetry remains outside workflow correctness artifacts

PASS.

`harness-optimization/codex/benchmarking.md` defines session-level before/after observability and quality pairings without making token/allowance telemetry a required Exploration/Techplan/Build/Review/Testing artifact.

### 9. Codex safety guidance remains proportional

PASS.

The harness translation does not blanket-ban Git/workspace work. It distinguishes ordinary authorized operations from materially destructive/irreversible actions, while deferring actual protected paths and concrete config syntax to target-project/current-Codex authority.

## Known limitations / next evidence needed

- Validation #1 benchmark lacks a pre-Exploration snapshot and combines Exploration + Techplan + decomposition in one measured session.
- Proposal 0033 changes a protected Techplan surface from one real validation because the issue is structural; it still needs a different real task before any promotion to `main`.
- The independent Techplan review prompt still requires 2+ real Complex-tier validations before it should be considered a stable mandatory mechanism.
- Verification-ownership guidance should be judged by whether the next run preserves defect-finding signal while reducing unjustified repeated suites; do not infer success merely from the text change.

## Candidate freeze rule

Treat the commit containing this check as the next **workflow-v2 validation candidate**. Do not continue speculative cleanup before the next real task.

Change this candidate only if a pre-run correctness problem is found or the next validation produces concrete evidence of a gap, repeated ambiguity, or unnecessary work.
