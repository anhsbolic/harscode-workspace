# Solution Reviewer — Agent-Owned Best Practices

Focused review techniques for multi-contract solution correctness.

## Independent source comparison

- Review from original approved acceptance criteria, then inspect producer outputs. A producer's traceability claim is **hypothesis** until independently checked.
- Use bidirectional mapping: each source requirement must have outcome/verification coverage; each output decision must have a source authority or legitimate delegated design rationale.
- Separate missing material content from intentionally delegated implementation details.
- Check stale reference, version mismatch, unapproved Human decision, out-of-scope addition and undocumented consumer dependency.

## Boundary consistency checks

- A success response/state must require all necessary authoritative conditions; verify errors, partials and conflicts cannot yield equivalent successful meaning.
- Client-visible affordances never replace server authorization for protected actions.
- Trust/provenance labels must match evidence sources, not merely internal role grants.
- Verify that interface types and error states have real producers/consumers and compatible ownership. Security and persistence obligations need an eventual test owner.

## Evidence economics

- Design review evidence is neither executing tests nor proving a feature works.
- For each material requirement ask: what is observable, by whom, against what original authority and environment, and what would disprove it?
- Demand additional analysis only when it changes an actual decision or safeguards an important risk. A short high-quality finding is better than an exhaustive generic checklist.

No central Best Practices index is required by default. Current project guardrails and Space contract remain binding irrespective of duplicated Agent knowledge.
