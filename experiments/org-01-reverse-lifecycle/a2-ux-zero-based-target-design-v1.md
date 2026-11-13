# A2 UX — Zero-Based Target Design v1 (reviewed candidate v1.1)

> **Standing:** DRAFT RESEARCH CANDIDATE v1.1 / HUMAN CONTENT AND EXACT-REVISION ACCEPTANCE PENDING (2026-11-13). This is a redesign proposal for reusable Harscode UX capability, **not** effective `design/ux/` guidance, target-project UX acceptance, operational `main` policy, formed Space, implementation authority or proven usability.
> **Authoritative comparison baseline:** Harscode `research/cross-stage-mapping@6aa247c7c45ac99c87016ce43839894ae7b87178`. The existing six UX owning guidance/template files preserve their distinct `SETTLED_FOR_RESEARCH` exact-approval standing (see [historical A2 research approvals](https://github.com/anhsbolic/harscode-workspace/blob/947d9b361bd4cdf07d3aeebffb4a27eaf18da49a/experiments/org-01-reverse-lifecycle/audit-revision-plan-and-tracker.md)). This target does not rescind, reinterpret as unapproved, or edit those accepted bytes.
> **Research lineage:** [2026-11-12 UX quality problem framing and 2026-11-13 Foundational UX Model v0.1](audit-revision-plan-and-tracker.md). This proposal is **zero-based in conceptual derivation**, then reconciled against the current UX source for no silent loss.
> **Design owner:** Human decision-maker for research direction and acceptance. Harscode is reusable guidance; a real target project owns its Product/UX truth and observed execution evidence.
> **Revision provenance:** Original v1 is frozen at [commit `c3ce331`](https://github.com/anhsbolic/harscode-workspace/blob/c3ce3311110700b763cb4a5b23494aa4b4db0c0a/experiments/org-01-reverse-lifecycle/a2-ux-zero-based-target-design-v1.md), blob `336d80897b1d0d1bd720780e996bbdc4e7926ec8`. v1.1 is a **same-collaboration critical source review**, not a separate Human approval, external reviewer finding or actor usability test. See §12.

## 1. Question and decision

The target is **UX Design capability that can produce a comprehensible, usable and fit-for-purpose experience**, not an inventory of diagrams or a preserved 11 Input / 9 Process / 9 Output / 6 Outcome structure.

Three research questions:
1. Why was a bounded earlier UX perceived as unclear? **Observed:** Human criticism and uneven coverage of actor comprehension evidence. **Unproven:** specific causal responsibility of guidance, knowledge, execution, prior experience, or Product.
2. What makes UX clear and high-quality? **Candidate answer:** actor- and context-dependent understanding, usable action, appropriate control, accurate feedback, and grounded quality evidence.
3. What must Harscode UX do to deliver better work? **Candidate answer:** frame, discover, conceptualize, compare, specify, evaluate, decide and hand off with legitimate authority and decision-specific proof.

**Recommended direction:** a substantive **Process + Outcome redesign**, a targeted **Input strengthening**, and an **Output/consumer contract redesign** that preserves actual material flow, structure and state information while removing the assumption that output formats are UX quality. This is a new semantic model, not a light patch to P1/P2/P8 wording.

## 2. UX responsibility and non-ownership

**UX owns the design and justification of how people understand, navigate, decide, act, receive feedback and recover within an experience**, using actual actor goals, context and binding Product meaning. Its professional judgment includes detecting questions not answered by upstream requirements; seeking information; conceptualizing alternative experiences; choosing interaction/information/navigation patterns; exposing decision-relevant representations; assessing quality; and reconciling uncertainty.

UX **does not** independently invent Product capabilities, roles, eligibility, law/consent/privacy claims, irreversible effects, success semantics or trust evidence; impose reusable cross-feature Design Standards; set final visual/brand expression; or own technical implementation, runtime/API behavior or test results. Project-level sources prevail over reusable Harscode guidance. Decisions are scoped, reversible where possible, and attributed to their legitimate owners.

**Important:** An actor-facing conceptual model is a **UX explanation of effective Product meaning**, not a new owner of entity, capability, permission or domain definitions. A Product requirement may be semantically sufficient for binding consequences and still leave an **experience problem** for UX to discover and solve. Absence of comprehensive user research is neither automatic permission to invent actor facts nor an automatic blocker to safe bounded exploration.

## 3. Quality model — desired vs evidenced

### 3.1 What “clear” means

Clarity is not minimal copy, familiar cards or a completed flow. The relevant actor can correctly determine, to a proportionate standard:
- **Purpose:** what is possible, why it may be relevant, and what is not promised.
- **Concept:** what key objects/roles/relationships mean in their own task context.
- **Action:** available choices, prerequisites, immediate steps and material consequences.
- **State:** what happened, what did not, what is pending, what failed and what remains unknown.
- **Continuation:** what can be inspected, changed, recovered or done next, including when no further action is available.

Not every question has equal weight or must be answered on the first surface; timing and discoverability must match the decision. Truth-critical information must not be hidden by simplification.

### 3.2 Proposed quality properties — six logical targets

| Q | Desired property | Practical test, selected by real context |
| --- | --- | --- |
| **Q1 — Actor and purpose fit** | Experience addresses a real actor goal and the legitimate Product commitment, not a requirement-derived sequence that lacks user meaning | Can the actor identify the relevant goal and does the resulting experience actually support it? |
| **Q2 — Comprehension and predictability** | Terms, relationships, options, consequences, system status and next steps are understandable and not misleading | Can the actor accurately explain the significant choice/result and predict the next interaction? |
| **Q3 — Effectiveness and proportional effort** | Relevant tasks can be completed with proportionate effort, attention and cognitive load; perceived ease/satisfaction matter when relevant | Can the intended task succeed without unjustified work, and is the effort/experience acceptable to affected actors in context? |
| **Q4 — Agency, feedback and recovery** | Actor can make informed choices, retain appropriate control, correct mistakes, and recover from negative or uncertain situations | Can the actor discover safe available alternatives and recognize what is and is not reversible? |
| **Q5 — Truthful and responsible experience** | Interaction does not fabricate certainty, authority, eligibility, endorsement or outcomes, or manipulate choice | Do representation and behavior preserve the accepted source of truth and material disclosures? |
| **Q6 — Accessible and context-adaptive** | Experience respects relevant modalities, abilities, environments, devices and inclusive interaction needs | Is the experience usable under applicable assistive/input/environment constraints, with appropriate evidence? |

Subjective responses such as perceived safety, confidence, comfort, satisfaction or delight can matter according to context; they are **not** universal requirements to make an interface cheerful, nor permission to obscure truth or invent Product benefits.

These six **are target research meanings, not six mandatory metrics** or a claim of statistical validation. They are challengeable; other domain-specific qualities can be material. Evidence method and quality threshold depend on actor/context, consequence and intended consumer.

### 3.3 Evidence-to-claim discipline

- **Source/diagram review:** can establish logical coverage, consistency and authority trace; not observed actor comprehension.
- **Expert critique/heuristic walkthrough:** can identify plausible defects and trade-offs; not proof of representative-user success.
- **Visual/interactive prototype inspection:** can inspect bounded layout, task/state behavior and potentially accessibility aspects at that fidelity; not actual backend effects or validated user comprehension.
- **Representative actor observation/comprehension test:** may substantiate scoped understanding and task performance if method, participants and conditions fit; not automatic cross-context generality or production readiness.
- **Implemented/runtime evidence:** separately belongs to authorized implementation and actual test/operations owners; design-level success cannot claim it.

For each material quality claim, ask **what observed misunderstanding, error, harm, exclusion, friction or actor response would disconfirm it**. Research with actual users must respect applicable consent, privacy, authorization, data minimization and safeguarding; do not collect sensitive data merely to make the evidence packet appear stronger.

State **DESIRED**, **ASSESSED / METHOD-LIMITED**, or **DEMONSTRATED IN STATED CONDITIONS** rather than an unqualified “UX PASS”. Where risk is material and comprehension untested, withhold strong user-understanding claims while still allowing explicitly provisional design exploration.

## 4. INPUT — five information responsibilities (not five required documents)

| ID | Decision-relevant information | Sufficient / missing handling |
| --- | --- | --- |
| **I1 — Product meaning and actual commitment** | Intended Product outcomes, domain actors/rights, success/negative/unknown consequences, required information/disclosure, accepted scope and binding sources | Verify exact current owning Product meaning for dependent binding UX; ask Product for unresolved consequential decisions, not detailed screen advice |
| **I2 — Actor goals, context and mental models** | Primary, secondary and affected actors when applicable; conflicting goals, surrounding touchpoints, frequency, skills, expectations, mental-model hypotheses, accessibility, barriers, motivations and non-users | Do not assume upstream actor descriptions explain real comprehension; investigate cross-actor effects and unanswered questions proportionally |
| **I3 — Existing experience and surrounding ecosystem** | Accepted UX patterns, previously observed behavior/problems, prior interactions and navigation context, available artifacts and user feedback | Treat existing design as inspectable evidence/constraint where accepted, **not** a compulsory template or known good solution |
| **I4 — Applicable standards, feasibility and safeguards** | Project Design Standards, accessibility/device/input constraints, technical feasibility, safety/security/privacy, relevant platform patterns, real tooling and implementation constraints | Check legitimate source and authority; do not make unverifiable technical claims or require preexisting Engineering Spaces |
| **I5 — Evidence, uncertainty and decision landscape** | Available usability/research evidence, assumptions, contradicted evidence, unresolved actor questions, evaluation conditions and decisions/owners | UX actively identifies what else it needs to know; prioritize consequential uncertainty; allow explicitly hypothetical bounded research without falsely claiming sufficient Product authority |

These groups are a **semantic consolidation** of current 11 categories, not five upstream producers. Actual sources may satisfy multiple groups; no fixed collection order, interviews requirement or research artifact taxonomy.

### Input sufficiency principle

Ask: **Which decision can responsibly be made with what we know, which can be explored as a hypothesis, and which is blocked by missing ownership/meaning/evidence?** A missing item blocks only a materially dependent **binding** decision, not all other authorized research.

## 5. PROCESS — seven iterative UX responsibilities, deliberately non-sequential

| ID | Responsibility | Required professional judgment | When sufficient |
| --- | --- | --- | --- |
| **P1 — Frame experience problem** | Verify decision scope, actor goal, actual task, stakes, inherited assumptions, baseline evidence and who owns each meaning. Challenge a solution disguised as a requirement | A scoped, actor-relevant question and explicit problem/hypothesis are identifiable |
| **P2 — Discover and investigate** | Find unanswered user questions, mental-model ambiguity, opportunities, potential misunderstandings and evidence gaps. Choose cheap legitimate ways to learn, and distinguish assumed from observed | Enough understanding for the next reversible design decision; unresolved risk is labeled/owned |
| **P3 — Conceptualize experience** | Form and challenge an actor-facing **interpretation of accepted** concepts, relationships, decisions, states and feedback; compare materially distinct concepts when warranted | Coherent, challengeable concept and rationale, without letting a layout silently become the premise; sketches/prototypes may help discover the concept |
| **P4 — Design and challenge interactions** | Decide task progression, information priority, actions, navigation, search/findability, feedback, control, failure/uncertainty/recovery, relevant routes and inclusive modalities; inspect trade-offs | Meaningful user-facing decisions exist, challenged against goals and constraints; no silent invented Product policy |
| **P5 — Express inspectable decisions** | Select the least elaborate **representation that lets actual reviewers/consumers understand and test** concept, flow, structure and relevant states; preserve a material decision/proof link | Applicable interaction/IA/navigation/state meaning is inspectable; representation has known fidelity/evidence limitations |
| **P6 — Evaluate, refine and calibrate claims** | Specify the material failure to detect (misunderstanding, unsafe action, friction, exclusion, loss of control); seek disconfirming evidence with suitable methods, refine or state limits | Findings and decisions are traceable; claims match performed checks, and unresolved high-consequence uncertainty is not silently accepted |
| **P7 — Reconcile, decide and hand off** | Decide within UX delegation, advise Human on material UX acceptance, return Product-owned meaning to Product, verify constraints with Engineering, and prepare decision-specific consumer source/handoff | Legitimate decisions, exact effective sources, unresolved issues, consumer information and limitations are reconstructable |

**No mandatory seven-stage pipeline or concept-before-sketch gate.** Sketching may help discovery, and evaluation can precede a finalized concept. Discovery and evaluation may recur after representation; simple delegated work may reuse existing sufficient evidence. P7 decision-making occurs throughout, not only at a final approval gate. Design may begin with a safe exploratory hypothesis even when Product meaning is not yet complete; binding outcomes cannot silently rely on unapproved meaning.

### Capability expectations that must actually be exercised

**Core:** problem framing, mental-model reasoning, research literacy, interaction/information design, concept generation, critical comparison, accessible interaction, quality evaluation, written/visual communication, and authority-aware judgment.

**Conditional:** advanced user research, content strategy, responsive design, interaction animation/voice, formal accessibility evaluation, high-stakes risk analysis, cross-modal support, service/physical journey design, etc. Need and competence depend on actual medium/problem. Do not assume that including a named activity proves skill or craft.

**Design taste/judgment is operational, not aesthetic magic:** ability to see awkward conceptual framing, needless complexity, unclear hierarchy, false confidence and incoherent interaction; articulate why a design fails for its actors; compare meaningful choices and improve through critique/evidence. Visual aesthetics remain UI's owning expertise unless they affect functional UX clarity.

**Reasoning challenge, not a required form:** What concrete actor question or problem is resolved? Which materially different solution, if any, was considered and why was it rejected or unnecessary? What observable failure would falsify this concept? Which truth belongs to Product rather than UX? Do not manufacture alternatives when one approach is plainly sufficient.

## 6. OUTPUT — six logical decision meanings (not six mandated files)

| ID | Consumer-relevant meaning | Minimum when applicable |
| --- | --- | --- |
| **O1 — Experience question & actor context** | Relevant actors/affected people and goals, actual problem/context, constraints, assumptions, material uncertainties and research/evidence source | Specific enough to distinguish meaningful design from requirement transcription |
| **O2 — Experience concept & rationale** | Actor-facing explanation of **accepted Product concepts**, experience approach, material hypotheses and alternatives, why selected and what remains provisional | Enables challenge of the concept **before** reviewing only a screen, diagram or route |
| **O3 — Interaction, information & navigation contract** | **Separately inspectable** task/branch flow, decision-stage IA, navigation/routes, user-facing states/feedback/recovery and applicable modality/accessibility constraints | No material consumer information disappears within one umbrella output; never invent Product or backend semantics |
| **O4 — Decision-appropriate inspectable proofs** | Diagram, scenario, storyboard, structural Lo-Fi, dialogue/voice simulation, prototype or accepted equivalent **matched to material decision and consumer** | For new/material screen UI, inspectable flow/branch and representative structure remain the default evidence obligations; format is flexible with valid equivalence/exception |
| **O5 — UX evaluation, findings & refinement** | Quality questions, method, results, trade-offs, changes, unresolved issues and proportional claim standing | Evaluation meaning available independently of whether an interactive prototype exists |
| **O6 — Scoped decisions & consumer handoff** | Decision and acceptance standing, owner/delegation, exact source/revision, scope/exclusions, applicable binding UX meaning, downstream dependencies and source links | Consumer can reconstruct what is binding, provisional, unknown and available to decide independently |

**One artifact may serve several Outputs; several sources may jointly serve one Output.** The Output IDs are research reference labels, not a required delivery packet. Do not create a second Product/UX master when original project-owned accepted sources are sufficient.

### 6.1 Consumer information coverage — safeguard distinct from file count

**O3 is an umbrella grouping, not permission to hide decisions.** The receiving responsibility must be able to find each applicable meaning (a compact source pointer may suffice). A genuinely inapplicable meaning may be noted N/A with a context-specific reason; do not mandate one new coverage file.

| Information meaning | Must be inspectable when material | Example proof, not required format |
| --- | --- | --- |
| **C1 Actor/problem/concept** | Goal, actual problem, mental-model hypotheses, selected approach and relevant affected actors | Scenario, concept rationale |
| **C2 Interaction progression** | Entry/exit, decisions, branches, denial, uncertainty and recovery | Flow, task script, interaction simulation |
| **C3 Information and structure** | Decision-stage information priority, disclosure, representative surface layout for screen work | IA, storyboard, structural Lo-Fi |
| **C4 Navigation/continuity** | Destinations, returns, page-vs-state where relevant, cross-touchpoint continuity | Navigation map, route/dialogue reference |
| **C5 State/feedback/control** | Allowed action, focus/feedback, loading, validation, failure/unknown and safe recovery | State/interaction requirements |
| **C6 Accessibility/constraints** | Applicable assistive/input modalities and safety/technical limitations that shape UX | A11y notes, verified constraint refs |
| **C7 Evidence/standing** | Actual source/revision, scope/approval, proof strength, unresolved issues and decision owner | Scoped handoff/decision refs |

**New/material screen UX → receiving UI:** **C2 flow/branch proof and C3 representative structural proof are REQUIRED BY DEFAULT** through newly authored or sufficiently accepted exact-revision equivalents. A waiver requires the affected decision, concrete non-applicability/unchanged-scope evidence, authorized owner/delegation and consumer consequence. Unavailable renderer is a **NOT RENDERED** verification limit, not automatic permission to claim complete visual proof. Missing material meaning blocks **only** the dependent accepted consumer decision, not unrelated exploration.

Mermaid for flow and HTML/CSS for new structural Lo-Fi remain useful authoring defaults, **not universal format obligations**. A consumer must actually be able to inspect the material interactions and layout; “UI can infer it” is not an equivalent. For non-screen/voice/service UX, use meaningful dialogue/task/state proofs rather than invented web pages. Existing sufficient accepted source can be referenced without duplication.

### 6.2 Evaluation is not a prototype dependency

O5 is **not contingent on O4 being clickable**. A conceptual-comprehension walkthrough, expert review or actual user observation can support different bounded conclusions. A prototype is one possible evidence instrument, not the meaning of UX evaluation.

### 6.3 Compatibility with accepted UX/UI contracts — must resolve before adoption

The accepted research UI `design/ui/definition.md` I01/I02 and UI authority/handoff expect legacy UX **O2 Flow** and **O6 Lo-Fi**, whereas this target's new **O2 means Experience Concept** and **O6 means Consumer Handoff**. It is a **semantic ID collision**. A rename without changing consumer interpretation would silently break a material source contract.

**Proposed scoped adoption plan (not yet authorized):**
1. Inventory exact affected UX and UI README/AGENTS/definition/authority/template references, plus any real downstream Engineering input reading old IDs.
2. Migrate by **information meaning**, not matching numbers: legacy UX O2 Flow → new O3/C2 + O4 flow proof; legacy UX O6 Lo-Fi → new O3/C3 + O4 representative structural proof. Preserve all other material old UX outputs via §8 mapping and C1–C7.
3. Either **jointly review an effective UX/UI compatible revision set** or explicitly retain a **source-pinned compatibility interpretation** until legitimate UI owner approval. Do not present the new UX O2/O6 as satisfying old UI I01/I02 merely because numbers match.
4. Inspect actual receiving UI decision with exact source, applicable Product/UX meaning, decision/proof coverage and evidence limitations. Source-level coherence alone is not independent consumer proof.

Do not silently edit separate UI/Engineering guidance or re-label historical accepted blobs. Scope and Human approval must accompany any future effective replacement.

## 7. Explicit decision/authority routing

| Question | UX response | Owner |
| --- | --- | --- |
| How should a user understand or navigate an already accepted Product meaning? | Investigate, recommend and decide within UX delegation; seek material acceptance as appropriate | UX / legitimate project Human |
| Which of multiple interaction approaches is better? | Compare meaningful trade-offs and run suitable bounded evidence; do not require option catalogs | UX |
| Who may perform an action, what effect is committed, what does success mean? | State exact missing consequential meaning and recommend Product alternatives; no binding invention | Product |
| Can a proposed interaction be implemented safely or meet technical constraint? | Verify actual feasibility with owner; reconcile UX decisions rather than silently transferring design ownership | Engineering / relevant control owner |
| Should a bounded pattern become reusable across a project? | Propose with evidence; do not auto-canonicalize | Project Design Standards owner |
| Does a design meet user's actual needs? | Match evidence to scoped claim; Human approval is not observational research | UX evaluators and actual Human acceptance owner |
| Does a prototype or test authorize production? | No; separate implementation, security, protected-write and runtime gates apply | Actual implementation/Human owner |

A **working decision** can remain a hypothesis during exploration. A **binding accepted UX decision** needs legitimate project authority and exact source standing where material. A user request for a redesign does not itself authorize target-project writes or production.

## 8. Traceability from accepted A2 11/9/9/6 — no silent loss

This is a **semantic migration view**, not a decision to renumber current guidance now.

**Inputs:**
- Old I1/I3/I4/I5/I6 → new **I1** (Product meaning) plus relevant new **I5** (evidence/uncertainty).
- Old I2 → new **I2**; strengthen lived context, mental model, investigation.
- Old I8 → new **I3**; existing design can be evidence, not default pattern to preserve.
- Old I7/I9/I11 → new **I4** with applicable standards/references and verified constraints.
- Old I10 → new **I5**; strengthen proactive evidence acquisition.
- New I1–I5 may draw from multiple actual sources; no mandatory upstream chain.

**Processes:**
- Old P1 → new P1/P2/P3 (scope, discovery, concept).
- Old P2/P3/P4/P6 → new P3/P4/P5 (concept-grounded flow, IA, route, states).
- Old P5/P7 → new P5 and conditional O4 (proof/representation, not design quality alone).
- Old P8 → new P6 (quality question → appropriate evidence → refinement).
- Old P9 → new P7 (conditional Human acceptance, delegated decision and handoff).
- New P roles can overlap and recur without stage gating.

**Outputs:**
- Old O1 → new O1/O2.
- Old O2/O3/O4/O5/O7 → new O3, supported by O4 where material proof is required.
- Old O6 → new O4, preserving relevant representative structure for receiving UI.
- Old O8 → new O4 (conditional interactive proof) **and** new O5 (separate evaluation evidence).
- Old O9 → new O6, with new O2/O5 decision rationale and evidence.
- **Critical:** no new model may omit branch/state/navigation/structural information material to an actual receiving consumer.

**Outcomes:**
- Old Goal-Oriented → new Q1/Q3.
- Old Intuitive → new Q2/Q3/Q4, more explicit about comprehension and control.
- Old Clear IA → new Q2/Q3 with timing/discoverability.
- Old Efficient → new Q3.
- Old Trustworthy → new Q2/Q5 and state truth.
- Old Accessible → new Q6.
- New Q4 explicit agency/recovery is strengthened, not permission to change Product outcomes.

**Other preserved rules:** scoped acceptance/revisions; Product vs UX vs UI vs Standards vs Engineering boundaries; conditional web routing; source-based input sufficiency; truthful incomplete/unknown states; accessibility; no automatic Space/phase; no fake rendering/usability/runtime claims; no mandatory project-wide standards.

## 9. Three falsifiable explanations of earlier poor UX (not settled causes)

| Hypothesis | Source-level support | What could disconfirm or strengthen it |
| --- | --- | --- |
| **H1 — problem discovery under-executed** | Existing P1 lists context/expectations but does not directly demand unknown actor-question discovery; available laboratory evidence did not reconstruct a strong problem-question trace | Reconstruct independent actor assumptions/UX alternatives from real execution; show discovery already occurred and was adequate, or demonstrate missing critical question |
| **H2 — concept formation insufficient** | Existing P2 starts at Flow; no explicit concept-level responsibility in A2. Old design may be semantically accurate yet user-opaque | Blind-first UX concept exploration; see whether concept decisions materially improve comprehension or old concept already fits |
| **H3 — evaluation/representation mismatch** | Old P8 and O8 mention evidence/review, but actor comprehension was not observed and O2/O6 proof obligations are strong | Select evaluation matching actual quality claim; compare candidate and baseline with suitable actors/method, noting confounds |

**Upstream Product/standards insufficiency remains an alternative explanation, not a proven blocker**. Escalate only a concrete unmet consequential decision/evidence need. A better-looking prototype alone cannot prove this v1 correct or causal.

## 10. Cross-context conceptual stress tests — not empirical generalization

| Experience context | Decision/quality emphasis | Appropriate evidence/representation |
| --- | --- | --- |
| New user creating an unfamiliar entity | Mental model, purpose, consequence comprehension and credible continuation | Concept comparison, contextual explanation, task/review walkthrough, actor comprehension |
| Expert repeated operational task | Speed, error prevention, keyboard efficiency, recovery and status | Task/keystroke map, state proof, repeated-use observations; avoid mandatory onboarding screens |
| High-consequence irreversible action | Eligibility, informed choice, explicit commitment, uncertainty and safe recovery | Decision-critical disclosure, failure-state model, focused consequence comprehension and risk review |
| Voice/nonvisual interaction | Turn-taking, command discoverability, confirmation, state feedback and repair | Conversation/state script, audio/dialogue simulation, accessibility evidence; no fake web routes |

All four fit the **same abstract responsibilities**, with different emphasis. This is a stress test of semantics only, not proof of independently delivered UX in those contexts.

## 11. Research adoption and review sequence — not an imposed workflow

1. **Review this target v1 on semantics:** challenge I/P/O/O responsibilities and quality/evidence discipline, not arbitrary counts.
2. **Choose bounded validation:** derive a new UX concept blind-first from the lab's actual approved Product meaning and applicable standards; do not preserve old UX; compare afterward with provisional prior UX under the same quality questions. Real actor testing if justified and feasible, otherwise qualify claims.
3. **Check a different interaction context:** a deliberately different scenario (e.g. frequent expert workflow or voice) to see if generic semantics force unjustified screen flows or ceremony.
4. **Prepare exact consumer compatibility and owning-doc changes only after evidence/decision:** UX README/AGENTS/definition/authority/template; UI I01/I02 references and consumer sufficiency; downstream source pointers. Keep old accepted research approvals as historical lineage. Require a separate legitimate Human exact-revision decision before saying revised research guidance is `SETTLED_FOR_RESEARCH`.
5. **Operational promotion remains independent:** research quality improvement, source review, legitimate project acceptance, independent consumption, and actual runtime verification are distinct.

**Explicitly NOT done:** edited accepted UX/UI files; target project Design/Product changes; user usability test; independent consumer implementation; new Harscode operational policy; acceptance of this draft by Human.

## 12. Source-based critical review of v1 and v1.1 corrections (2026-11-13)

> **Standing:** Author-led adversarial **source critique** within this same Human–AI research collaboration, comparing original v1 to accepted UX/UI guidance. **Not** independent actor testing, independent consumer execution, third-party verification or Human acceptance. Initial v1 is preserved by exact Git revision in the header.

| ID | Critical finding | v1.1 correction |
| --- | --- | --- |
| **CR-01 HIGH — Concept/authority** | UX concept could be read as authority to redefine domain objects, actors or capabilities | Express accepted Product meaning through actor-facing concepts; binding domain decisions still belong to Product |
| **CR-02 MED — Actor/quality breadth** | Single-actor/task emphasis underrepresents affected actors, cross-touchpoint tension and subjective UX quality | Relevant multi-actor context and subjective perceptions included conditionally, without mandatory delight or research |
| **CR-03 HIGH — False phase gate** | “Before screen layout” could be applied as a mandatory linear concept-design gate | Explicit iteration/sketch-first allowance; conceptual reasoning must be challengeable, not chronologically first |
| **CR-04 HIGH — Design judgment operationality** | Named skillsets alone might produce polished but unchallenged designs | Concrete critique prompts and disconfirming quality questions, without mandatory option catalog |
| **CR-05 HIGH — Output/consumer gap** | One O3 grouped contract might hide necessary flow/state/navigation/structural meaning | C1–C7 inspectability map; preserve C2 flow and C3 structural proof required-by-default for material receiving screen UI |
| **CR-06 HIGH — O2/O6 collision** | New output ID meanings differ from already accepted receiving UI I01/I02 contracts | Concrete semantic mapping and scope-bound joint/compatible adoption plan; no automatic old UI acceptance |
| **CR-07 MED — Evidence/research safety** | Design review could still claim observed user clarity; new research could collect personal data casually | Falsifiable evaluation claims; appropriate consent/privacy/research safeguards and limits |
| **CR-08 OPEN — Actual effectiveness** | More complete UX guidance does not prove that real users will understand or succeed | No usability success claim; bounded lab and distinct-context consumer checks remain necessary |

**Review verdict:** v1 direction is defensible but would be unsafe to promote without CR-01, CR-03, CR-05 and CR-06 corrections. This revised v1.1 candidate addresses those source-level risks but **does not** establish that 5/7/6/6 is optimal or that the revised UX is empirically better. Exact Human content approval and the real consumer/proof checks remain separate.

**Next inquiry:** Challenge v1.1 on real actor problem framing and disconfirming UX evidence through one bounded **blind-first** experience design case, then check an unrelated interaction context and consumer compatibility. Only then decide whether to prepare an effective replacement and synchronized UI/Engineering reference amendments.
