# component-composition-and-abstraction.md

Location: `react/component-composition-and-abstraction.md`

Principle Extract components around meaningful UI or behavioral responsibilities, not line count. Abstract multiple implementations only when they demonstrate stable shared semantics; repeated code is evidence worth evaluating, not proof that a shared abstraction is required.

Prefer explicit composition and stable named variants over generic components whose behavior is controlled by a growing configuration surface. A small amount of feature-local duplication is cheaper than an abstraction that hides meaning, couples unrelated features, or accumulates structural mode flags.

Bad

```
<EditorPanel
  compact
  embedded
  admin
  hideHeader
  showSummary
  allowGuest
/>

function ProjectButton(props) {
  return <Button {...props} />; // no added semantics or contract
}
```

Good

```
<EditorPanel>
  <EditorHeader />
  <EditorFields />
  <EditorActions />
</EditorPanel>

<AdminEditorShell>
  <EditorPanel />
</AdminEditorShell>
```

When a structurally different variant becomes stable and meaningful, give it an explicit entry point rather than continually adding mode flags.

One occurrence can justify extraction when it represents a meaningful independent concept or behavior. Multiple occurrences justify evaluating whether shared semantics exist, but repetition alone does not justify generalization.

Decision order

1. Does extraction create a meaningful responsibility, interaction boundary, or independently understandable UI concept?
2. If implementations repeat, is the similarity semantic/behavioral or merely visual/structural coincidence?
3. Are the shared variation axes stable and understood?
4. Can children, slots, or explicit variants express the differences more clearly than configuration flags?
5. Does the abstraction reduce complexity for callers without hiding important behavior?
6. Is the abstraction genuinely cross-feature, or should feature-specific composition remain close to its feature?

Checklist

* [ ] Components are extracted for meaningful responsibility rather than file length alone
* [ ] Repetition triggers evaluation of shared semantics; no mechanical rule-of-three decides architecture
* [ ] Genuine binary state props (`disabled`, `required`, `open`) are distinguished from flags selecting structural/behavioral modes
* [ ] Growing structural-mode flags trigger reconsideration of composition or explicit variants
* [ ] Pass-through wrappers add semantics, behavior, constraints, defaults, or an intentional stable project API
* [ ] Feature-specific composition remains feature-local until cross-feature semantics are demonstrated
* [ ] Compound-component/context patterns are introduced only when simpler composition no longer expresses the contract clearly
* [ ] Component boundaries are not distorted merely to expose implementation details to tests
