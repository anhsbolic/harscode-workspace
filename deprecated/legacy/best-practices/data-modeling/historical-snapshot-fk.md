# historical-snapshot-fk.md

**Location:** `data-modeling/historical-snapshot-fk.md`

**Principle**
A plain foreign key always resolves to the referenced row's *current* state — that's correct for stable relationships, but wrong for a transactional/historical record that needs to reflect the state of the world *at the time the transaction happened*. If an `orders` row references a `sales_region_id` and that region gets reorganized six months later, a plain join now reports every historical order as belonging to the new region — silently rewriting history that should be immutable. The fix isn't to avoid the foreign key (the live relationship is still useful for other purposes); it's to *also* store a snapshot of the value that mattered at that point in time, as a plain column alongside the foreign key. The foreign key answers "what is true now"; the snapshot column answers "what was true then" — a report or audit against historical data should read the snapshot, never re-derive it through the live relationship.

**Bad**
```sql
CREATE TABLE orders (
    id UUID PRIMARY KEY,
    sales_region_id UUID NOT NULL REFERENCES sales_regions(id),
    amount NUMERIC(12,2) NOT NULL,
    created_at TIMESTAMPTZ NOT NULL
);

-- Six months later, sales_regions.id = 'north' gets renamed/reorganized
-- into two new regions. This report now silently attributes every
-- historical order to whatever 'north' currently means today —
-- the historical attribution is gone, with no error and no warning.
SELECT r.name, SUM(o.amount)
FROM orders o
JOIN sales_regions r ON r.id = o.sales_region_id
GROUP BY r.name;
```

**Good**
```sql
CREATE TABLE orders (
    id UUID PRIMARY KEY,
    sales_region_id UUID NOT NULL REFERENCES sales_regions(id), -- live relationship, for current-state queries
    sales_region_name_at_order TEXT NOT NULL,                    -- snapshot: what it was called when the order happened
    amount NUMERIC(12,2) NOT NULL,
    created_at TIMESTAMPTZ NOT NULL
);

-- Written once, at the moment the order is created:
-- INSERT INTO orders (id, sales_region_id, sales_region_name_at_order, amount, created_at)
-- VALUES (:id, :region_id, (SELECT name FROM sales_regions WHERE id = :region_id), :amount, now());

-- Historical reporting reads the snapshot — immune to later reorganization
SELECT sales_region_name_at_order, SUM(amount)
FROM orders
GROUP BY sales_region_name_at_order;

-- The live FK is still there for anything that genuinely needs "where does
-- this order's region currently sit in the org structure" — a different question.
```

**Checklist**
- [ ] Any foreign key on a transactional/historical row is evaluated for whether the *referenced entity* can meaningfully change after the transaction is recorded (reassignment, renaming, status change, restructuring)
- [ ] Where it can, a snapshot column (named to make its point-in-time nature explicit, e.g. `_at_order`, `_at_time_of_event`) stores the value that mattered at that moment, written once and never updated afterward
- [ ] Historical reports and audit views read the snapshot column, never re-derive the historical value by joining through the live foreign key
- [ ] The live foreign key is kept (not replaced) when something genuinely needs the current state of the relationship — snapshotting and the live FK serve different questions, not one replacing the other
- [ ] Stable relationships that never change after creation (e.g. an order's line-item reference to a specific product variant that's itself immutable) are not snapshotted unnecessarily — this pattern is reserved for genuinely mutable referenced entities
