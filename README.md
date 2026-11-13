<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/header-dark.svg">
  <img src="assets/header-light.svg" alt="mnevfel" width="360">
</picture>

# Mustafa Nevfel

I'm a software architect and founder in Izmir, Türkiye. I run Mobixify, an independent software studio, and write engineering notes with code.

I have worked on production software since 2013, across the full stack: backend, frontend, mobile, AWS and real-time systems.

## Notes

Newest first. Each note carries working code.

- `2026-10-24` [Freeze invoices as snapshots: totals, rule versions and numbering](https://mnevfel.com/notes/invoice-is-a-snapshot-not-a-calculation/)
- `2026-10-23` [Design the reconnect first: sequence numbers, replay and snapshots](https://mnevfel.com/notes/design-the-reconnect-first/)
- `2026-10-23` [Run AI agents like queue workers: briefs, budgets and stop reasons](https://mnevfel.com/notes/running-ai-agents-like-production-systems/)

Shorter code references are at [mnevfel.com/snippets](https://mnevfel.com/snippets/). All notes are at [mnevfel.com/notes](https://mnevfel.com/notes/).

From [Gapless invoice numbering in PostgreSQL without a sequence](https://mnevfel.com/snippets/gapless-invoice-numbering-postgresql/). The row lock orders issuers, and a rollback gives the number back.

```sql
-- per issue, READ COMMITTED (the default)
BEGIN;
UPDATE number_counters SET last_seq = last_seq + 1
WHERE tenant_id = $1 AND series = $2
RETURNING last_seq;          -- zero rows: no such series, ROLLBACK
INSERT INTO documents (id, tenant_id, series, seq_no, idempotency_key)
VALUES ($3, $1, $2, $4, $5); -- $4 is the last_seq returned above
COMMIT;                      -- on any error, including 23505: ROLLBACK
```

## Open source

- `2026-11-13` [pg-gapless](https://github.com/mnevfel/pg-gapless): Gapless invoice and receipt numbers in PostgreSQL for Node.js, safe under retries and rollbacks

## Work

Most of my work was for employers and clients, so it is not public.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/seam-dark.svg">
  <img src="assets/seam-light.svg" alt="" width="100%">
</picture>

[mnevfel.com](https://mnevfel.com) · [Now](https://mnevfel.com/now/) · [LinkedIn](https://www.linkedin.com/in/mnevfel) · [X](https://x.com/xmnevfel)
