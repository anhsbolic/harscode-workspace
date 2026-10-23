# Outcome Selection

> Scope: Harscode Product guidance in the current branch. Product truth and consequential selections are owned by the target project; no change to operational main.

Phase: `PROD-SEL`. Output kind: `PROD-SELECTION` — Selected Product Outcome.

## Purpose

From connected Product Journeys and accepted value promises, select one meaningful, coherent, bounded Product outcome for elaboration. Selection is neither automatic roadmap ordering nor Engineering authorization.

## Selection tests

| Test | Question |
| --- | --- |
| Value | Does a real actor obtain a worthwhile outcome tied to accepted Product value? |
| Semantic sufficiency | Are actors, authority, truthful success, negative/unknown states and consequential claims clear enough to elaborate? |
| Dependencies | Do actual prerequisite behaviors exist, belong within this bounded outcome, or remain explicit blockers? |
| Truthfulness | Can its success be evidenced without treating seeded data, prototype, review, handoff or specification as delivery? |
| Boundary | Does it avoid absorbing unrelated reviews, financial states, recoveries or journeys? |

Product dependencies are a partial order, not a universal sequence. If a prerequisite is absent, either defer the outcome, include only its smallest coherent prerequisite, or mark the affected part blocked. Do not create misleading partial successes.

## Output and decision

Record the selected outcome, stable project-local outcome key, owner decision, current source revisions, why it provides value, real prerequisites and explicit exclusions. Keep the record small when a pointer into existing authority suffices.

Human selection authorizes Product elaboration only. It does not automatically approve the eventual Product Contract or any Design/Engineering assignment.

Next: Outcome Definition (`PROD-DEF`).
