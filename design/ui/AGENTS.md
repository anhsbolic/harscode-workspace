# UI AGENTS — Direct Visual Interface Concern

> **Standing:** A3 RESEARCH DRAFT / HUMAN CONTENT REVIEW PENDING. Scope: `design/ui/` only. Does not grant tool, Git write, external API, preview, deployment, Space invocation, protected-path or target-project Design approval permissions.

## Required UI agent behavior

1. Start with [local UI README](README.md), [UI Definition](definition.md) and [UI Authority & Handoff](authority-and-handoff.md). Use their **semantic contracts**, not a parent Design routing document or sibling Harscode agent instruction.
2. Identify bounded UI outcome and **source authority**: inspect effective **target-project** Product decisions, scoped UX flow/IA/navigation/web routes/states, applicable Design Standards, accessibility/security/privacy constraints, assets/copy requirements, actual consumer requirements and existing implementation **as evidence**. Pin exact revisions for consequential design claims.
3. Perform the [UI Input Sufficiency Check](definition.md#3-ui-input-sufficiency-check) before treating new/material Hi-Fi decisions as binding. For new/material UX, expect **UX O2 flow diagram and O6 representative Lo-Fi screens by default**, or accepted equivalent/legitimate evidence-based exception. Also require applicable UX IA/navigation/state and material webpage paths. **Report gaps to their actual owners; never improvise accepted UX or Product meaning.**
4. Keep **exploration distinct from acceptance**. Propose bounded visual alternatives when project direction or material UX information remains open, label them `PROPOSED` and state the exact affected acceptance edge. Other independent authorized work may continue.
5. For new/material UI design, produce **reviewable visual evidence**, not just prose. For newly authored **web Hi-Fi**, follow the [Visual Artifact Format Baseline v1](definition.md#7-visual-artifact-formats-verification-and-limits): **static HTML/CSS; one HTML per accepted actual UX webpage; states within that page; relative preview links; shared CSS when useful**. Record any accepted equivalent or concrete owner-backed exception. Do not silently use JavaScript to swap multiple actual webpages inside one file. No universal Figma, directory layout or frontend framework mandate.
6. Verify actual UX webpage-to-HTML preview mapping and page-vs-UI-state distinctions for new/material web UI. Inspect **rendered pages**, responsive widths and relevant state variants when permitted/available. Record actual tool/inspection, screenshots and limits or `NOT VISUALLY VERIFIED`; HTML source/mocked clicks do not prove actual visual, accessibility, usability or backend behavior.
7. Apply purpose-driven quality judgment: visual hierarchy, real context/copy, content density, keyboard/focus/read order, responsive priority, truthful provenance/status, respectful assets and no gratuitous generic filler. Assess “Anti-AI Slop” against concrete user/consumer consequences, not personal taste or a new scoring process.
8. For actual Human review, identify **precise UI decisions, affected surfaces/states, source/asset revisions and proof limits**. Record accepted exact project-owned content/revisions separately; a commit or template completion does not constitute approval.
9. Pass required accepted UI information directly to relevant functional consumers with source pointers, visual proof, scoped UI decisions, UX/Product constraints, delegated implementation freedom and actual verification standing. Do not invent a named consumer chain, reusable Project Standard, new frontend component API, or implementation authorization.

## Hard boundaries

- No invented domain roles/eligibility, payment/identity/privacy/legal claims, confirmation of unknown results, backend auth/API behavior, verified trust cues, or inaccessible state communication.
- No silent alteration of accepted UX Flow, IA, webpage paths, meaningful interaction states or Product/domain outcomes for aesthetic or technical convenience. Raise a specific reconciliation issue with the legitimate owner.
- No automatic promotion of local components, tokens, copy rules, brand direction, generated assets or Hi-Fi screens to **project-wide reusable standards**. An approved feature-specific UI design is **not** a canonical Project Design Standard.
- No forced new Hi-Fi artifacts for trivial delegated changes where existing accepted design already suffices; no automatic omission of visual proof for new/material UI work.
- No assertion of browser/rendered comparison, pixel fidelity to uninspected reference images, contrast pass, screen-reader check, user research, backend integration or release without performed evidence.
- Repository-root/project/Harness security and authorization rules still apply; available tools alone convey no permissions.

**Stop condition:** if a material binding UI decision lacks its actual owner-approved Product/UX/visual standard or required evidence, mark **affected decision BLOCKED or PROPOSED**, name the missing source/owner, and do not silently issue final UI acceptance. Independent safe, authorized exploration can remain open.
