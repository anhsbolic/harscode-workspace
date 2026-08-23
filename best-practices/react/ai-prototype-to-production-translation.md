# ai-prototype-to-production-translation.md

**Location:** `react/ai-prototype-to-production-translation.md`

**Principle**
AI design tools (Claude Design, v0, and equivalents) that export working React/HTML code are increasingly used as a visual/structural precedent before real implementation — validating a design system or page shape faster than static wireframes, and cheaper to keep roughly in sync. But the export comes from the tool's own scratch environment: its own component primitives, its own styling mechanism, its own placeholder data and local state. Treating it as a structural/behavioral reference is exactly right; treating it as a source of code to copy in is a category error that reintroduces exactly the drift problem prototypes are supposed to avoid — the "reference" quietly becomes a second, uncoordinated implementation of the design system. The failure isn't hypothetical: it shows up as inline styles bypassing the real design-token pipeline, mock data shapes diverging from the actual API contract, and a scratch component library slowly getting treated as if it were the real one.

**Bad**
```tsx
// copied straight from the design-tool export into the real app
function DonationForm() {
  const [amount, setAmount] = React.useState(0); // scratch local state, ignores the real
                                                    // app's react-hook-form + zod convention
  return (
    <div style={{ background: "var(--color-primary-600)", borderRadius: "var(--radius-md)", padding: "12px 14px" }}>
      <window.DesignToolPrimitives.Button onClick={() => submit({ amount, method: MOCK_METHODS[0] })}>
        {/* scratch primitive + hardcoded mock data, never replaced */}
        Donate
      </window.DesignToolPrimitives.Button>
    </div>
  );
}
```

**Good**
```tsx
// structure/composition and states carried over; styling, data, and state
// management translated to the real app's actual conventions
function DonationForm() {
  const { register, handleSubmit, formState } = useForm<DonationFormValues>({
    resolver: zodResolver(donationSchema), // real validation convention, not scratch useState
  });
  const mutation = useDonationMutation(); // real TanStack Query hook, real API contract

  return (
    <form onSubmit={handleSubmit((values) => mutation.mutate(values))}>
      <div className="bg-primary-600 rounded-md p-3"> {/* Tailwind utilities via the real token pipeline */}
        <AmountField {...register('amount')} /> {/* component decomposition kept, from the reference */}
        <MethodGrid {...register('method')} options={paymentMethods} /> {/* real options, not mock data */}
        <Button type="submit" disabled={mutation.isPending}>Donate</Button> {/* real component library */}
      </div>
    </form>
  );
}
```

**Checklist — what transfers directly (structural/behavioral precedent)**
- [ ] Component decomposition and composition (how the reference splits a page into sub-components) is a reasonable starting shape to mirror
- [ ] Which UI states exist and how they visually differ (idle/busy/selected/disabled) — the reference is useful evidence for "what states does this need," even though the mechanism producing them will be rewritten
- [ ] Microcopy/content (labels, helper text, button text) is legitimate to reuse or adapt
- [ ] Accessibility patterns already present in the export (e.g. `aria-pressed`, focus order) are worth carrying forward, not reinventing

**Checklist — what must be translated, never copied verbatim**
- [ ] Inline styles or style objects referencing design tokens are re-expressed through the real app's actual styling mechanism (e.g. Tailwind utility classes mapped in the real config) — never left as copy-pasted inline styles
- [ ] Hardcoded pixel/spacing values are mapped to the real design system's spacing scale, not reproduced as exact numbers — the export doesn't reliably use its own tokens consistently everywhere
- [ ] The design tool's own scratch component primitives (its own `Button`/`Badge`/`Icon`/etc.) are never imported into or referenced by production code — the real app's own component library is used, built from the actual design-token documentation, with the reference consulted only for expected composition/behavior
- [ ] Mock/placeholder data in the export is illustrative only — real data shape always comes from the actual API contract (OpenAPI schema or equivalent), never from what's hardcoded in the reference
- [ ] Local component state (`useState` scattered through the export) is replaced with the real app's actual state-management conventions (server state via a query library, client state via the real store, forms via the real validation library) — not preserved as-is because it "already works"
- [ ] Before treating anything in an export as correct, a known-issues/precedent doc (if one exists for that reference) is checked first — prototypes routinely have confirmed-wrong details sitting right there in otherwise-working code, and "it's already implemented" is not evidence it's correct