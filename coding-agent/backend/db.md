# RCF - Back-end / DB

> Schema definitions, migrations, repository patterns, query helpers. Consult this file before designing any new table or writing a non-trivial query.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: `users` table - Postgres canonical shape

**Project fit:** Any product that has accounts. Single source of truth for user identity columns, indices, and the auth-friendly fields most downstream tables FK against.

**Value:**

> _(Add your tested migration here - column list, types, NOT NULL / DEFAULT constraints, indices, and the `created_at` / `updated_at` trigger you use across the schema.)_

---

## Context Relevancy: Soft-delete pattern

**Project fit:** Tables where rows must be recoverable for support / compliance. Adds a nullable `deleted_at`, hides soft-deleted rows from default queries, exposes an "include deleted" override for admin tooling.

**Value:**

> _(Add your tested soft-delete migration + repository helper here, including the partial index on `deleted_at IS NULL` you use to keep query plans cheap.)_
