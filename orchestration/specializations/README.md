# Role Specialization Routing

Specialization refines a canonical Role for project/runtime routing. It does not create authority and does not own the guidance it references.

Example:

```text
Role: Implementer
Specialization: frontend
```

A project may provide a specialization index that points to relevant authorities such as:

```text
frontend
→ framework best practices
→ browser/security guidance
→ frontend testing guidance
→ client architecture
→ applicable Project Learning
```

The referenced sources remain owned by their original concern.

## Retrieval rule

Use:

```text
Role
+ Specialization
+ Task scope
+ Workflow phase
→ relevant routing index/subindex
→ minimum applicable guidance
```

Do not load all specialization-linked documents merely because the specialization matches.

Harscode core intentionally does not standardize project-specific specialization names or physical index locations in v0.1.
