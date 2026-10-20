# accessibility-fundamentals.md

**Location:** `react/accessibility-fundamentals.md`

**Principle**
An "a11y check" gate is only as good as what it's actually checking — without an explicit baseline, an agent (or a human) running that gate improvises criteria each time, and coverage drifts silently. The baseline that matters most for agent-generated UI: semantic HTML over div-soup (a `<button>` gets keyboard/focus/role behavior for free; a `<div onClick>` gets none of it and has to reinvent all of it correctly), every interactive control has an accessible name, focus is managed explicitly at state transitions (route change, modal open/close, async content replacing a loading skeleton), and information is never conveyed by color alone. These are the failures that are both common in agent-generated markup and invisible in a visual-only review pass.

**Bad**
```jsx
// clickable div: no keyboard access, no role, no focus ring
<div className="btn" onClick={handleSubmit}>Submit</div>

// icon-only button with no accessible name
<button onClick={onClose}><XIcon /></button>

// color as the only signal
<span className="text-red-500">{status}</span>
```

**Good**
```jsx
<button type="submit" onClick={handleSubmit}>Submit</button>

<button onClick={onClose} aria-label="Close dialog">
  <XIcon aria-hidden="true" />
</button>

<span className="text-red-700">
  <AlertIcon aria-hidden="true" /> {status}
</span>
```

**Focus management example — modal open/close**
```jsx
function Modal({ isOpen, onClose, children }) {
  const closeButtonRef = useRef(null);
  const triggerRef = useRef(null); // element that opened the modal

  useEffect(() => {
    if (isOpen) {
      triggerRef.current = document.activeElement;
      closeButtonRef.current?.focus(); // focus moves into the modal on open
    } else {
      triggerRef.current?.focus(); // focus returns to the trigger on close
    }
  }, [isOpen]);

  if (!isOpen) return null;
  return (
    <div role="dialog" aria-modal="true">
      <button ref={closeButtonRef} onClick={onClose} aria-label="Close">×</button>
      {children}
    </div>
  );
}
```
Without this, focus silently stays on (or defaults to) an element that's no longer visible or relevant — a keyboard/screen-reader user loses their place with no way to tell where they landed.

**Checklist**
- [ ] Interactive elements use native semantic tags (`button`, `a`, `input`, `label`) — a non-native element (`div`/`span`) acting as a control has `role`, `tabIndex={0}`, and both click and keyboard (`Enter`/`Space`) handlers, not just `onClick`
- [ ] Every icon-only or image-only control has an accessible name (`aria-label`, `aria-labelledby`, or visually-hidden text) — decorative icons/images use `aria-hidden="true"` or empty `alt=""` instead
- [ ] Form fields have a programmatically-associated `<label>` (via `htmlFor`/`id` or wrapping), and field-level errors are linked with `aria-describedby` + `aria-invalid`, not just visual proximity
- [ ] Focus moves explicitly on route change, modal/drawer open (into the new content) and close (back to the trigger), and toast/async content appearing — never left on a now-hidden or removed element
- [ ] Nothing is conveyed by color alone (status, required-field marker, error state) — pair color with an icon, text, or pattern
- [ ] Contrast ratios follow the project's design-token documentation (e.g. text/background pairs), not eyeballed
- [ ] Keyboard-only navigation (Tab/Shift+Tab/Enter/Escape) can complete every primary flow the component supports — this is directly testable via React Testing Library's role/keyboard queries, not just a manual pass
