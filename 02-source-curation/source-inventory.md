# Source Inventory

Source curation is **70% of the work**. For capital markets the sources are diverse and have different freshness, ownership, and approval requirements.

> Companion docs: [freshness-matrix.md](freshness-matrix.md) (ingestion cadence) and [canonical-lifecycle.md](canonical-lifecycle.md) (approval workflow).

---

## Product Documentation

| Source | Owner | System | Sensitivity |
|---|---|---|---|
| Term Sheets & Pricing Supplements | Structuring Desk | SharePoint / Doc Mgmt | Confidential |
| Product Approval Memos (PAM / NPAC) | Product Approval Committee | SharePoint | Confidential |
| Indicative Term Sheets (ITS) | Sales / Structuring | Doc Mgmt | Confidential |
| Final Prospectuses / Base Prospectuses | Legal | Doc Mgmt | Internal/Public |
| Structured Product Payoff Definitions | Quants | GitHub / Internal Wiki | Confidential |

## Legal & Contractual

| Source | Owner | System | Sensitivity |
|---|---|---|---|
| ISDA Master Agreements (2002 / 1992) | Legal | Doc Mgmt | Confidential |
| Credit Support Annexes (CSA / VM-CSA / IM-CSA) | Legal | Doc Mgmt | Confidential |
| GMRA (Repo) | Legal | Doc Mgmt | Confidential |
| GMSLA (Securities Lending) | Legal | Doc Mgmt | Confidential |
| Confirmations & Trade Confirmations | Middle Office | OMS / Doc Mgmt | Confidential |

## Regulatory & Compliance

| Source | Owner | System | Sensitivity |
|---|---|---|---|
| Regulatory Circulars (RBI, SEBI, IRDAI) | Compliance | Regulator portals | Public |
| Prudential Regulations (Basel III/IV CRR3) | Compliance | BIS / EBA / national regulators | Public |
| Reporting Standards (EMIR, DTCC, MAS TRs) | Compliance | TR portals | Public |
| Internal Compliance Policies | Compliance | Confluence | Internal |

## Risk & Quant

| Source | Owner | System | Sensitivity |
|---|---|---|---|
| Risk Policy Documents | Risk Management | Confluence / Doc Mgmt | Internal |
| Model Documentation (validation reports) | Model Risk | Doc Mgmt | Restricted (model IP) |
| Greeks & Sensitivity Definitions | Quants | Internal Wiki | Internal |
| Stress Testing Scenarios | Risk | Doc Mgmt | Confidential |
| FRTB / SA / IMA Documentation | Risk | Doc Mgmt | Internal |

## Market Data & Reference Data

| Source | Owner | System | Sensitivity |
|---|---|---|---|
| Instrument Reference Data (ISIN, CUSIP, LEI) | Reference Data Ops | RDS / DWH | Internal |
| Benchmark Rate Definitions (SOFR, SONIA, ESTR, MIBOR) | Market Data Team | Bloomberg / Refinitiv | Public/Internal |
| Index Compositions & Rebalancing Rules | Index providers | Vendor feeds | Public |
| Holiday Calendars | Reference Data Ops | RDS | Internal |

## Technology & Operations

| Source | Owner | System | Sensitivity |
|---|---|---|---|
| FIX Protocol Specifications | Tech Platform | FIX Trading Community + internal extensions | Internal |
| API Contracts (REST, FIX, SWIFT MX) | Tech Platform | GitHub / Schema Registry | Internal |
| Data Contracts & Schema Registries | Data Platform | Schema Registry | Internal |
| Settlement SOPs & Runbooks | Operations | GitHub / Confluence | Internal |
| Incident Reports | SRE / Ops | Confluence / PagerDuty | Confidential |

## Research & Intelligence

| Source | Owner | System | Sensitivity |
|---|---|---|---|
| Internal Research Reports | Research | Research Portal | Internal/Confidential |
| Earnings Call Transcripts | Vendor (Refinitiv / FactSet) | Vendor feed | Public |
| Credit Rating Reports (Moody's, S&P, CRISIL) | Vendor | Vendor feed | Internal |
| Market Commentary | Research / Vendor | Research Portal / Vendor | Internal/Public |

---

## Phase 2 (Structured Products Pilot) Scope

Only these source sets are in scope for the first pilot:

- Term Sheets (50–100 historical)
- Product Approval Memos
- Payoff Definitions
- Risk Policy Documents (Structured Products section)
- ISDA + CSA templates (master + relevant addenda)
- MiFID II suitability rules (Articles 24–25)

Everything else waits for Phase 3 expansion.

---

## Open Questions for Phase 1 Sign-off

- [ ] Confirm authoritative system for each row (one row may have multiple — pick the canonical one).
- [ ] Confirm owner-team mapping aligns with entitlement service group names.
- [ ] Identify any sources missing from the inventory.
- [ ] Resolve sensitivity tier ambiguity (e.g., are prospectuses Public or Internal during draft window?).
