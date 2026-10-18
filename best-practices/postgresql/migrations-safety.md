# PostgreSQL Migration Safety

> **Status:** Station 5 C1 research revision candidate; experimental branch only, not operational `main`.
> **Scope:** Schema evolution of PostgreSQL databases, including existing production data.
> **Triggers:** migration, ALTER TABLE, default, NOT NULL, backfill, index, rollback, deployment.

## 01 — Applicability

Apply to changes that may affect existing data, live writes, locks, constraints or deployment order. An empty development database has different risks from a populated live table; a green local migration is not a production safety proof.

## 02 — Principle / Rule

- Design migrations for actual table size, data state, PostgreSQL version, lock duration and compatible application rollout.
- **Do not claim** `ADD COLUMN ... NOT NULL DEFAULT false` necessarily fails on existing rows: a valid non-null constant default supplies the value. On modern PostgreSQL, adding a constant default normally avoids rewriting every row; it can still acquire a consequential lock.
- For derived/backfilled values or incompatible rolling deploys, prefer additive schema change, data backfill in safe batches, validation, then constraint tightening.
- Treat destructive changes, irreversible transforms, uniqueness changes, and lock-heavy operations as distinct high-risk decisions needing planned fallback.

## 03 — Rationale & Risk

Generic nullable-first advice can create unnecessary steps or incorrect claims, while an indiscriminate one-step `ALTER` can block production writes, fail on inconsistent data, or break old application versions. A migration can succeed yet still misclassify or erase historical data.

## 04 — Application Guidance

1. Establish existing-row assumptions and write a before/after data invariant.
2. If the default is a correct value for *all* existing rows and deployment compatibility is adequate, adding a constant non-null default may be appropriate. Confirm database/version behavior and lock tolerance.
3. If the value requires per-row computation, add nullable/new representation, backfill with measured batches, validate, then enforce `NOT NULL`/FK/UNIQUE as justified.
4. For unique constraints, first detect/remediate actual duplicates; plan concurrent index creation or other online strategy where required.
5. Plan upgrade ordering, monitoring, tested down migration or an explicit forward-recovery strategy. A `down` file cannot magically undo lost data.

## 05 — Verification

Test upgrade against a representative populated DB including NULLs/duplicates and old/new application compatibility. Assert invariant preservation, failure behavior and rollback/fallback. When impactful, measure lock/statement time in representative conditions. Record PostgreSQL version and executed SQL; do not infer deployment safety from linting alone.

## 06 — Boundaries & Trade-offs

Simple early-stage schemas may not need multi-release rollout. Large/critical tables may need careful online migration even for syntactically simple alterations. This guidance does not demand staged backfills universally and does not authorize applying migrations to protected databases.

## References

- https://www.postgresql.org/docs/current/ddl-alter.html
- https://www.postgresql.org/docs/current/sql-altertable.html
