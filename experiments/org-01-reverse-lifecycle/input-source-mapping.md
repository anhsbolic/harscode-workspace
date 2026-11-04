# ORG-01 — Reverse Input–Source Mapping (Five Stages)

> **Status:** CANDIDATE CROSS-STAGE MAPPING / WORKING EXPERIMENT — NOT VERIFIED, NOT CANONICAL.
> **Owner of experiment decisions:** Anhar. **Persist authorized:** 2026-11-04.
> **Repository scope:** Harscode-Workspace `refactor/harscode-foundation` (research only; operational `main` remains unchanged).
> **Basis:** [Engineering — Builder](engineering-builder.md), [UI Design — Hi-Fi](ui-design-hifi.md), [Rancang](rancang-engineering-solution.md), [UX Design — Lo-Fi](ux-design-lofi.md), and [Product](product-definition.md) working models.
> **Scenario:** Calon Pembentuk Organisasi (illustrative ORG-01); no audit or comparison to existing Kencleng ORG-01 implementation or artifacts.

## Purpose and reading guide

Map each stage's **inputs** back to likely **outputs of one or several other stages**, **project-level sources**, or **Human / external evidence**. A stage does **not** necessarily wait for the preceding stage or an entire producing stage to finish. **Wajib / conditional / nice-to-have** statuses remain defined in the linked stage models; diagram edges are information provenance candidates, not new requirements or a state-machine/execution workflow.

- Solid arrow `-->`: **candidate primary/direct information source**.
- Dotted arrow `-.->`: **candidate additional or conditional source**.
- Source category labels (e.g. "Project Design System") **do not assert an actual artifact exists**. No specific source path, current revision, ownership, or suitability has been verified.
- A single Builder/Rancang/Design input may be **multi-source**. That does not grant a non-owner authority to change a Product, UX, or Engineering decision.
- This document records the mappings discussed, **not** a complete cross-stage coherence audit. Any gap is noted without silently rewriting an already accepted stage working model.

## 1. Engineering — Builder (10 inputs)

```mermaid
flowchart LR
    subgraph PHASE["Phase Outputs"]
        direction TB
        P["Product: Product Contract"]
        UX["UX Lo-Fi: UX Flow, Interaction & Webpage Map"]
        HI["UI Hi-Fi: Screens, Prototype & Visuals"]
        R["Rancang: Engineering Solution & Contracts"]
    end
    subgraph PROJECT["Project-Level Sources"]
        direction TB
        ENG["Existing Codebase & Engineering Standards"]
        TEST["Testing Standards"]
        DS["Design System"]
        ASSET["Brand & Asset Library"]
    end
    subgraph BUILDER["Engineering Builder — Inputs"]
        direction TB
        I1["1. Product Contract"]
        I2["2. UX Flow & Interaction Spec"]
        I3["3. Hi-Fi UI Design"]
        I4["4. Engineering Solution Design"]
        I5["5. API Contract"]
        I6["6. Data Model & Schema"]
        I7["7. Codebase & Technical Standards"]
        I8["8. Test & Acceptance Scenarios"]
        I9["9. Design System"]
        I10["10. Web Assets"]
    end
    P --> I1
    P --> I8
    UX --> I2
    UX -.-> I8
    HI --> I3
    HI -.-> I9
    HI -.-> I10
    R --> I4
    R --> I5
    R --> I6
    R --> I8
    ENG --> I7
    TEST --> I8
    DS --> I9
    ASSET --> I10
```

**Key composite input:** `Test & Acceptance Scenarios` receives Product acceptance criteria, Rancang technical verification, project testing conventions and potentially UX interaction cases. `Design System` and `Web Assets` may come directly from project-level sources and/or final Design outputs; in the Builder model they are conditionally required if the accepted design/project requires them.

## 2. UI Design — Hi-Fi (12 recorded inputs)

```mermaid
flowchart LR
    subgraph PHASE["Phase Outputs"]
        direction TB
        P["Product: Product Contract"]
        UX1["Lo-Fi: UX Flow"]
        UX2["Lo-Fi: Wireframes"]
        UX3["Lo-Fi: IA & Webpage Map"]
        UX4["Lo-Fi: Interaction & UI States"]
        R["Rancang: Material Technical Constraints"]
    end
    subgraph PROJECT["Project-Level Sources"]
        direction TB
        BR["Brand & Visual Guidelines"]
        AC["Accessibility & Device Standards"]
        QC["Design Quality / Anti-AI Slop"]
        DS["Existing Design System & Components"]
        AS["Brand & Asset Library"]
        REF["Visual References"]
        UR["User Research & Feedback"]
    end
    subgraph INPUT["UI Design — Hi-Fi Inputs"]
        direction TB
        I1["1. UX Flow Diagram"]
        I2["2. Lo-Fi Wireframes"]
        I3["3. Product Requirements & Rules"]
        I4["4. Screen Content & Information"]
        I5["5. UI States & Interaction Requirements"]
        I6["6. Brand & Visual Guidelines"]
        I7["7. Responsive & Accessibility"]
        I8["8. Design Quality / Anti-AI Slop"]
        I9["9. Existing Design System"]
        I10["10. Web Assets"]
        I11["11. Visual References / Moodboard"]
        I12["12. Usability Research / Feedback"]
    end
    P --> I3
    P -.-> I4
    UX1 --> I1
    UX2 --> I2
    UX3 --> I4
    UX3 -.-> I1
    UX4 --> I5
    UX2 -.-> I7
    R -.-> I5
    BR --> I6
    AC --> I7
    QC --> I8
    DS --> I9
    AS --> I10
    REF --> I11
    UR --> I12
```

**Candidate reconciliation gap:** Lo-Fi explicitly outputs **Webpage Map & Route Specification** as a Design contract for Hi-Fi, but the recorded Hi-Fi model has no **separate, explicit named input** for it. The diagram currently shows its contribution through UX Flow and screen content. This is a note for later review, **not** a change to either approved experiment model. Rancang technical constraints may inform Hi-Fi when material; no requirement to finish the entire Rancang stage first. If project Brand Guidelines do not exist, the Hi-Fi working model requires explicit permission to set visual direction.

## 3. Rancang — Engineering Solution (13 inputs)

```mermaid
flowchart LR
    subgraph PHASE["Phase Outputs"]
        direction TB
        P["Product: Product Contract"]
        U1["Lo-Fi: UX Flow"]
        U2["Lo-Fi: Wireframes"]
        U3["Lo-Fi: IA, Navigation & Webpage Map"]
        U4["Lo-Fi: Interaction & UI States"]
    end
    subgraph PROJECT["Project-Level Sources"]
        direction TB
        CB["Existing Codebase & Architecture"]
        ES["Engineering Standards & Tech Stack"]
        SEC["Security & Privacy Standards"]
        API["Existing API & Database"]
        INT["Existing Integrations"]
        NFR["Non-Functional Standards"]
        TS["Testing Standards"]
        RES["Technical Research / PoC"]
    end
    subgraph INPUT["Rancang — Engineering Solution Inputs"]
        direction TB
        I1["1. Product Contract"]
        I2["2. UX Flow Diagram"]
        I3["3. Lo-Fi Wireframes"]
        I4["4. IA & Navigation Structure"]
        I5["5. Interaction & UI States"]
        I6["6. Existing Codebase & Architecture"]
        I7["7. Engineering Standards & Stack"]
        I8["8. Security & Privacy Requirements"]
        I9["9. Existing API & DB Schema"]
        I10["10. Integration Requirements"]
        I11["11. Non-Functional Requirements"]
        I12["12. Test & Acceptance Scenarios"]
        I13["13. Technical Research / PoC"]
    end
    P --> I1
    P -.-> I8
    P -.-> I10
    P -.-> I11
    P --> I12
    U1 --> I2
    U2 --> I3
    U3 --> I4
    U4 --> I5
    U4 -.-> I12
    CB --> I6
    CB -.-> I9
    ES --> I7
    SEC --> I8
    API --> I9
    INT --> I10
    NFR --> I11
    TS --> I12
    RES --> I13
```

**Boundary:** Rancang directly consumes Product meaning, Lo-Fi UX, and project engineering reality. It owns API design and technical enforcement, **not** webpage navigation authority. **Hi-Fi is intentionally not a default Rancang input** and no special visual-format interpretation capability is required. A PoC need not pre-exist; Rancang may generate bounded research/evidence if a material unknown warrants it.

## 4. UX Design — Lo-Fi (11 inputs)

```mermaid
flowchart LR
    subgraph PHASE["Phase Outputs"]
        direction TB
        P1["Product Intent & Selected Outcome"]
        P2["Product: Actor Definition & Goals"]
        P3["Product User Journey"]
        P4["Product Contract"]
        R["Rancang: Known Technical Constraints"]
    end
    subgraph PROJECT["Project-Level Sources"]
        direction TB
        UXSTD["UX & Accessibility Standards"]
        NAV["Existing IA & Navigation Patterns"]
        ENG["Existing Technical Architecture"]
        RESEARCH["User Research & Feedback"]
        PATTERN["UX Patterns & References"]
        DOMAIN["Existing Product & Domain Information"]
    end
    subgraph INPUT["UX Design — Lo-Fi Inputs"]
        direction TB
        I1["1. Product Intent & Selected Outcome"]
        I2["2. Actor Definition & Goals"]
        I3["3. Product User Journey"]
        I4["4. Product Requirements & Rules"]
        I5["5. Product Acceptance Criteria"]
        I6["6. Content & Information Requirements"]
        I7["7. Accessibility & Device Requirements"]
        I8["8. Existing IA & Navigation Patterns"]
        I9["9. Known Technical Constraints"]
        I10["10. User Research & Usability Findings"]
        I11["11. UX Patterns & Design References"]
    end
    P1 --> I1
    P2 --> I2
    P3 --> I3
    P4 --> I4
    P4 --> I5
    P4 --> I6
    DOMAIN -.-> I6
    UXSTD --> I7
    P4 -.-> I7
    NAV --> I8
    ENG --> I9
    R -.-> I9
    RESEARCH --> I10
    PATTERN --> I11
```

**Candidate mapping gap:** Lo-Fi needs **Content & Information Requirements**, while Product's recorded outputs do not name these as a distinct artifact. Product Contract may supply them, supplemented by project domain sources, but **coverage is not yet verified**. Rancang constraints are optional/conditional: UX exploration does not need to wait for Rancang to finish.

## 5. Product — Product Definition (13 inputs)

```mermaid
flowchart LR
    subgraph PROJECT["Project-Level Sources"]
        direction TB
        DIR["Product Vision & Direction"]
        DOM["Domain Knowledge & Terminology"]
        BASE["Existing Product Baseline"]
        RULE["Existing Business Rules & Policies"]
        MET["Product Metrics & Analytics"]
        LEG["Legal & Privacy Requirements"]
        OPS["Business & Operational Constraints"]
        DEP["Related Product Capabilities"]
    end
    subgraph HUMAN["Human & External Sources"]
        direction TB
        OWNER["Human / Product Decision Owner"]
        SIGNAL["Problem Signals & Hypotheses"]
        ACTOR["Candidate User Context"]
        RES["User Research & Feedback"]
        MARKET["Market & Competitor References"]
    end
    subgraph INPUT["Product Definition — Inputs"]
        direction TB
        I1["1. Product Direction & Context"]
        I2["2. Problem Statements & Signals"]
        I3["3. Candidate Actor & Context"]
        I4["4. Domain Context & Terminology"]
        I5["5. Existing Product Behavior"]
        I6["6. Existing Business Rules"]
        I7["7. Stakeholder Goals & Authority"]
        I8["8. Product Success Signals"]
        I9["9. User Research & Feedback"]
        I10["10. Legal & Privacy Constraints"]
        I11["11. Business & Operational Constraints"]
        I12["12. Related Product Dependencies"]
        I13["13. Market & Competitor References"]
    end
    DIR --> I1
    OWNER -.-> I1
    SIGNAL --> I2
    RES -.-> I2
    MET -.-> I2
    ACTOR --> I3
    RES -.-> I3
    DOM --> I4
    OWNER -.-> I4
    BASE --> I5
    RULE --> I6
    OWNER --> I7
    MET --> I8
    OWNER -.-> I8
    RES --> I9
    LEG --> I10
    OPS --> I11
    DEP --> I12
    MARKET --> I13
```

Product's earliest inputs often arise from project-level authority, stakeholders, domain knowledge, and external evidence, **not** from a mandatory prior lifecycle stage. Existing observed behavior is evidence of the system's condition, but does not automatically establish the correct Product policy.

### Optional feedback to Product (not a mandatory prerequisite)

```mermaid
flowchart LR
    UX["UX Lo-Fi Findings"] -.-> PR["Product Review"]
    HF["Hi-Fi Design Findings"] -.-> PR
    R["Rancang Feasibility Findings"] -.-> PR
    B["Builder / Runtime Evidence"] -.-> PR
    PR -->|"Only if consequential Product decision is made"| D["Product Decision & Contract"]
```

A phase finding is **not automatically** a Product Contract change. Reconciliation and relevant Human/Product authority are required for consequential changes.

## Current findings (candidate, not resolved)

1. **Non-linear and multi-source:** direct Product → Builder, Lo-Fi → Rancang and Hi-Fi, project standards → multiple consumers, and Product + Rancang + project testing standards → Builder acceptance/testing inputs.
2. **Project-level sources are first-class:** Codebase, current standards, design systems, evidence and constraints should not be recreated by arbitrary preceding stages. Their actual authority and revisions have not yet been checked.
3. **Potential Hi-Fi input gap:** Webpage Map & Route Specification is a Lo-Fi output and Hi-Fi Design contract, but is not listed as a separate Hi-Fi input in the current model.
4. **Potential Lo-Fi input gap:** Content & Information Requirements may be contained in Product Contract, but explicit output coverage is not yet verified.
5. **Feedback is not auto-approval:** feasibility, user feedback, and implementation evidence may trigger owner review, not silently supersede existing decisions.

## Standing / next review boundary

**Completed:** lightweight candidate reverse mapping for all five phases, diagrammed with Mermaid, including source types and initial gaps. **Not completed:** verified artifact-to-input traceability, full cross-stage coherence analysis, source existence/version/authority verification, specific implementation feasibility or runtime validation.

Existing five stage working models are deliberately unchanged. Harscode operational `main`, existing Rancang/Product/Design authority, and Kencleng ORG-01 artifacts remain unchanged. Any decision to revise stage models, validate against current project source-of-truth, or promote to operational guidance is a separate future action by Anhar.
