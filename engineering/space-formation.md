# Engineering Space — Formation and Contract Discipline

> **Status:** WORKING / RESEARCH-ONLY. Defines a design quality floor, not an executable Space runner.

## Meaning

A **Space** is one reusable, bounded production capability with a coherent external result and inspectable input/output contract. It is **not** an agent persona, a phase folder, an arbitrary engineering task, an orchestrator or a file-layout standard. Specific Specialists can collaborate *inside* a Space if justified by real responsibility boundaries.

Formation cost must be justified by actual need, reusable applicability and failure/consumer risk. For a small task, reuse an appropriately bounded capability or a permitted simpler path; do not form Spaces merely to populate a catalog.

## Formation decision

For a proposed reusable capability, document only what changes the decision:

1. **Demand/evidence:** the real repeated or consequential production gap, consumers, current alternatives and reason a separate capability adds value.
2. **Responsibility boundary:** the coherent externally useful result, what it cannot decide, what belongs to upstream Human/Product/Design and which risks require Human approval.
3. **Strict generic I/O:** required input classes and provenance, output meaning and verifiable completeness, producer/consumer roles, refusal, failure and partial-result semantics.
4. **Specialist composition:** only necessary internal responsibilities, locally applicable knowledge/guardrails, independent review requirements and quality/failure ownership. No universal role count.
5. **Runtime requirements:** source accessibility, scoped writes, source/revision handoffs, tool/model capability, authorization gates and observed evidence required from the selected harness.
6. **Human formation approval:** explicit exact definition revision, approved scope and owner. Definition approval alone does not authorize execution.

Keep reusable definitions **project-neutral but strict**. Project-specific API routes, policy, schema or feature choices belong in concrete assignment or target repository. Do not require a fixed PRD/TRD or one source-file format.

A Space may be technology- or framework-specific when that boundary materially improves correctness, effectiveness, or execution efficiency. Reusability is evaluated within the declared capability boundary; project-neutrality does not require technology-neutrality. Do not broaden a Space for hypothetical cross-technology reuse.

## Project standards take precedence over Space base knowledge

For **every** Engineering Space and Agent, reusable technical knowledge, architecture patterns, checklists, sample artifacts and preferred methods are **non-binding defaults**. Before choosing a method or representation, inspect the current target project's owning, effective, approved engineering/design standards, relevant code/conventions and explicit assignment constraints. **Follow applicable project-owned standards even when they contradict Space-local preferences.** Explain the selected project convention in output evidence; do not silently impose an alternative because the Space guidance calls it a best practice.

Distinguish accepted project policy from historical examples, incidental existing code, unapproved proposals and obsolete documents; those are evidence, not automatically binding standards. A project standard can choose technology, notation, API/schema source, error conventions and architecture *within delegated technical authority*, but does not override higher-priority Product/Design acceptance, applicable legal/security protections, protected-path permissions, explicit Space I/O obligations or Human approval gates. If an actual project standard appears to conflict with one of those **material** boundaries, record both exact source revisions, the affected risk and owner; stop only dependent action and seek the authorized Human/security/authority decision. Do not silently obey an unsafe instruction or silently replace project policy with Space taste.

Space-local examples and templates are selectable aids only; use the project's existing templates first where adequate. Record any material deviation and the authority that allowed it. This precedence rule applies regardless of whether the selected harness runs one Agent or several.

## Two separate compatibility checks

- **Generic compatibility:** Can output type/quality/standing from producer satisfy the downstream Space's declared input contract?
- **Bound compatibility:** Does this **actual**, current, accepted artifact revision from the project satisfy the downstream consumer's scope, source and security/acceptance obligations?

Both may be UNKNOWN. A plausible dependency graph is not a completed compatibility test.

## Human authorization and gates

The Human directly invokes the Coordinator with a bounded objective, pinned project/definition refs, allowed actions/tool/write paths, output/state destination and intended consumers. Balad may advise but never dispatch, coordinate or secretly amend the assignment.

Gates are **consequence-based**, not approval for every internal handoff. Human decisions are required for material Product/design authority choices, privilege/security/protected scope expansion, and final acceptance of a material downstream binding result. `supervised` progress review is not acceptance; any explicitly authorized autonomous mode still obeys consequential Human gates.

Revision-bound approval must include the exact affected source/action. Missing, stale or broader-than-authorized approval blocks the affected operation. Real native tool permissions must be checked; a textual guardrail alone is not enforced containment.

## Readiness and evidence

A formed Space is a declarative capability with formation approval, **not** proof of tool access, effective isolation, reviewer independence or output quality. Each concrete invocation needs reality-based readiness. Report `PARTIAL`, `BLOCKED` or `UNVERIFIED` when evidence is absent; do not invent a global scheduler, run registry or automatic orchestrator to paper over missing primitives.
