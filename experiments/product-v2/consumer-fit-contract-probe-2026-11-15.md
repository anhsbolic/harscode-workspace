# Product v2 — Consumer-Fit Contract Probe (2026-11-15)

> **Standing:** RESEARCH EVIDENCE / SINGLE-CONTEXT CONTRACT-BASED PROBE; not independent Agent execution, project Product approval, consumer acceptance, formation, implementation, or runtime verification.
> **Scope:** Product v2 frozen candidate at commit `6609a68ecb652ce07b2887d41a44d2f7682e12e4` (blob `305b5433372111437a1f7c0b00b7b68ed404be17`), unchanged. This report is separate research evidence, not a v2 revision.
> **Target:** Hypothetical SchoolPickup pilot. No actual school project, authorized school policy owner, real UX participants, engineering system, independent Security analyst or native separated Agent execution was involved.

## Sources and test configuration

- **Product v2 frozen model:** [Product v2](product-responsibility-model-v2-frozen.md), especially §§3, 4.1, 4.4–4.6, 5–6. **Test input for consumer cold-read:** only the nine *proposed Product decisions* in §4.1, and the four logical information groups in §3; §§4.2–4.6 were treated as existing author-side analysis, **not** independent consumer evidence or already binding school policy. The three prior stress-test resolutions were separately checked as *proposals*, not silently promoted to project authority.
- **UX consumer:** [UX v1.1 experimental definition](../../design/ux-v1-1/definition.md) (blob `70f7c76f42f894978d66af688db633cdfb8f144c`; 2026-11-13; experimental only), especially I1–I5, P1–P7, output consumer sufficiency.
- **Engineering consumer:** [Rancang contract](../../engineering/spaces/rancang/contracts.md) (blob `903c54e05083640ee6060af1056995de8e9614ae`) and [coordination](../../engineering/spaces/rancang/coordination.md). Rancang is an **unformed research candidate**, not production-invocable.
- Evaluation method: two **separate responsibility/contract lenses** against the same fixed, proposed SchoolPickup input. Findings are a reasoned audit by one assistant context; no claim of independent consumer runs, independent security review, user study, code execution or validation. Test explicitly separates readiness to explore from readiness to commit/bind.

## A. UX v1.1 — consumer lens

| Relevant UX input/decision | Observed fit of SchoolPickup proposed Product input | Disposition |
| --- | --- | --- |
| I1: intended value, actors, capabilities and safety/authority boundaries | Scope is sufficient to ask initial human-experience questions; does not predetermine pages, entry channel, flows or visual design | **SUFFICIENT for discovery** |
| I2: people/situated context | Actual guardian, staff, pickup-person motivations, language/device/access needs, and constraints not researched; UX legitimately owns inquiry, not Product's user-journey reconstruction | **UX discovery required**, not a default Product blocker |
| I3: surrounding experience | Existing school release practices, telephone/manual channels, interruptions and re-entry not supplied for hypothetical pilot | **Discover**, not invented Product truth |
| I4: accepted constraints | School policy, actual safeguarding/privacy, accessibility, legal applicability and platform context unverified | **CONDITIONAL** for nonbinding concepts; must verify before binding related design |
| I5: evidence and authority | Model labels SchoolPickup decisions *proposed*; no project-owned Human/domain approval. No real user evidence | **Do not present as accepted or field-validated** |

**Representative bounded UX inquiry/output (hypotheses, not decisions):** Starting situation could be a guardian who needs to authorize an alternate pickup; investigate actual handoff, misunderstandings, whether the guardian or school staff initiates, and how a pickup person's identity is communicated. Compare *self-service authorization request* versus *staff-assisted request* as exploratory concepts. UX may choose information hierarchy, sequence, navigation, explanation, feedback, accessibility and recovery **only within accepted Product/safety constraints**. UX must not claim that submitted authorization means the school has authorized the final physical release.

**Material Product/domain question surfaced by UX cold-read:** What is the actual outcome of an electronically submitted request—accepted instruction, pending school confirmation, or merely a proposal? Which actor must approve, if anyone? "Pengajuan digital tidak otomatis berarti anak boleh diserahkan" protects release but does not fully decide request-state meaning and actor-visible success wording. UX cannot choose a binding "approved" state without owning decision.

**Another consequential question:** May guardian A revoke or supersede permission submitted by guardian B, and under what actual school/legal policy? UX can investigate the interaction but cannot create guardian precedence rules.

**UX verdict:** `SUFFICIENT` to start actor inquiry and provisional experience conceptualization; `CONDITIONAL` for binding UX semantics, until legitimate affected Product/domain constraints and relevant evidence are established. No Product-owned User Journey or mandatory outcome-tree was needed to form relevant UX questions.

## B. Engineering Rancang — consumer lens

| Rancang input | SchoolPickup evidence / source classification | Disposition |
| --- | --- | --- |
| I01 accepted Product meaning and acceptance | Nine school decisions are **proposed**, not project-authorized; no exact accepted school commitment/acceptance | **BLOCKED** for binding solution decisions; bounded feasibility inquiry possible |
| I02–I05 accepted UX meaning | No accepted UX flow, Lo-Fi/structural evidence, IA, interaction states or matching UX decisions | **BLOCKED** for material screen solution; UX owns these |
| I06–I07 code/stack/Engineering Standards | No target codebase, current technical constraints or accepted stack supplied | **UNVERIFIED**, not Product's duty to invent |
| I08 safety/privacy/security constraints | Critical minor-safety domain; no approved school safeguarding/privacy source, independently assessed threat model or authorized security control acceptance | **BLOCKED** where binding safety design depends on missing authority |
| I09–I10 existing APIs/integration | No existing system specified; authoritative school-record access and revocation update semantics are unknown | I09 **NOT APPLICABLE** if genuinely greenfield; I10 **UNVERIFIED/CONDITIONAL** |
| I11 NFR / I12 scenarios | Availability, degraded operation, freshness needs unknown; original Product trial identifies some race/conflict/outage scenarios but they are not approved source-backed acceptance | **CONDITIONAL**, safety-critical decisions held |
| I13 PoC | Feasibility experiments on current-record integration and revoked-permission race may be justified, but no performed PoC | **PERMITTED as scoped research**, not PASS |

**Representative Engineering-only research that may start safely:** Investigate possible authoritative record integration and update freshness; enumerate failure modes for stale screenshots/cached permits; assess concurrent revocation/final release time-of-check/time-of-use and manual-degraded procedures. Do **not** choose a weaker school authority source, legal precedence rule or release policy for convenience. No runtime results were obtained.

**Material missing Product/institutional rule:** The digital request's acknowledgment/validity/approval meaning and rules governing conflicting guardians are not settled. Previously proposed §4.4 mitigations (current-status check at final release, disputed rights escalated, screenshots insufficient during outages) are useful hypotheses but do not establish approved school policy or a verified technical mechanism.

**Engineering verdict:** `CONDITIONAL` for bounded technical feasibility/risk inquiry; `BLOCKED` for binding Engineering Solution handoff. This does not imply Product must author UX flow, Engineering Standards or architecture.

## C. Cross-consumer incompatibility, independent of Product v2

**Known semantic identifier collision:** UX v1.1 reassigns experimental `O2 = Experience Concept` and `O6 = Scoped Decisions/Handoff`, while Rancang I02/I03 still describes the older accepted UX `O2 = UX Flow`, `O6 = Lo-Fi`, and I05 references `O7`. UX v1.1 itself warns that old O2/O6 cannot be substituted by ID, and suggests meaning-based mapping: legacy Flow → experimental O3/C2 + O4; legacy Lo-Fi → O3/C3 + O4. A legitimate receiving-input compatibility check and appropriate coordinated approval would be needed before any new accepted handoff. **This is not evidence of Product v2 insufficiency.** It is an existing UX↔Rancang integration boundary.

## D. Tested propositions and disposition

| Proposition | Outcome and evidence limit |
| --- | --- |
| Product v2 enables UX discovery without a Product-owned User Journey | **Supported at contract-probe level** by identifying independent UX questions, provisional concepts and Product escalations from §4.1 |
| Product v2 permits Engineering to design safely without invented consequential Product truth | **Supported as authority separation**: Engineering can research, but correctly cannot bind missing school policy, UX decisions or technical inputs |
| Four logical Product information groups are sufficient for *all* downstream activities | **NOT ESTABLISHED**; sufficiency is decision-specific, and binding Engineering/design are not ready |
| UX↔Rancang output contracts are ready for new experimental UX v1.1 handoff | **NOT ESTABLISHED / semantic ID collision**, separate from Product v2 |
| Independent consumers actually used v2 and produced acceptable outputs | **NOT TESTED**; one context performed a contract-based analysis |
| Product v2 should be operationally adopted now | **NOT JUSTIFIED** by this probe |

**Overall status:** `PARTIAL / CONTRACT-FIT PROBE COMPLETE`. No rewrite of frozen v2 or existing Product, UX, Rancang or operational `main` is justified by this analysis. No Agent or formed Space was invoked.

## Next evidence needed

One **genuinely isolated fresh-consumer test**, preferably starting with UX v1.1, should consume only the frozen Product v2 + bounded proposed SchoolPickup Product input (without reading §4.2–4.6 author-side consumer simulation) and its own UX definition. Capture actual inquiry, concept/meaning, source status, material Product escalations, and what remained unexplorable. Then assess Engineering readiness separately using that genuinely produced/authorized UX meaning and exact owned project/security inputs, or explicitly limit the test to feasibility. Do not demand fabricated school authority, field observations or runtime proof.

**Decision / Action By Anhar:** None for this research evidence; any operational invocation/adoption would require separate authorization.
