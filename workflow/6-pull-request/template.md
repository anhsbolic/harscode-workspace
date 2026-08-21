# Template: PR Description

Five sections. Background, Solution, References, and Demo are always
present. Changes is conditional — see `guidelines.md` for when to
include it.

```markdown
## Background

Why this change needs to exist. Problem / previous behavior. Short
prose, no section headers inside it.

## Solution

What was done, at a conceptual level. Use a table if there's a
toggle/rule matrix that's easier to scan than prose.

## Changes

<!-- Include this section ONLY if the change touches multiple
     separate files/points that a reviewer needs a map for. Omit it
     if the change is a single conceptual change already explained
     in Solution — don't duplicate. -->

- **`path/to/file`** — what changed and why

## References

{ticket link}

## Demo

**Before:** concrete previous behavior.

**After:** concrete new behavior. This is the section a reviewer reads
first — it should stand on its own without needing to read the code.
```