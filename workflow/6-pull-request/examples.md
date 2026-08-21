# Examples

Three real examples, showing when the Changes section is included vs
omitted.

---

## Example with Changes section (multiple files, needs a map)

Source: GMRT-50456 (KBLI version validation)

```markdown
## Background

KBLI (Klasifikasi Baku Lapangan Usaha Indonesia) validation on product
create/update previously only matched KBLI **code** between the seller's
company OSS data and the category's legacy `kbli` column. However, KBLI
codes are versioned by year (e.g. `2020`, `2025`), and the same code can
have different meanings across versions.

## Solution

Add a new `MARKETPLACE-KBLI2025` toggle that enables **code + version**
exact matching.

| `VALIDATE_KBLI_KILL_SWITCH` | `MARKETPLACE-KBLI2025` | Behavior |
|---|---|---|
| ON | * | Skip all KBLI validation |
| OFF | OFF | Code-only validation (legacy) |
| OFF | ON | Code + version exact match |

## Changes

- **`domains/product/constant.go`** — add `MARKETPLACE_KBLI2025` toggle constant
- **`domains/product/service.go`** — rewrite KBLI validation into 3 branches
- **`domains/product/service_ConstructAllProductTable_test.go`** — 6 new unit test cases

## References

https://govtech-lkpp.atlassian.net/browse/GMRT-50456

## Demo

**Before:** seller with KBLI code `41011` (version `2020`) could pass
validation against a category with the same code but version `2025`.

**After:** when the toggle is ON, a version mismatch returns a clear
error. When OFF, legacy behavior is preserved.
```

Why Changes is included here: 3 files across 2 different layers
(constant + service + test) — a reviewer benefits from the map.

---

## Example without Changes section (single conceptual change)

Source: GMRT-49885 (NIE document mandatory)

```markdown
## Background

Previously, when the NIE document was not available in KFA (empty URL),
the field didn't exist in the category form, or the download failed,
the system silently skipped the autofill process without returning any
error. Products could be saved without the required NIE document.

## Solution

Make the NIE document mandatory by converting all three silent-skip
conditions in `constructDocumentFromKFAIdentifierIDs` into explicit
`InvalidRequest` errors.

## References

https://govtech-lkpp.atlassian.net/browse/GMRT-49885

## Demo

**Before:** when the NIE document URL was empty or the download failed,
the product was still created successfully without any NIE document.

**After:** all three failure conditions now return a clear
`InvalidRequest` error, blocking submission until resolved.
```

Why Changes is omitted here: it's one conceptual change in one function
— Solution already says exactly what changed. A Changes section here
would just repeat the same sentence in table form.