# visual-verification.md

Location: `react/visual-verification.md`

Principle When a change affects rendered UI, verify the observable result in a real browser or another layout-capable rendered environment. Non-visual code checks and behavioral tests do not prove layout, visual hierarchy, responsive behavior, or spatial interaction correctness; rendered verification does not replace those checks either.

Match verification depth to the changed surface and its risk. Inspect the smallest representative set of states, viewports, and content conditions capable of exposing likely failures rather than generating an exhaustive Cartesian matrix.

Workflow ownership

Rendered inspection may happen during implementation as part of the edit → render → fix feedback loop. Those implementation-time checks help the builder converge on a correct UI and may be reported as build evidence, but they do not replace independent verification.

When the workflow has a separate Testing phase, final rendered verification belongs there. Testing consumes prior build claims as evidence, spot-checks what is already well-supported, and independently exercises the representative states or conditions most capable of disproving the rendered result.

Bad

```
Tests: PASS
Build: PASS
Visual QA: PASS
```

No rendered surface, state, viewport, interaction, or independent verification boundary was identified.

Good

```
Build-time rendered checks:
- editor page: narrow layout exercised while implementing
- fixed action overlap before handing off

Testing rendered verification:
- editor page, narrow viewport: default + long-title state
- editor page, wide viewport: default state
- form: validation error + submitting state
- no remaining clipping, overlap, or accidental overflow observed
```

When an approved design, prototype, or existing production precedent exists, compare the rendered result against its intended hierarchy, composition, content grouping, interaction states, and responsive behavior. Do not require raw pixel identity when production tokens, implementation constraints, or known prototype limitations intentionally differ.

Decision order

1. Did the change affect rendered output or spatial interaction? If not, rendered verification is normally unnecessary.
2. What observable surface actually changed?
3. Which interactive, asynchronous, or content state is most capable of exposing a failure?
4. Which supported viewport or container condition is most capable of exposing a failure?
5. Is there an approved visual or production precedent whose intent should be preserved?
6. Render and inspect the smallest representative set that exercises those risks.
7. Fix correctness failures before spending scope on subjective polish.
8. Capture screenshots or other evidence when they materially help review, comparison, regression diagnosis, or handoff — not as a ritual for every UI change.

Checklist

* [ ] Rendered verification is performed for changes that materially affect UI output; internal/type-only refactors are not forced through a meaningless visual ritual
* [ ] Build-time rendered checks are treated as implementation feedback, not as a substitute for independent Testing when the workflow defines a separate Testing phase
* [ ] Testing independently exercises representative rendered conditions rather than trusting build claims as facts
* [ ] Relevant interactive or async states are exercised, not only the initial static page
* [ ] Responsive risks are sampled at representative supported viewport/container conditions when applicable
* [ ] Realistic stress content such as long text, large values, validation errors, empty content, or missing media is exercised when it could invalidate the changed layout
* [ ] Approved references are compared by product/design intent rather than assumed pixel identity
* [ ] Visible focus, overlays, sticky/fixed surfaces, and important actions are inspected spatially when affected
* [ ] Correctness failures such as clipping, overlap, unreachable actions, missing states, or unintended information loss are distinguished from subjective polish
* [ ] Automated checks are not skipped because the UI looked correct, and rendered verification is not skipped merely because non-visual tests passed
* [ ] Objective rendered checks may be performed by a capable agent; unresolved subjective product/design intent follows the project's existing human-review checkpoint
* [ ] Verification reporting identifies the surface and representative condition checked instead of recording an unqualified `PASS`
