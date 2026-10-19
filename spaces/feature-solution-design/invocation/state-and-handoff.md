# S1 Invocation State and Handoff — Proposed

**State is an evidence/continuity requirement, not a scheduler or global state machine.** A fresh Codex session should reconstruct the next safe action from durable project output plus a small current-effective invocation record.

## Authority separation

- **Definition:** Harscode `spaces/feature-solution-design/` at pinned approved Git commit, with Agent packages, contracts and harness guidance.
- **Project truth/accepted solution:** target project repository at explicit output path/revision. Material decisions become project-binding only with valid project/Human authority.
- **Active coordination:** one small current-effective invocation record at an **approved writable location**; possible `harscode-state/` only if actually present, accessible and explicitly authorized. No assumption it is initialized.
- **Chat/session transcripts:** optional evidence, not current-effective truth.

## Minimum reconstructable record

Record the invocation's actual ID/reference or descriptive key, Space definition SHA, target repo/ref/SHA, source authority refs, assignment scope and approved write locations, Human invocation/privileged gates, chosen agents/model+efforts with actual availability evidence where performed, current accepted intermediate/final artifact refs, blocking facts/findings, next owner/action and last checked revisions.

Do not invent runtime statuses. Describe observed `not started`, `in progress`, `awaiting decision`, `delivered/reviewed` and `blocked` in prose. `COMPLETE`/etc. describe output conformance separately. A row of checkboxes is not proof of a tool invocation.

## Recovery and change

1. Inspect current target repo and Space definition revision. Locate the actual invocation state owner and existing accepted output refs; if none exists, do not pretend continuity.
2. Compare current sources with pinned input revisions. Material upstream change → Balad coordinates rebind/review; Specialist cannot silently substitute new authority.
3. Resume only from accepted artifacts and revalidate changed dependencies, scoped authorization, model availability and affected reviewer checks. Do not rely on a prior chat's implicit agreement.
4. If a material artifact is missing/unreadable, report blocker and owner; don't reproduce imagined decisions to fill a gap.

## Handoff record (on meaningful boundaries only)

```text
Space definition revision:
Project input revision:
Completed output refs + actual checks:
Produced but unverified/partial refs:
Open blockers and affected consumer:
Human decision/approval required:
Current invocation state owner/ref:
Next authorized action + owner:
```

When no current-effective state storage path is available, submit a concrete proposed path for Anhar approval at preflight. Never create a central Run registry, workspace root state or project truth mirror merely to satisfy this template.
