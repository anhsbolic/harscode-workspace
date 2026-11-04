# ORG-01 — Engineering / Builder

> **Status:** WORKING EXPERIMENT SNAPSHOT, not approved Harscode policy or a verified implementation.
> **Method:** Reverse lifecycle; first stage examined. **No comparison/audit of existing ORG-01 artifacts.**
> **Owner of experiment decisions:** Anhar. **Recorded:** 2026-11-03.

**Actor:** Calon Pembentuk Organisasi.

**Target:** A working end-to-end Kencleng feature in which the actor can form an organization context and become its first valid internal Owner, with truthful, inspectable outcomes.

## 1. INPUT

| Concrete input | Standing for this case |
| --- | --- |
| Product Contract (requirements, business rules, acceptance criteria) | **Wajib** |
| UX Flow / Interaction Specification (navigation and success/error interaction) | **Wajib** |
| Hi-Fi UI Design (screens, responsive layouts and relevant interaction states) | **Wajib** |
| Engineering Solution Design (architecture, auth, state and data flow) | **Wajib** |
| API Contract (endpoints, schemas, statuses, errors) | **Wajib** |
| Data Model / Database Schema (entities, relations, constraints, migrations) | **Wajib** |
| Existing Codebase & Technical Standards | **Wajib** |
| Test & Acceptance Scenarios | **Wajib** |
| Design System (components, tokens, styling) | **Nice to have*** |
| Web Assets (logo, icons, illustration, images, fonts) | **Nice to have*** |

*Conditional: the relevant Design System elements and web assets become **Wajib** if the accepted design or project constraints actually require them. "Wajib" refers to the **needed information or material**, not necessarily a distinct file or document.*

**Cross-stage acceptance clarification (2026-11-04, approved by Anhar):** For consequential Builder work, consumed Product, UX, Hi-Fi and Engineering artifacts carry their **relevant source revision, acceptance standing/scope and material unresolved decisions**. Merely locating an artifact does not establish acceptance. This uses the records already owned by each source; **no new approval workflow or duplicate authority source** is introduced.

## 2. PROCESS

1. **Input Review** — understand inputs, confirm relevant source revisions and acceptance scope, and identify material inconsistencies, unresolved decisions, or missing implementation decisions.
2. **Implementation Planning** — arrange frontend, backend, database and integration work.
3. **Frontend Development** — build pages, forms, navigation, interactions and responsive UI.
4. **Backend Development** — build API, authentication, authorization and business logic.
5. **Database Implementation** — implement schema, relationships, constraints and migrations.
6. **Integration** — connect frontend, API and database.
7. **Testing & Verification** — verify functionality, security, visual behavior, accessibility and end-to-end outcomes.
8. **Review & Handoff** — resolve material findings and hand off implementation with verification evidence.

These are logical activities; they do not require one Builder to own all frontend and backend work.

## 3. OUTPUT

- **Functional Web UI** — organization creation, review, sign-in, success and failure/uncertain-result interactions.
- **Working Backend API** — organization creation and retrieval services.
- **Operational Database Structure** — organizations, accounts and initial Owner relationships.
- **Integrated Application** — frontend, backend and database working together.
- **Test & Verification Results** — evidence against acceptance criteria and accepted design/engineering requirements.

## 4. OUTCOME

The actor can:

1. Start forming an organization.
2. Understand the information and consequences before creation becomes effective.
3. Authenticate as needed for attribution and explicitly submit the creation.
4. Form the organization **together with** an effective, valid first internal Owner relationship.
5. Inspect the organization and Owner relationship again after success.
6. Receive truthful information when creation fails or its result remains uncertain.

**End-state test:** not merely a finished-looking UI or passing unit tests. The integrated feature must actually fulfill the actor outcome; organization and initial Owner must be valid together, durable and inspectable.

**Boundary:** The wording above does not determine exact login timing, route count or screen order. Those remain Design/Engineering choices subject to consequential Product meaning. This is the **target** of the experiment, not a claim that any currently existing Builder implementation has passed these checks.

## Snapshot standing

Input/Process/Output/Outcome above is the discussion's **working model for the ORG-01 example**. It is not yet compared with source files, accepted as canonical Harscode guidance, or verified through real execution. Further stages are intentionally not defined here.
