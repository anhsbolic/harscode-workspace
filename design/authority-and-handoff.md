# Design Authority and Engineering Handoff

> **Status:** WORKING / RESEARCH-ONLY. Decisions belong to the target project and are approved by its authorized Human.

## Establish authority by concern

Do not accumulate conflicting generations of tokens, prototypes, interaction rules, asset directions and old UI guidance as simultaneously current. Identify the owner and standing of each concern:

- **Approved/current:** binding in its explicitly scoped project concern and revision.
- **Working/open:** candidate or unresolved; not silently implementable precedent.
- **Evidence/reference:** rendered proof, prototype, screenshot or former implementation; not authority without promotion.
- **Superseded:** no longer effective; preserve only relevant history/provenance.

Human approval must name the actual decision, scope, supporting evidence and intended source. Canonicalize only that decision. Update relevant project navigation and avoid re-copying specifications into a second master document. Before removing old active guidance, harvest valid principles and search for semantic stale references, not only broken links.

## Consumer packet — logical contract, not required template

A fresh Design/Engineering consumer should locate:

| Concern | Minimum |
| --- | --- |
| Product constraints | Approved actor experience and consequential product meaning, with owning source/revision |
| Design intent | Approved information priority, interaction meaning, visual/system decisions and accessibility requirements |
| Experience states | Consequential disclosure, success, incomplete/error/unknown, provenance, disabled/unauthorized and responsive priorities as applicable |
| Evidence | What a rendered/prototype proof actually shows, and what it cannot prove |
| Freedom | UI component/DOM/CSS/API/data-fetch mechanics and design gaps left to the authorized downstream owner |
| Gaps | Material unresolved owner decisions, applicability, affected consumers and acceptance evidence |

**Read accepted meaning first.** If a design artifact contradicts binding Product Authority, Product wins and the conflict must be escalated. A pretty prototype is not an acceptance test for data state, security, or finances.

## Implementation boundary

Engineering reconciles current code against accepted Design Authority; existing components may be reused, adapted or replaced, but code is not design authority by longevity. Avoid imposing a full rewrite or componentization solely for consistency. Shared primitive changes require blast-radius checks. Material UI work needs rendered, accessible verification at representative scope, and Human design acceptance where project ownership requires it.

A Design handoff can be READY for a bounded question while Engineering remains blocked on architecture, identity or contracts. Design acceptance, Engineering verification and Product delivery are distinct claims. Reopen approved design only with material evidence.
