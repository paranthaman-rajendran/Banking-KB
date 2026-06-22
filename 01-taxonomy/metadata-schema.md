# Mandatory Metadata Schema

Every document chunk in the production index MUST carry the fields below. These fields drive routing, filtering, access control, and lineage. Missing fields fail the ingestion gate.

> **Phase 1 deliverable.** Lock this schema before any ingestion code is written.

---

## Field Reference

| Field | Type | Required | Values / Examples | Why |
|---|---|---|---|---|
| `domain` | enum | yes | `CapitalMarkets`, `Risk`, `Compliance` | Top-level routing |
| `sub_domain` | enum | yes | `FixedIncome`, `StructuredProducts`, `XVA` | Precision retrieval |
| `product_class` | string (free) | when applicable | `IRS`, `Autocallable`, `CLO`, `G-Sec` | Product-level scoping |
| `sensitivity_tier` | enum | yes | `Public`, `Internal`, `Confidential`, `Restricted` | Access control |
| `regulatory_tag` | array<string> | when applicable | `MiFID2`, `DoddFrank`, `SEBI`, `BaselIII` | Compliance search |
| `source_system` | string | yes | `Confluence`, `Bloomberg`, `SharePoint`, `GitHub` | Lineage |
| `data_as_of` | date (ISO) | yes for market data | `2025-06-01` | Freshness for market data |
| `effective_date` | date (ISO) | yes for policies | `2025-01-01` | Policy validity window start |
| `expiry_date` | date (ISO) | yes for policies | `2026-01-01` | Auto-expire stale policy |
| `owner_team` | string | yes | `Structured Products Desk`, `Risk Engineering` | Escalation contact |
| `geography` | array<enum> | yes | `IN`, `EU`, `US`, `APAC`, `GLOBAL` | Regulatory jurisdiction |
| `language` | enum | yes | `en`, `de`, `fr` | Multi-jurisdiction |
| `approval_status` | enum | yes | `Draft`, `Reviewed`, `Approved`, `Canonical`, `Superseded`, `Archived` | Lifecycle gate |

---

## Ingestion Gate Rules

A chunk is rejected from the production index unless ALL of the following hold:

1. `approval_status == Canonical` — no draft or reviewed-only content in production.
2. `effective_date <= today` AND (`expiry_date IS NULL` OR `expiry_date > today`).
3. `sensitivity_tier` is set and matches one of the four enum values.
4. `domain` and `sub_domain` are codes from [taxonomy.md](taxonomy.md).
5. `owner_team` resolves to a registered team in the entitlement service.
6. `source_system` is in the registered source allowlist.

Failures route to a quarantine queue with the failing field surfaced to the owner.

---

## Derived / System Fields (added by the platform)

These are added by the ingestion pipeline. Do not set them at source.

| Field | Description |
|---|---|
| `chunk_id` | UUID v4 |
| `document_id` | Stable ID for the parent document |
| `document_version` | Monotonic version per document |
| `chunk_hash` | sha256 of normalized text — change detection |
| `ingested_at` | UTC timestamp |
| `embedding_model` | Model + version used to embed |
| `chunking_strategy` | Strategy name (e.g., `clause`, `section`, `step`) |

---

## Examples

### Term sheet chunk
```yaml
domain: CapitalMarkets
sub_domain: StructuredProducts
product_class: Autocallable
sensitivity_tier: Confidential
regulatory_tag: [MiFID2]
source_system: SharePoint
effective_date: 2025-03-15
expiry_date: 2026-03-15
owner_team: Structured Products Desk
geography: [EU]
language: en
approval_status: Canonical
```

### Regulatory circular chunk
```yaml
domain: Compliance
sub_domain: MiFID2
sensitivity_tier: Internal
regulatory_tag: [MiFID2, MiFIR]
source_system: Confluence
effective_date: 2025-01-01
expiry_date: null
owner_team: Compliance
geography: [EU]
language: en
approval_status: Canonical
```

### SOP / Runbook chunk
```yaml
domain: TechPlatform
sub_domain: Operations
sensitivity_tier: Internal
source_system: GitHub
effective_date: 2025-05-01
expiry_date: 2026-05-01
owner_team: Settlement Operations
geography: [IN]
language: en
approval_status: Canonical
```

---

## Open Questions for Phase 1 Sign-off

- [ ] Should `client_id` be a top-level field for client-confidential chunks, or namespace-isolated?
- [ ] Should MNPI / insider-info be a separate `sensitivity_tier` value or a flag?
- [ ] Do we need a `desk_code` field for desk-level entitlements, or is `owner_team` enough?
- [ ] Final list of accepted `source_system` values.
