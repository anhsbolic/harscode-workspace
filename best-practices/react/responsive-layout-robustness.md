# responsive-layout-robustness.md

Location: `react/responsive-layout-robustness.md`

Principle Responsive correctness means preserving usability, readability, and structural intent across supported viewport sizes and realistic content variation. Prefer intrinsic and fluid adaptation; add breakpoints when composition genuinely needs to change rather than as isolated pixel patches.

Do not optimize only for one reference screenshot or happy-path content. Dynamic text, errors, empty states, large values, narrower containers, and interactive surfaces must have intentional shrink, wrap, stack, scroll, or clipping behavior. The project's CSS strategy determines how those invariants are implemented.

Bad

```
.content-layout {
  display: flex;
  width: 720px;
}

.content-main {
  width: 520px;
  height: 160px;
  overflow: hidden;
}

.content-action {
  width: 200px;
}

/* important information disappears only to make mobile fit */
@media (max-width: 48rem) {
  .content-status {
    display: none;
  }
}
```

Good

```
.content-layout {
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto;
  gap: 1rem;
}

.content-main {
  min-width: 0;
}

@media (max-width: 48rem) {
  .content-layout {
    grid-template-columns: 1fr;
  }
}
```

Hiding, reordering, collapsing, or replacing information at a breakpoint is a behavioral/product decision, not merely a CSS fix. It is valid when the intended information or action remains available through an approved responsive interaction.

Decision order

1. Can intrinsic sizing, flexible containers, wrapping, or stacking handle the variation without another breakpoint?
2. Which content can realistically grow, wrap, become empty, or contain an error?
3. Which elements are allowed to shrink, wrap, stack, scroll, clip, or remain fixed-size?
4. Does a proposed breakpoint correspond to a meaningful change in composition or hierarchy?
5. Are fixed dimensions safe for the content they contain?
6. Is any overflow intentional, reachable, and usable rather than an accidental side effect?

Checklist

* [ ] No accidental horizontal overflow is introduced by the changed surface
* [ ] Dynamic user-facing content can grow or wrap without clipping, overlap, or unreachable actions
* [ ] Important information and actions remain available when layout recomposes
* [ ] Fixed widths/heights on dynamic-content containers have an explicit reason and overflow behavior
* [ ] Dialogs, drawers, sticky/fixed controls, and form actions remain reachable in constrained viewports
* [ ] Horizontal scrolling is intentional for surfaces that genuinely require it, not a generic escape hatch
* [ ] Breakpoints represent meaningful layout changes rather than accumulating one-off pixel corrections
