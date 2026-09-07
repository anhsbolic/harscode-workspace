# 0017 — Responsive robustness and rendered visual verification

Status: Accepted  
Date: 2026-09-07  
Protection Tier: general  
Triggered by: Frontend best-practices gap audit while preparing Harscode for agent-driven React development. Existing guidance covers accessibility, async states, prototype translation, component testing, and mechanical lint/test enforcement, but it does not define responsive layout robustness as an observable correctness concern or require rendered verification when a change materially affects UI output. The audit also found that `testing-automation-boundary.md` currently collapses all non-mechanical judgment into a human-only checkpoint, which is too coarse for modern coding-agent harnesses capable of browser/runtime inspection.

Target area: best-practices

Target file(s):

- New: `best-practices/react/responsive-layout-robustness.md`
- New: `best-practices/react/visual-verification.md`
- `best-practices/react/testing-automation-boundary.md` — distinguish mechanical automation, objective runtime/rendered verification, and unresolved subjective judgment
- `best-practices/index.md` — add two React routing rows and update the testing-automation summary

## Gap found

### 1. Responsive layout failures have no dedicated correctness guidance

Current guidance can catch semantic/accessibility failures and test behavioral states, but not common layout failures such as:

- accidental horizontal overflow;
- dynamic text or validation errors being clipped;
- fixed-height containers failing with realistic content;
- important actions disappearing at narrow widths;
- arbitrary breakpoint patches accumulating instead of fixing the underlying layout model;
- sticky, fixed, or dialog surfaces becoming unreachable.

These are not merely aesthetic preferences. They can make content or actions unusable even when type checks, lint, and component tests all pass.

The missing rule should describe invariants rather than mandate a CSS strategy. Mobile-first CSS, Tailwind, CSS Modules, specific breakpoint values, and pixel-perfect matching are intentionally outside scope.

### 2. Rendered UI changes can pass every non-visual check while still be wrong

A frontend implementation can have:

- green unit/component tests;
- a successful build;
- correct API behavior;

while still having clipped content, overlay collisions, broken responsive behavior, invisible states, or hierarchy that contradicts an approved design precedent.

The workspace needs explicit guidance that rendered changes require rendered inspection, with verification depth proportional to the changed surface and risk.

The goal is not an exhaustive screenshot matrix. The smallest representative set capable of disproving the implementation is preferable.

### 3. Current automation guidance has a false binary

`testing-automation-boundary.md` currently separates:

- mechanically detectable → automate;
- requires intent → human/manual.

That omits a middle category now available to agent harnesses:

- objective runtime/rendered outcome → executable or browser-based verification by a capable agent.

Examples include overflow, clipping, focus visibility, overlay reachability, a modal opening in the expected state, or a known visual reference being structurally preserved.

Subjective or unresolved product/design intent still belongs at the existing human checkpoint. This proposal adds no new workflow stage.

## Proposed change

### New: `react/responsive-layout-robustness.md`

```md
# responsive-layout-robustness.md

Location: `react/responsive-layout-robustness.md`

Principle Responsive correctness means preserving usability, readability, and structural intent across supported viewport sizes and realistic content variation. Prefer intrinsic and fluid adaptation; add breakpoints when composition genuinely needs to change rather than as isolated pixel patches.

Do not optimize only for one reference screenshot or happy-path content. Dynamic text, errors, empty states, large values, narrower containers, and interactive surfaces must have intentional shrink, wrap, stack, scroll, or clipping behavior. The project's CSS strategy determines how those invariants are implemented.

Bad

    .campaign-layout {
      display: flex;
      width: 720px;
    }

    .campaign-content {
      width: 520px;
      height: 160px;
      overflow: hidden;
    }

    .campaign-action {
      width: 200px;
    }

    /* important information disappears only to make mobile fit */
    @media (max-width: 48rem) {
      .campaign-status {
        display: none;
      }
    }

Good

    .campaign-layout {
      display: grid;
      grid-template-columns: minmax(0, 1fr) auto;
      gap: 1rem;
    }

    .campaign-content {
      min-width: 0;
    }

    @media (max-width: 48rem) {
      .campaign-layout {
        grid-template-columns: 1fr;
      }
    }

Hiding, reordering, collapsing, or replacing information at a breakpoint is a behavioral/product decision, not merely a CSS fix. It is valid when the intended information or action remains available through an approved responsive interaction.

Decision order

1. Can intrinsic sizing, flexible containers, wrapping, or stacking handle the variation without another breakpoint?
2. Which content can realistically grow, wrap, become empty, or contain an error?
3. Which elements are allowed to shrink, wrap, stack, scroll, clip, or remain fixed-size?
4. Does a proposed breakpoint correspond to a meaningful change in composition or hierarchy?
5. Are fixed dimensions safe for the content they contain?
6. Is any overflow intentional, reachable, and usable rather than an accidental side effect?

Checklist

- [ ] No accidental horizontal overflow is introduced by the changed surface
- [ ] Dynamic user-facing content can grow or wrap without clipping, overlap, or unreachable actions
- [ ] Important information and actions remain available when layout recomposes
- [ ] Fixed widths/heights on dynamic-content containers have an explicit reason and overflow behavior
- [ ] Dialogs, drawers, sticky/fixed controls, and form actions remain reachable in constrained viewports
- [ ] Horizontal scrolling is intentional for surfaces that genuinely require it, not a generic escape hatch
- [ ] Breakpoints represent meaningful layout changes rather than accumulating one-off pixel corrections
```

### New: `react/visual-verification.md`

```md
# visual-verification.md

Location: `react/visual-verification.md`

Principle When a change affects rendered UI, verify the observable result in a real browser or another layout-capable rendered environment. Non-visual code checks and behavioral tests do not prove layout, visual hierarchy, responsive behavior, or spatial interaction correctness; rendered verification does not replace those checks either.

Match verification depth to the changed surface and its risk. Inspect the smallest representative set of states, viewports, and content conditions capable of exposing likely failures rather than generating an exhaustive Cartesian matrix.

Bad

    Tests: PASS
    Build: PASS
    Visual QA: PASS

No rendered surface, state, viewport, or interaction was identified or exercised.

Good

    Visual verification:
    - campaign detail, narrow viewport: default + long-title state
    - campaign detail, wide viewport: default state
    - donation form: validation error + submitting state
    - found and fixed CTA overlap with sticky footer
    - no remaining clipping or accidental overflow observed

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

- [ ] Rendered verification is performed for changes that materially affect UI output; internal/type-only refactors are not forced through a meaningless visual ritual
- [ ] Relevant interactive or async states are exercised, not only the initial static page
- [ ] Responsive risks are sampled at representative supported viewport/container conditions when applicable
- [ ] Realistic stress content such as long text, large values, validation errors, empty content, or missing media is exercised when it could invalidate the changed layout
- [ ] Approved references are compared by product/design intent rather than assumed pixel identity
- [ ] Visible focus, overlays, sticky/fixed surfaces, and important actions are inspected spatially when affected
- [ ] Correctness failures such as clipping, overlap, unreachable actions, missing states, or unintended information loss are distinguished from subjective polish
- [ ] Automated checks are not skipped because the UI looked correct, and rendered verification is not skipped merely because non-visual tests passed
- [ ] Objective rendered checks may be performed by a capable agent; unresolved subjective product/design intent follows the project's existing human-review checkpoint
- [ ] Verification reporting identifies the surface and representative condition checked instead of recording an unqualified `PASS`
```

### `react/testing-automation-boundary.md`

Keep the first two Principle paragraphs unchanged.

Replace:

```md
Requires understanding intent (does this test actually prove anything, does this UX decision feel right) → stays manual, and specifically stays at the human checkpoint / Finalize smoke-test stage this workspace's workflow already defines — this file doesn't add a new manual stage, it narrows what the existing one needs to spend attention on.
```

with:

```md
Not every non-mechanical check is human-only. Objective runtime/rendered outcomes that cannot be reduced reliably to lint/AST rules should be verified with the appropriate executable, browser, accessibility, or rendered tool; a capable agent may perform that verification when its harness supports it. Subjective or unresolved product/UX intent remains at the existing human checkpoint / Finalize stage. This file adds no new workflow stage.
```

Replace the current decision table with:

```md
Checklist — decision table for any new checklist item found in this workspace's other `react/` files

Question | If yes | If no
--- | --- | ---
Can the violation be described reliably as an AST/text/type pattern (banned call, banned prop, banned identifier)? | Automate — lint rule, type check, or equivalent | Continue
Is it an objective runtime/rendered outcome with a known expected result? | Verify with the appropriate executable/rendered tool; automate the stable mechanical subset where practical; a capable agent may perform the check | Continue
Does checking it require unresolved product/UX intent or subjective judgment? | Existing human checkpoint / Finalize stage | —
Is it an accessibility property? | Automate the mechanically detectable subset (`jest-axe`/equivalent), exercise objective keyboard/focus/rendered behavior where tooling permits, and retain human review when assistive-tech/product intent remains unresolved | —
```

Replace:

```md
- [ ] Automated a11y checks (`jest-axe`) are treated as a floor, not a substitute for a manual keyboard/screen-reader pass — this workspace's Finalize/smoke-test stage remains where that manual pass happens, not a new stage
```

with:

```md
- [ ] Automated a11y checks (`jest-axe` or equivalent) are treated as a floor, not proof of the full experience; objective keyboard/focus/rendered behavior is exercised with available tooling, while unresolved assistive-tech or UX judgment remains at the existing human checkpoint
```

Keep the existing "gates aren't gamed" human-checkpoint item: determining whether a test genuinely proves its intended behavior remains intent judgment rather than an observable runtime UI result.

### `best-practices/index.md`

Add:

```md
react | [react/responsive-layout-robustness.md](react/responsive-layout-robustness.md) | responsive, breakpoint, mobile layout, overflow, wrapping, fixed width, fixed height, viewport, sticky, drawer sizing, dialog sizing, long content | no | Preserve usability and structural intent across supported viewport sizes and realistic content growth; prefer intrinsic adaptation and intentional breakpoint/overflow behavior

react | [react/visual-verification.md](react/visual-verification.md) | visual verification, visual QA, UI verification, rendered UI, screenshot, responsive check, design reference, prototype comparison, layout regression, visual regression, browser inspection, visual state | no | Verify rendered UI changes in representative failure-revealing states and contexts; compare approved intent rather than raw pixels; keep rendered judgment complementary to automated checks
```

Place both after `loading-empty-error-state-conventions.md`, with `responsive-layout-robustness.md` before `ai-prototype-to-production-translation.md` and `visual-verification.md` after it.

Update the existing `testing-automation-boundary.md` summary from:

```md
Grep/AST-pattern-matchable checklist items become lint rules, not prose reminders; intent/judgment items stay manual at the existing human-checkpoint/Finalize stage
```

to:

```md
Mechanically detectable checklist items become automation; objective runtime/rendered outcomes use executable/rendered verification; unresolved subjective intent stays at the existing human checkpoint
```

## Rationale

The proposed rules are generic frontend engineering concerns:

- responsive failure is observable regardless of CSS framework;
- rendered verification applies to any browser-based React application;
- the proposal intentionally avoids universal viewport numbers, screenshot quotas, pixel-perfect gates, or mobile-first implementation rules;
- visual verification is proportional: it selects representative conditions rather than requiring an exhaustive matrix;
- browser-capable coding agents can verify objective outcomes without changing the workspace's policy ownership or removing human review for ambiguous product/design decisions;
- automation, rendered verification, and human judgment become three distinct mechanisms rather than a false mechanical-vs-human binary.

This remains best-practice knowledge, not a new frontend workflow phase.

---

After human review: update the Status above. If Accepted, merge into the target documents and leave this proposal in place — it serves as the proposal log/changelog.