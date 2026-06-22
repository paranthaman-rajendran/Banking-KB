# Source Freshness Matrix

Per-source ingestion cadence and method. Drives the ingestion scheduler design in Phase 2.

| Source Type | Freshness Requirement | Ingestion Method | Trigger |
|---|---|---|---|
| Regulatory circulars | Within 24h of publication | Webhook / scheduled pull | Regulator RSS or scraping |
| Term sheets & pricing | Real-time / T+0 | Event-driven ingestion | Doc Mgmt workflow event |
| Market data reference | EOD batch | Nightly scheduled | Cron + Bloomberg/Refinitiv pull |
| Internal policies | On approval | Workflow-triggered | Confluence/SharePoint approval event |
| Research reports | Within 2h | Near real-time | Research portal publish event |
| Legal agreements | On execution | Document workflow | E-signature completion event |
| Runbooks & SOPs | On publish | Git-triggered | GitHub merge to `main` |

---

## Re-ingestion Schedules

For sources without push triggers, run a poll-and-diff sweep on a fixed cadence:

| Source Group | Polling Cadence | Diff Strategy |
|---|---|---|
| Regulator portals (RBI, SEBI, EU Official Journal) | Hourly | URL + headline hash |
| Internal Confluence spaces | Every 15 min | Confluence webhook (preferred) + 6h fallback poll |
| SharePoint document libraries | Every 15 min | Graph API delta token |
| GitHub repos (SOPs, schemas) | On push (webhook) | Git commit SHA |
| Bloomberg / Refinitiv reference data | EOD (22:00 local) | Vendor-provided change file |

---

## Expiry & Auto-Retirement

- Chunks with `expiry_date < today` are marked `Superseded` and removed from the production index automatically.
- The owner of an expiring document receives an alert 30 days, 7 days, and 1 day before expiry.
- A weekly digest of expiring documents is emailed to each `owner_team`.

---

## Change Detection

- Every document has a `chunk_hash` (sha256 of normalized text).
- On re-ingestion, if any chunk hash differs from the indexed version:
  1. The new version is queued for approval (drops to `Reviewed`).
  2. The previous version stays in the index, marked `Pending Review`.
  3. The owner receives a diff-highlighted alert.
- The old version is only `Superseded` when the new version reaches `Canonical`.

This guarantees the production index is never in a state where neither version is queryable.

---

## SLA per Source Type (Phase 2 target)

| Source | Ingestion → Indexed | Approval → Indexed |
|---|---|---|
| Term sheets | < 5 min | < 30 min |
| Regulatory circulars | < 60 min | < 4 hours |
| Internal policies | < 15 min | < 30 min |
| Research reports | < 30 min | < 2 hours |
| Runbooks (Git) | < 5 min | < 15 min |

Approval-to-indexed assumes the document already cleared the canonical lifecycle.
