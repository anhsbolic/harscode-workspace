# Independent Security Specialist — Risk-Based Assessment Reference

> **Type:** Non-binding Agent-owned practice. Effective project security policy, law, approved Engineering Standards and protected-path rules prevail; this reference does not approve exceptions or establish runtime security testing.

## Assess boundary before control

- Establish actor/principal, trusted decision-maker, resource ownership, data sensitivity, input provenance and authorization point from effective originals.
- Review privilege escalation, insecure direct object/resource access, identity spoofing, replay/duplicate submissions, lost response, inconsistent state, exposure/logging of sensitive information and unsafe defaults **only where plausible for the actual solution**.
- Distinguish authentication from per-resource authorization; client affordance is not enforcement. Review concrete O2 negative/result semantics and O3 claims together.
- For an Engineering Standards revision, evaluate wider consumers, backward compatibility, default secure configuration, mitigation, migration and rollback implications.
- State actual evidence: design inspection is not implementation security verification, threat-model discussion is not pen testing, and an Agent label is not context isolation.
- Prefer the least complexity that meets the material threat/risk and binding security floor; do not mandate a framework, service or security tool absent justification.

## Findings and independence

Record affected original and output/standard revisions, risk/consequence, concrete evidence, producer correction requested, verification obligation and disposition (open, addressed-with-evidence, unresolved or not-assessed). Reinspect only changed material edges. Do not author fixes to the same artifact under independent review; do not certify your own output. Escalate consequential risk acceptance to Human through Coordinator, not through unilateral policy change.

[Actor contract](agent.md) · [Space handoff](../../contracts.md)
