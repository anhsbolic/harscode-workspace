# UI Composition, Accessibility, Responsive Quality, and Intentional Craft

> **Applicable when:** route/page/component, copy, visual treatment, prototype translation, layout, interactions or accessibility behavior changes. The target project's Design/Content/Asset authority and real application conventions always win over generic examples.

## Meaning before surface

Start with actual user goal, essential information hierarchy, valid interaction and accurate consequences. Visual success that misrepresents Product state or permission is failure. Use approved language, tone, icon baseline, color/type system and asset standing; when absent, make delegated ordinary choices with evidence-based clarity rather than inventing canonical design policy.

For meaningful new UI, Engineer and Craft Specialist challenge each other **early** while technical/visual trade-offs are still reversible. One Engineer owns production code. Craft's proposed copy, layout, or visual reference guides improvement but is not new Product/Design authority.

## Composition without speculative abstraction

Create components around coherent behavior or meaningful visual/interaction responsibility, not line count, number of files or hypothetical reuse. Route-local or feature-local composition is often right; repetition prompts evaluation, not automatic extraction. Prefer explicit composition and stable named variants over a “universal component” with many boolean props. Only create global state, primitives and design-token abstractions when actual project consumers and existing conventions justify them.

A prototype or visual export is a **reference**, not production implementation authority. Transfer useful composition, interaction states, copy or accessibility intent, but map styling, tokens, data shape, components and state to the real project. Never copy prototype placeholders or scratch mock behavior as canonical API truth.

## Actual accessibility and robust layout

Prefer semantic native controls and correctly associated field labels; ensure icon-only controls have meaningful accessible names, decorative visuals do not create noisy descriptions, and status/permission is not conveyed by color alone. Focus and keyboard handling should preserve reachability during dialogs, route transitions, async content changes and failure states. Determine project-specific contrast requirements and actual input/device support.

Use intrinsic sizing, wrapping, sensible stacking and explicit overflow for dynamic text, translated copy, long names, errors, missing media and large values. Breakpoints should represent meaningful composition changes, not isolated pixel patches. Never hide essential information or a consequential action on narrow screens merely to make a screenshot fit. Fixed/sticky controls and overlays must stay reachable.

## Intentional Craft / Anti-Slop

Treat every prominent illustration, badge, hero treatment, icon, surface, animation and text block as carrying a purpose. Reject filler cards, arbitrary imagery, copied “AI-looking” visual tropes and unsupported verification/safety claims because they lack information or authority—not because of their creation tool. Purposeful whitespace and clear typography are valid solutions. Use existing approved assets first; if a new asset cannot be created or approved, produce a useful brief and mark only necessary dependent work blocked. A temporary wordmark cannot silently become brand identity.

## Observation

For material rendered changes, inspect representative actual states and viewport/content stresses using tools and methods the project authorizes. Lint or component tests do not prove spatial layout; screenshots do not prove keyboard interaction. If project assigns manual QA or prohibits browser automation, comply and record what remains externally owned or unverified. Do not fabricate visual PASS.
