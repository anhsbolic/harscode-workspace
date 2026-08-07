# Examples

## Example: Stage 1 Plan Announcement

```
I'll explore this in three areas, in this order:

1. Curation diff logic (domains/product/service.go) — need to
   understand how the skip list is actually consumed before I can say
   what adding new selectors does.
2. KFA API client + domain model mapping (domains/product/model.go,
   principal/service.go) — need to see whether `registrar` is already
   available anywhere before assuming it needs to be added from
   scratch.
3. Database layer (product_kfa table, migrations/) — last, since what
   I find in area 2 determines whether a migration is even needed.

Order is dependency-based: 3 depends on findings from 2, and 1 gives
context for why 3 matters at all. Let me know if you want a different
area or order before I start.
```

Why this is good: areas are concrete (named files/components, not
"the backend"), the order has a stated reason, and it ends by inviting
correction rather than assuming silence means approval.

---

## Example: Stage 2 Gap Analysis output (one area)

```
### Area 2: KFA API client + domain model mapping

**Current state:**
`principal/service.go` already maps `Registrar` from the Kemenkes KFA
API response into `kfa.Product.Registrar` (*string) — for both
`getKfaFarmasi` (line 1389) and `getKfaAlkes` (line 1498). This part is
done.

However, `domains/product/model.go`'s `KFA` struct has NO `Registrar`
field, and `ConstructKFADB` in `service.go` (~line 320-369) does not map
`tmp.Registrar` anywhere despite `tmp` (the KFA API response) already
having it available.

**Requirement:**
PRD requires `registrar` to act as a re-curation trigger — meaning it
must be persisted and participate in the curation diff.

**Gap:**
The value is fetched but dropped before it reaches the domain model,
database, or diff logic. Three additions needed: domain model field,
service-layer mapping, repository persistence.

**Sniffing:**
- *Misleading signal*: `Registrar *string` already exists in the KFA
  API client models and even gets mapped one layer in — someone
  skimming the codebase could easily assume this "already works" when
  it silently stops before reaching anywhere that matters.
- *Miscontext*: none found — PRD's assumption that this data is
  available from KFA is correct, just not yet wired through.
- *Risk*: low in isolation, but see Area 3 for backfill implications
  once this is wired up (existing rows will be NULL).
```

Why this is good: current state is specific (file, line, function
names), the gap is a precise statement of what's missing (not "needs
more work"), and the misleading-signal note calls out exactly why this
was easy to miss — without proposing how to fix it yet.

---

## Good clarifying question patterns for Stage 2 (gap-analysis framing, not solution framing)

**Edge case framing (concrete scenario, not abstract):**
> "What happens when the seller sends a CDAKB entry but the KFA source
> data has no URL for it?"

Concrete scenario > "what about edge cases?" — the latter tends to get
a generic non-answer.

**Backward compatibility framing (specific stakeholders):**
> "Will this break existing GraphQL clients? What happens to rows that
> already exist in the DB with the old schema?"

Naming the specific things that could break (old clients, old rows)
gets a more useful answer than "is this backward compatible?"

Note: trade-off framing ("what are the pros/cons of A vs B") belongs to
Stage 3, not here — asking it during Stage 2 is exactly the premature
solutioning this process is designed to avoid.