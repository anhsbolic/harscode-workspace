# testing-automation-boundary.md

Location: `react/testing-automation-boundary.md`

Principle The same lesson this workspace already learned the hard way for techplan review (`workflow/2-techplan/retro.md` — a rule restated in prose gets skipped, twice, regardless of model or person; converting it into an explicit mechanical check is what actually held) applies to frontend correctness/security checklist items too.

If a checklist item's violation can be pattern-matched reliably from the AST, text, or type system — a banned function call, banned prop usage, or banned identifier appearing in JSX — it belongs in automation, not in a reviewer or tester's memory. The boundary: mechanically detectable → automate.

Not every non-mechanical check is human-only. Objective runtime or rendered outcomes that cannot be reduced reliably to static rules should be verified with the appropriate executable, browser, accessibility, or rendered tool. A capable agent may perform that verification when its harness supports it, and a separate Testing phase owns the independent verification when the workflow defines one.

Subjective or unresolved product/UX intent remains at the existing human checkpoint. This file adds no new workflow stage.

Bad

```
<!-- checklist item, sits in a review guideline as prose, relies on the -->
<!-- reviewer remembering to check it on every PR -->
- [ ] No component calls `fetch` directly outside `lib/api/`
```

Same failure shape as R18 / severity-leak in the techplan driving story: correct advice, restated instead of enforced, and it recurs.

Good

```
// eslint.config.mjs
export default [
  {
    // default: raw fetch is banned everywhere
    rules: {
      'no-restricted-globals': ['error', {
        name: 'fetch',
        message: 'Use the centralized apiFetch client from lib/api/, not raw fetch(). See react/api-client-centralization.md.',
      }],
    },
  },
  {
    // the one place raw fetch is allowed: the client itself
    files: ['lib/api/client.ts'],
    rules: { 'no-restricted-globals': 'off' },
  },
];

// dangerouslySetInnerHTML: banned by default (react/no-danger), only escapable
// with an explicit disable comment — forces the exception to be visible and
// reviewable, rather than silently allowed everywhere
{
  rules: {
    'react/no-danger': 'error',
  },
}

// usage now requires an explicit, reviewable justification at the call site:
// eslint-disable-next-line react/no-danger -- sanitized via DOMPurify.sanitize, see xss-and-content-sanitization.md
<div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(narrative) }} />

// custom rule sketch: flag `error.message`/`err.toString()` used directly
// inside JSX — the exact shape that leaks raw backend error text to the user
{
  rules: {
    'no-restricted-syntax': ['error', {
      selector: 'JSXExpressionContainer > MemberExpression[property.name="message"]',
      message: 'Do not render error.message directly — use a generic, user-facing message. See react/loading-empty-error-state-conventions.md.',
    }],
  },
}
```

Checklist — decision table for any new checklist item found in this workspace's other `react/` files

| Question                                                                                                           | If yes                                                                                                                                                                                                                        | If no    |
| ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| Can the violation be described reliably as an AST/text/type pattern (banned call, banned prop, banned identifier)? | Automate — lint rule, type check, or equivalent                                                                                                                                                                               | Continue |
| Is it an objective runtime/rendered outcome with a known expected result?                                          | Verify with the appropriate executable/rendered tool; automate the stable mechanical subset where practical; a capable agent may perform the check                                                                            | Continue |
| Does checking it require unresolved product/UX intent or subjective judgment?                                      | Existing human checkpoint                                                                                                                                                                                                     | —        |
| Is it an accessibility property?                                                                                   | Automate the mechanically detectable subset (`jest-axe`/equivalent), exercise objective keyboard/focus/rendered behavior where tooling permits, and retain human review when assistive-tech/product intent remains unresolved | —        |

* [ ] Every "no raw X" / "always do Y" item added to any `react/` best-practice file in this workspace is checked against the table above before being left as prose-only
* [ ] Lint rules that ban a pattern by default include an explicit, reviewable escape hatch (a disable comment with justification), not a silent allowlist buried in config — makes exceptions visible at review time instead of invisible
* [ ] Automated a11y checks (`jest-axe` or equivalent) are treated as a floor, not proof of the full experience; objective keyboard/focus/rendered behavior is exercised with available tooling, while unresolved assistive-tech or UX judgment remains at the existing human checkpoint
* [ ] "Gates aren't gamed" (assertions actually test something, thresholds not quietly lowered) stays a human-checkpoint item regardless of how much lint/type coverage exists — no static rule substitutes for reading whether a test's mock is at the right layer (see `component-test-mocking-discipline.md`)
