# AGENTS.md — best-practices/

This tree is a routed knowledge base, not a folder to browse exhaustively.

## Hard rules

- Do not edit files in this tree directly on ordinary work. Changes go through the root `proposals/` mechanism.
- If the active technology/concern is already known and a category subindex exists (for example `react/index.md` or `go/index.md`), enter through that subindex instead of scanning the global `index.md`.
- Otherwise use `index.md` as a **clue map**, not as mandatory prose to absorb end-to-end.
- For security-relevant work, target the Security Concern Map for the active concern unless a narrower applicable subindex already points to the required security guidance.
- Open only the matching best-practice files. If no trigger matches, do not force one.
- An index/subindex entry routes to authority; it does not replace the target file's rule.
- Specialization indexes may point here, but specialization does not own these documents.
- Read full `index.md` governance/detail only when maintaining the best-practices system itself.

## Progressive indexing

Preferred retrieval:

```text
known specialization/concern
→ narrow category/subindex
→ matching file(s)
→ STOP
```

Fallback when the category is not yet known:

```text
global index
→ matching category/subindex
→ matching file(s)
```

Reading an index never implies reading all of its children.
