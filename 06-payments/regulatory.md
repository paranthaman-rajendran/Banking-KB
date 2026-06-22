# Payments Regulatory Landscape

The regulatory map for Payments differs sharply from Capital Markets. Payments regulation is heavily geography-specific (per central bank / scheme) and changes more frequently.

> **Per-jurisdiction deep-dives** (incl. engine-compliance perspective): see [regulatory/](regulatory/) — covers USA, UK, Europe, Singapore, China, Japan, plus cross-border international and an engine-compliance matrix.
>
> Companion: [../03-governance/data-classification.md](../03-governance/data-classification.md) — classification mapping for regulated content.

---

## Quick Index — Jurisdiction Deep-Dives

| Jurisdiction | Deep-Dive |
|---|---|
| Cross-border / international | [regulatory/cross-border-international.md](regulatory/cross-border-international.md) |
| USA | [regulatory/usa.md](regulatory/usa.md) |
| UK | [regulatory/uk.md](regulatory/uk.md) |
| Europe / EU | [regulatory/europe.md](regulatory/europe.md) |
| Singapore | [regulatory/singapore.md](regulatory/singapore.md) |
| China | [regulatory/china.md](regulatory/china.md) |
| Japan | [regulatory/japan.md](regulatory/japan.md) |
| Engine compliance matrix | [regulatory/engine-compliance-matrix.md](regulatory/engine-compliance-matrix.md) |

The high-level overview below is preserved for quick reference; the deep-dives carry engine-feature mapping and citations.

---

## India — RBI / NPCI

| Authority | Scope |
|---|---|
| Reserve Bank of India (RBI) | Master Directions on Payment Systems; PSS Act 2007; Master Direction on PPI (wallets); Authorization of PA/PG |
| NPCI | UPI, IMPS, NEFT operating (alongside RBI), Bharat Bill Payments, AePS, NACH |
| FIU-IND (Financial Intelligence Unit) | AML/CFT reporting (STR, CTR) |
| CERT-In | Cybersecurity reporting |
| MeitY | Data localization, IT Rules |

### Key Mandates
- **PSS Act 2007** — overall payment systems authority.
- **Data Localization (RBI 2018)** — payment system data of Indian residents must be stored in India. Only.
- **PA-PG framework** — Payment Aggregators and Payment Gateways are licensed; net worth requirements + KYC/AML duties.
- **PPI Master Direction** — wallets and prepaid instruments.
- **Recurring Transactions Framework** — for cards and UPI AutoPay; AFA (Additional Factor of Authentication) requirements.
- **Online Dispute Resolution (ODR)** — for digital payments, defined dispute SLAs.
- **Tokenisation of Card Transactions** — only tokens may be stored by merchants/PSPs (effective Sep 2022 onwards).

### NPCI Circulars
- Operating circulars for UPI, IMPS, NACH (mandate framework) — rolling publication; subscribe + ingest.
- Procedural guidelines per rail.

---

## EU — PSD2 / PSR / EBA / EPC

| Authority | Scope |
|---|---|
| European Commission | PSD2 (Directive 2015/2366), PSD3 + PSR (in legislative process), Instant Payments Regulation (IPR), EU AML Reg |
| European Banking Authority (EBA) | Regulatory Technical Standards (RTS) — SCA, Account Information Services, etc. |
| European Central Bank | TARGET2, TIPS operator; Eurosystem oversight |
| European Payments Council (EPC) | Scheme rulebooks for SEPA CT, DD, Inst |

### Key Mandates
- **PSD2** — Strong Customer Authentication (SCA), Open Banking (AISP/PISP), transparency, liability shift.
- **EBA RTS on SCA** — defines acceptable authentication factors + exemptions.
- **Instant Payments Regulation (IPR)** — applies from Nov 2024; mandatory instant CT availability for all EU/EEA PSPs offering CT.
- **PSD3 + PSR** — in process; expected to refine PSD2, especially on fraud liability and open finance.
- **EU AML Package** — single AML Rulebook + new EU AMLA authority.

### EPC Rulebooks
- SCT Rulebook (annual versions)
- SCT Inst Rulebook (annual)
- SDD Core / B2B Rulebooks
- IPI Rulebook (where in use)

---

## US — Federal Reserve / NACHA / OFAC / FinCEN

| Authority | Scope |
|---|---|
| Federal Reserve | Operates FedWire, FedNow, ACH; Reg E (consumer protection), Reg J, Reg CC |
| The Clearing House (TCH) | Operates CHIPS, RTP |
| NACHA | ACH operating rules |
| OFAC (Office of Foreign Assets Control) | Sanctions screening |
| FinCEN | BSA / AML, CTR, SAR filings, Travel Rule |
| CFPB | Consumer financial protection |
| State regulators | Money transmitter licensing (per state) |

### Key Mandates
- **Reg E** — consumer remedies for unauthorized electronic transfers.
- **Reg J** — terms governing FedWire.
- **Reg CC** — funds availability.
- **NACHA Operating Rules** — annual updates; ACH risk management, third-party sender obligations.
- **OFAC Sanctions Lists** — SDN List, sectoral sanctions; updated continuously.
- **BSA Travel Rule** — originator/beneficiary information for transfers ≥ USD 3,000.
- **FedNow Operating Circular 8 + Service Description** — scheme rules.

---

## UK — FCA / PRA / Pay.UK / BoE

| Authority | Scope |
|---|---|
| FCA | Consumer payments conduct; e-money; PSR-onshored PSD2 derivative |
| PRA | Prudential regulation of major payment institutions / banks |
| Pay.UK | Operates FPS, Bacs, Image Clearing |
| Bank of England | CHAPS operator; oversight of payment systems |
| PSR (Payment Systems Regulator) | Competition + economic regulation of payment systems |
| ICO | Data protection (UK GDPR) |

### Key Mandates
- **Payment Services Regulations 2017** (UK-onshored PSD2 derivative).
- **Confirmation of Payee (CoP)** — name-check for FPS, CHAPS, Bacs.
- **APP Fraud Reimbursement (PSR mandate, 2024)** — reimbursement obligation for authorised push payment fraud.
- **NPA — New Payments Architecture** — FPS migration to ISO 20022.

---

## Cross-Border Standards Bodies

| Body | Role |
|---|---|
| BIS CPMI | International standards on payment, clearing, settlement (PFMI) |
| IOSCO | Securities side; co-publishes some standards with CPMI |
| FATF | AML/CFT recommendations; Travel Rule (Rec 16) |
| ISO | ISO 20022, ISO 4217 (currency), ISO 13616 (IBAN), ISO 9362 (BIC) |
| G20 Roadmap on Cross-Border Payments | 2027 targets on cost, speed, transparency, access |

---

## Sanctions Regimes

| Regime | Operator | Update Cadence |
|---|---|---|
| OFAC SDN | US Treasury | Continuous |
| EU Consolidated List | European Commission | Continuous |
| HMT Sanctions | UK Treasury | Continuous |
| UN Security Council Sanctions | UN | Periodic |
| SECO (Switzerland) | Swiss State Secretariat for Economic Affairs | Continuous |
| Country-specific PEP / domestic lists | Per country | Varies |
| Internal high-risk list | Bank | Bank-controlled |

Lists must be ingested and chunked carefully — they are structured data, not prose. Per-list metadata (`source_system`, `data_as_of`) is critical. Sanctions content typically lives in a separate ingestion pipeline (not RAG-style) and is consumed by deterministic screening engines — but the **policy and rationale** documents do belong in the KB.

---

## Data Privacy & Localization

| Regime | Scope |
|---|---|
| GDPR (EU) | Personal data handling |
| UK GDPR | UK-mirrored GDPR |
| RBI Data Localization | Indian payment data must be stored in India |
| China CSL + PIPL + DSL | Comprehensive data + cross-border restrictions |
| LGPD (Brazil) | GDPR-style personal data |
| HIPAA (US) | Health data — narrow but applies to health-related payments |
| State-level US privacy laws | CCPA/CPRA (CA), etc. |

These intersect with retrieval — `geography` metadata + namespace strategy must enforce data residency.

---

## Sources to Ingest

- RBI Master Directions + circulars (subscribe to RBI press releases / circulars)
- NPCI procedural guidelines + operating circulars
- EBA RTS, ITS publications; PSD2/PSR consultation papers
- EPC Rulebooks (current versions)
- Federal Reserve Operating Circulars 5, 6, 8 + NACHA Rulebook
- BoE / Pay.UK / PSR documentation
- BIS CPMI publications, FATF Recommendations + interpretive notes
- Internal: bank's regulatory compliance manual, jurisdiction matrix, sanctions playbook

---

## Open Questions

- [ ] Confirm bank's jurisdictional footprint — drives which regulators are in scope.
- [ ] Sanctions list ingestion pipeline ownership — KB vs. dedicated screening engine.
- [ ] Define escalation between Payments KB queries and regulatory-investigation flow.
