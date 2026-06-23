# Corporate Banking Channels

How corporate clients **interact** with the bank — portals, file-based connectivity, multi-bank SWIFT, APIs, ERP plug-ins. Distinct from retail digital channels in volume, complexity, and authorisation model.

---

## Bank Portals — Web-Based Corporate Banking

Each major bank has its flagship corporate banking portal. These are major engineering assets — typically 100+ engineering FTE programmes.

| Bank | Portal | Notes |
|---|---|---|
| **JPMorgan Chase** | ACCESS | Treasury Services; multi-product corporate |
| **Bank of America** | CashPro | Corporate cash mgmt + trade |
| **Wells Fargo** | CEO (Commercial Electronic Office) | Corporate access |
| **Citi** | CitiDirect / CitiDirect BE / CitiDirect Mobile | Multi-product |
| **HSBC** | HSBCnet | Global corporate platform |
| **Barclays** | iPortal / Barclays.Net | Corporate access |
| **BNP Paribas** | Connexis | Corporate platform |
| **Standard Chartered** | Straight2Bank | APAC + MEA + Europe strong |
| **DBS** | IDEAL | Singapore-led APAC dominant |
| **MUFG** | COMSUITE | Japan-strong |
| **Deutsche Bank** | db-Direct | EU corporate |
| **Société Générale** | Sogecash | EU |
| **UniCredit** | UC eBanking Global | EU |
| **ICICI** | iCorpConnect | India + cross-border |
| **HDFC** | NetBanking Corporate | India |
| **SBI** | SBI e-Trade / SBI CINB | India |

### Common Portal Capabilities
- Account information + balances + statements.
- Payment initiation (per-rail + bulk file).
- Receivables matching + lockbox visibility.
- Trade finance (LC issuance, BG issuance, doc tracking).
- Cash forecasting + reporting.
- Investment products (sweeps, MMFs).
- FX trading.
- Reporting + analytics.
- User management (corporate admin, signing rules, limits).
- Audit trail.
- Multi-entity support.

### Authentication
- Username + password (foundational).
- Hardware token / soft token / SMS / push (2FA).
- Biometric (where supported).
- Certificate-based for H2H.
- IP whitelisting + geo-restrictions.

### Authorisation Model
- Role-based (Initiator, Approver, Viewer, Admin).
- Multi-level approval (configurable per payment type + amount).
- Cut-off times per rail.
- Per-rail + per-currency + per-counterparty limits.

---

## Host-to-Host (H2H)

Corporate's ERP / treasury system **submits files directly** to the bank's gateway. Removes manual portal use.

### Protocols
- **SFTP** — dominant for file transfer.
- **AS2 (Applicability Statement 2)** — EDI-style, especially in US healthcare + retail.
- **AS4** — newer; PEPPOL standard.
- **MFT (Managed File Transfer)** platforms — IBM Sterling, Axway, Cleo.
- **HTTPS-based file upload** — newer banks.

### File Formats Inbound (Corporate → Bank)
- **NACHA ACH file** (US).
- **ISO 20022 pain.001** (CT initiation).
- **ISO 20022 pain.008** (DD initiation).
- **MT101** (Request for Transfer).
- **CSV / proprietary** (legacy).
- **EDI 820** (US payment order).

### File Formats Outbound (Bank → Corporate)
- **MT940** (EOD statement).
- **MT942** (intraday report).
- **camt.053** (ISO 20022 EOD statement).
- **camt.052** (ISO 20022 intraday).
- **BAI2** (US legacy).
- **EDI 822** (US lockbox report).
- **Custom CSV / fixed-width** (per corporate).

### Operations
- Pre-agreed file naming convention.
- Pre-agreed cut-off times.
- File acknowledgement (positive / negative).
- Reconciliation file back.
- Exception handling out-of-band.

---

## SWIFT for Corporates (S4C)

Multi-bank SWIFT connectivity for the corporate. Discussed in [treasury-services.md](treasury-services.md); summary here.

### Models
- **MA-CUG** — Member-Administered Closed User Group; bank-by-bank.
- **SCORE** — SWIFT-administered; multi-bank.
- **Bureau model** — bank or 3rd party provides SWIFT connectivity to the corporate.

### Message Types Used
- **MT101** (corporate-to-bank credit transfer).
- **MT940, MT942** (bank-to-corporate statements).
- **MT103** (in rare bank-to-bank-on-behalf-of-corporate).
- **MT798** (Trade Envelope — corporate trade messaging).
- **pain.001 / camt.053 / camt.052** (ISO 20022 equivalents).

---

## Corporate API

API-based programmatic integration. Increasingly important.

### Use Cases
- Real-time payment initiation (single + bulk).
- Real-time balance + transaction enquiry.
- Webhook for transaction events.
- Direct from corporate's microservices.
- Embedded in ERP / TWS.

### Common Bank API Estates
- **JPMC API Developer Portal**.
- **BofA APIs** (CashPro APIs).
- **Wells Wells Developer**.
- **Citi APIs**.
- **HSBC Developer Portal**.
- **Standard Chartered Developer**.
- **Bank-of-X Developer Portal** (most tier-1 have one).

### Standards
- **REST + JSON** dominant.
- **OAuth 2.0 / mTLS** for authentication.
- **OpenAPI / Swagger** for spec.
- **ISO 20022 JSON renderings** emerging.

### API Categories
- Account information.
- Payment initiation.
- Cash management (sweeps, ZBA).
- Trade finance (LC initiation, status).
- FX (rates, deal execution).
- Reporting.
- Onboarding (for fintech partners).

---

## ERP Connectors

Native integration with corporate's ERP.

| ERP | Bank-Side Connector |
|---|---|
| **SAP S/4HANA** | Bank-provided SAP-certified connector; SAP Multi-Bank Connectivity (MBC) — SAP's standardised |
| **SAP ECC** (legacy) | SAP IDOC / RFC integration |
| **Oracle ERP Cloud / EBS** | Oracle Banking adapters or REST |
| **NetSuite** | Banking + treasury connectors |
| **Microsoft D365 F&O** | Per-bank connectors |
| **Workday Financials** | Bank API connectors |
| **Sage Intacct** | Connectors for mid-market |

Modern direction: **APIs replacing IDOC / RFC / file batches**.

### SAP Multi-Bank Connectivity (MBC)
SAP-provided SaaS that connects SAP customers to many banks via a single configuration. Reduces per-bank H2H complexity for the corporate.

---

## Treasury Workstation Channels

Treasury Workstations (Kyriba, ION, FIS, SAP TRM, GTreasury, Coupa Treasury) sit between the corporate's ERP and many banks:

```
Corporate ERP → TWS → Multiple Banks (via H2H + API + SWIFT)
```

The TWS:
- Aggregates balances + transactions from all banks.
- Handles forecasting.
- Initiates payments (file out to each bank).
- Reconciles.
- Manages FX + investments.

Bank-side integration to TWS is **a recurring channel work item** for corporate banking technology.

---

## Channel Risk + Controls

### Authentication Strength
- High-value initiations need MFA + sometimes hardware token.
- IP whitelisting for H2H.
- Certificate-based authentication for sensitive APIs.

### Authorisation Workflow
- Multi-eyes approval (maker / checker / authoriser).
- Threshold-based escalation.
- Time-of-day restrictions.

### Fraud Controls
- Behavioural analytics on portal use.
- Anomaly detection on payment amounts + frequencies.
- Velocity checks.
- Beneficiary-onboarding cooldown periods.

### Audit
- Every action timestamped + user-attributed.
- Immutable audit log.
- Customer-facing audit reports.

---

## Open Questions

- [ ] Confirm bank's flagship portal + roadmap.
- [ ] Confirm H2H volume + file standards supported.
- [ ] Confirm SWIFT for Corporates / SCORE participation.
- [ ] Confirm API estate maturity + categories.
- [ ] Confirm ERP-connector partnerships.
- [ ] Confirm TWS integration coverage.
