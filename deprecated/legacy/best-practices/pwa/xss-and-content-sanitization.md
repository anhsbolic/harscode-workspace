# xss-and-content-sanitization.md

**Location:** `pwa/xss-and-content-sanitization.md`

**Principle**
Any content that originates from user input and is rendered back to the page must go through consistent output-encoding or sanitization. Modern frameworks (React, Vue) escape output by default through normal bindings — but the most dangerous points are where that's deliberately bypassed: `dangerouslySetInnerHTML` in React, `v-html` in Vue, or rendering the result of a Markdown-to-HTML conversion of user input without additional sanitization. These points easily slip past review because they look like an intentional feature, not a bug.

**Bad**
```jsx
<div dangerouslySetInnerHTML={{ __html: userProvidedDescription }} /> // no sanitization
```

**Good**
```jsx
import DOMPurify from 'dompurify';

<div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(userProvidedDescription) }} />
```

**Checklist**
- [ ] Every use of `dangerouslySetInnerHTML`/`v-html`/equivalent goes through a sanitization library (not manual regex)
- [ ] Markdown-to-HTML conversion of user input is sanitized after conversion, not trusted to be safe by default
- [ ] There is an explicit review checklist for finding points that bypass the framework's default auto-escaping
- [ ] Content rendered in different contexts (HTML body vs. attribute vs. URL) is sanitized appropriately for that context