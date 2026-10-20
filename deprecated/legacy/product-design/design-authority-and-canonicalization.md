# Design Authority and Canonicalization

Use this guidance when exploration has produced approved design decisions and the project needs one clear active source of truth.

Good design work can still fail downstream if approved decisions remain scattered across chats, prototypes, screenshots, old guidelines, and implementation artifacts.

Canonicalization is the discipline that turns exploration into durable authority.

## 1. Exploration evidence and canonical authority are different

Exploration may legitimately contain:

- discarded directions;
- alternative palettes;
- rejected typography;
- visual studies;
- prototype screenshots;
- generated images;
- rationale;
- unresolved questions.

Canonical authority should contain only the decisions intended to guide future work.

Do not ask engineers or agents to infer which exploration artifact “won.”

## 2. Define authority by concern

Avoid one giant design document that implicitly owns every product/design concern.

A healthy project usually separates concerns equivalent to:

```text
product/domain truth
→ product/domain specifications

stable product-design principles
→ decision principles, trust/clarity rules, readiness

selected brand/product UI direction
→ thesis, character, expressive relationship

concrete visual system
→ typography, color roles, spacing, surfaces, iconography

recurring UX patterns
→ interaction and feedback behavior

asset governance
→ truthfulness, approval, lifecycle

route/persona map
→ surface inventory / information architecture

selected visual references
→ approved evidence of direction with bounded authority
```

Exact filenames and repository layout are project-specific.

The reusable idea is concern ownership.

## 3. One active source of truth per concern

When a new design generation supersedes an old one, give each legacy artifact an explicit disposition.

Useful classifications:

```text
KEEP
REWRITE / ABSORB
DEMOTE TO EXPLORATION EVIDENCE
DELETE FROM ACTIVE TREE
```

Do not preserve contradictory active generations and expect readers to understand chronology.

Rule of thumb:

> History is an archive; the active tree is current truth.

If version control already preserves history, keeping stale design authority in the active tree often reduces safety rather than increasing it.

## 4. Harvest before deleting

Deleting old guidance is correct only after reusable knowledge has been classified.

Harvest principles that remain valid independent of the old aesthetic, for example:

- trust before persuasion;
- consequence clarity;
- progressive disclosure;
- explicit loading/empty/error semantics;
- responsive information priority;
- asset truthfulness;
- non-color-only state communication;
- provenance clarity;
- uncertainty as a valid state.

Drop generation-specific assumptions such as:

- old brand colors;
- old exact fonts;
- prototype-specific layout;
- obsolete shell composition;
- stale component architecture;
- temporary mock behavior;
- implementation details that were mistaken for design rules.

The question is not:

> Is this old?

The question is:

> Does this still express current product/design truth independent of the superseded generation?

## 5. Re-derive rather than patch blindly

When old and new design generations differ materially, patching the old docs line-by-line can preserve hidden assumptions.

A safer migration sequence is:

```text
HARVEST
→ RE-DERIVE
→ VERIFY
→ DELETE / DEMOTE LEGACY
→ INSTALL NEW AUTHORITY
```

This is especially useful when the old implementation or prototype had become an accidental source of truth.

## 6. Do not canonicalize false precision

A canonical document does not need to pretend every decision is final.

Do not freeze exact:

- palette values;
- typography;
- radius;
- spacing;
- icon family;
- photography rules;
- motion tokens;
- provenance wording;

merely because the document feels incomplete without them.

Mark material uncertainty explicitly as OPEN.

Visible incompleteness is safer than fabricated certainty.

## 7. Use proofs before promoting concrete system decisions

Concrete visual-system decisions deserve stronger evidence than a prose preference.

Before making exact visual rules canonical, validate them on representative proofs that can expose failure.

Examples:

- palette on both expressive and operational surfaces;
- typography under real information density;
- progress treatments with semantically different progress types;
- provenance treatment across known, reported, and pending states;
- responsive composition with realistic content growth.

Do not promote a token merely because it looked good in isolation.

## 8. Keep visual references subordinate to semantic authority

Every selected visual reference should have bounded authority.

A useful declaration is equivalent to:

```text
PROVES
- visual character
- hierarchy
- expressive intensity
- relationship between brand and product surfaces

DOES NOT PROVE
- domain semantics
- API fields
- permissions
- exact copy
- component contracts
- pixel-perfect production layout
```

Visual references support interpretation. They do not outrank product/domain truth.

## 9. Generated visuals need explicit status

Generated visuals can be valuable design evidence, but they are easy to over-trust because they look finished.

Classify them explicitly as one of:

- exploration candidate;
- selected direction reference;
- concrete system proof;
- approved brand asset;
- temporary placeholder.

Do not let “looks polished” silently become “is canonical.”

## 10. Human authority must be explicit

Brand-defining decisions often require human approval because they create durable identity and product precedent.

Typical human-gate decisions include:

- selected creative direction;
- logo/wordmark;
- brand-defining palette;
- typography identity;
- key illustration/photography language;
- material changes to trust/provenance presentation;
- replacing an established design generation;
- approving visual proofs as selected references.

An AI agent may explore, compare, synthesize, and document.

It should not silently approve its own brand-defining output when the project requires human ownership.

## 11. Approval should name what was approved

Avoid vague approvals such as:

> looks good

when the artifact contains many kinds of decisions.

Capture the scope of approval where practical:

```text
approved direction
approved palette roles
approved typography pairing
approved provenance grammar
approved visual reference
```

This helps later teams distinguish a selected thesis from accidental mock details.

## 12. Update routers when authority changes

Canonicalization is incomplete if the new source exists but routing still points to stale guidance.

Check applicable:

- root convention/agent files;
- frontend/mobile scoped agent files;
- architecture docs;
- design README/authority map;
- prototype/reference guidance;
- task templates;
- documentation indexes;
- comments that explicitly name removed authority.

A stale router can operationally resurrect a deleted design generation.

## 13. Search for semantic stale references, not only filenames

Legacy authority may survive after files are removed through phrases such as:

- “primary is green”;
- “follow the prototype exactly”;
- “use old design tokens”;
- “the design system is intentionally absent”;
- “prototype reference is canonical”.

Canonicalization should search for both removed paths and stale concepts.

## 14. Keep active tree clean when history already exists

Do not maintain multiple active sources of truth merely because deletion feels risky.

If the useful historical value is already preserved in Git history or explicitly archived exploration, leaving stale authority active imposes ambiguity on every future session.

Prefer clear current authority plus recoverable history.

## 15. Selected evidence is not pixel authority

Even approved visual proofs should not automatically define:

- exact component dimensions;
- responsive breakpoints;
- line-by-line copy;
- mock metrics;
- DOM hierarchy;
- component extraction;
- API contracts.

Promote the design rule, not every screenshot artifact.

## 16. Canonical design architecture should be navigable

A future engineer or agent should be able to answer quickly:

```text
Where do I learn what the product means?
Where do I learn why the experience behaves this way?
Where do I learn the visual system?
Where do I learn recurring UX behavior?
Where do I learn asset truthfulness rules?
Where do I see approved visual evidence?
```

If these answers require historical archaeology, canonicalization is incomplete.

## 17. Open decisions need ownership

Do not leave OPEN items as unowned prose.

An OPEN item should make clear enough:

- what is unresolved;
- why it matters;
- whether engineering may choose locally;
- whether human/product-design approval is required;
- whether it blocks implementation.

Not every OPEN item blocks engineering.

The important distinction is materiality.

## 18. Canonicalization checklist

Before declaring a design generation implementation-ready, verify:

```text
[ ] selected thesis/direction is human-approved where required
[ ] product/domain truth remains outside visual artifacts
[ ] stable principles are separated from concrete visual tokens
[ ] concrete visual decisions have representative evidence
[ ] visual references have bounded authority
[ ] generated assets/references have explicit status
[ ] OPEN decisions are explicit
[ ] legacy active guidance has an explicit disposition
[ ] reusable legacy knowledge was harvested before deletion
[ ] routers point to current authorities
[ ] stale semantic/path references were searched
[ ] implementation artifacts are not treated as authority by existence alone
```

## Rule of thumbs

- One concern, one active authority.
- Exploration evidence is not automatically canonical.
- Canonical does not mean “everything resolved.”
- Harvest principles before deleting a generation.
- Re-derive when patching would preserve hidden assumptions.
- Git history is usually a better archive than duplicate active docs.
- A polished generated image is still only as authoritative as explicitly approved.
- Promote rules, not screenshot accidents.
- Canonicalization includes routing cleanup.
- If future engineers must choose between conflicting generations, the migration is not finished.
