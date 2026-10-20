# form-validation-boundary.md

**Location:** `react/form-validation-boundary.md`

**Principle**
Client-side schema validation (`zod`, `yup`, or equivalent) exists purely for UX — immediate feedback without a round trip. It is never the source of truth for whether data is actually valid; the backend re-validates independently regardless of what the client already checked. The risk this creates isn't "someone bypasses the client validation" (expected, and harmless if the backend is solid) — it's the schemas silently drifting apart over time: the backend's validation rule changes (a new enum value, a tightened length limit, an added cross-field constraint) and the client schema isn't updated to match, so users hit a confusing generic error on submit that the form itself should have caught, or worse, the client schema is *stricter* than the backend and silently blocks valid input the backend would have accepted.

**Bad**
```ts
// client schema, hand-written, no link back to the backend's actual rules
const registerSchema = z.object({
  email: z.string().email(),
  password: z.string().min(6), // backend actually requires 8 — drifted silently
});
```
```tsx
// treating a 422 the same as a network/500 error — no field-level detail surfaced
if (!response.ok) {
  setError('Something went wrong'); // user resubmits and hits the same wall
}
```

**Good**
```ts
// client schema kept next to a comment pointing at the authoritative rule doc/spec,
// so a reviewer catches drift when the backend rule changes without the client
// schema being touched
const registerSchema = z.object({
  email: z.string().email(),
  // password policy: see spec/account/features/01-register.md — min 8 chars
  password: z.string().min(8),
});
```
```tsx
async function onSubmit(values: FormValues) {
  const res = await fetch('/api/register', { method: 'POST', body: JSON.stringify(values) });
  if (res.status === 422) {
    const { errors } = await res.json(); // field-level errors from the backend
    errors.forEach(({ field, message }) => form.setError(field, { message }));
    return; // backend validation result wins, client schema was only ever a first pass
  }
  if (!res.ok) {
    setFormError('Something went wrong — please try again.'); // request-level, not field-level
  }
}
```

**Checklist**
- [ ] Every client-side validation rule that encodes an actual business constraint (length, format, allowed values) references where that rule is authoritatively defined (spec doc, OpenAPI schema) — not invented ad hoc while building the form
- [ ] A 422/validation-error response is handled distinctly from a network/5xx error — field-level messages from the backend are surfaced on the corresponding field, never collapsed into one generic banner
- [ ] The backend's response is treated as the final word even when it disagrees with what client validation already approved — the UI doesn't assume "client passed, so this will succeed"
- [ ] No total, eligibility check, or computed value shown to the user is trusted without also being what's submitted/re-verified server-side — client-side computation is presentation only
- [ ] When the OpenAPI schema changes a validation-relevant field (enum, format, required-ness), regenerating types is not treated as sufficient by itself — the corresponding `zod`/form schema is reviewed for drift as a separate, explicit step
