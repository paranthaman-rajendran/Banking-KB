# Payments — Source Inventory

Payments-specific source list. Extends the master [../02-source-curation/source-inventory.md](../02-source-curation/source-inventory.md).

---

## Scheme Rulebooks & Operating Circulars

| Source | Owner | System | Sensitivity | Freshness |
|---|---|---|---|---|
| NPCI Operating Circulars (UPI, IMPS, NACH, AePS, BBPS) | NPCI | NPCI member portal | Internal | Rolling — subscribe |
| NPCI Procedural Guidelines per rail | NPCI | NPCI member portal | Internal | Per-version |
| RBI Master Directions (Payment Systems) | RBI | rbi.org.in | Public | Per-version |
| RBI Circulars on payment systems | RBI | rbi.org.in | Public | Continuous |
| EPC SCT / SDD / SCT Inst Rulebooks | EPC | europeanpaymentscouncil.eu | Public | Annual |
| Federal Reserve Operating Circulars (5, 6, 8) | Fed | frbservices.org | Public | Per-version |
| Federal Reserve FedNow Service Description + Fraud Mitigation Toolkit | Fed | frbservices.org | Public | Per-release |
| NACHA Operating Rules & Guidelines | NACHA | nacha.org | Member-only | Annual + supplements |
| TCH RTP Operating Rules + CHIPS Rules | The Clearing House | theclearinghouse.org | Member-only | Per-release |
| Zelle / Early Warning Services operating rules | EWS | Member-only | Confidential (member) | Per-release |
| Pay.UK scheme rules — FPS, Bacs, ICS, CoP | Pay.UK | wearepay.uk | Member-only | Per-version |
| Pay.UK NPA programme documentation | Pay.UK | wearepay.uk | Member-only | Continuous |
| BoE CHAPS Reference Manual + RTGS Renewal updates | BoE | bankofengland.co.uk | Public + Member | Per-version |
| LINK Scheme rules | LINK | link.co.uk | Member-only | Per-version |
| PSR specific directions (SD18 APP fraud, SD20 CoP, etc.) | PSR | psr.org.uk | Public | Per-direction |
| OBIE standards (Open Banking, VRP) | OBIE | openbanking.org.uk | Public | Per-version |
| Banco Central do Brasil — Pix regulations | BCB | bcb.gov.br | Public | Continuous |

## Message Standards

| Source | Owner | Sensitivity | Freshness |
|---|---|---|---|
| ISO 20022 Message Definition Reports | ISO 20022 RA (SWIFT) | Public | Annual |
| SWIFT Standards MT Release | SWIFT | Member-only | Annual (Nov SR) |
| SWIFT CBPR+ Usage Guidelines | SWIFT | Member-only | Annual |
| SWIFT HVPS+ Usage Guidelines | SWIFT | Member-only | Annual |
| Operator usage guidelines (FedWire, TIPS, T2, CHIPS, RTGS) | Per operator | Member-only / Public | Per-release |
| ISO 8583 base standard + scheme profiles (Visa, Mastercard, RuPay, etc.) | ISO + schemes | Member-only / Restricted | Per-release |
| EMVCo specifications (Books, 3DS) | EMVCo | Public + member | Periodic |
| PCI DSS / PCI PIN / PCI 3DS | PCI SSC | Public | Per-version |

## Regulatory & Sanctions

| Source | Owner | Sensitivity | Freshness |
|---|---|---|---|
| RBI Master Directions + circulars | RBI | Public | Continuous |
| EBA RTS / ITS publications | EBA | Public | Continuous |
| PSD2/PSR/PSD3 texts + consultation responses | EC / EBA | Public | Per legislative cycle |
| Reg E, J, CC, II (12 CFR Parts 1005, 210, 229, 235) | US Federal Reserve | Public | Per-version |
| FinCEN guidance + BSA exam manual sections | FinCEN | Public | Continuous |
| CFPB circulars + enforcement letters on payments | CFPB | Public | Continuous |
| State money transmitter regulations + NMLS guidance | State regulators + CSBS | Public | Continuous |
| FCA Handbook (BCOBS, SYSC, SUP, CASS, FINMAR) | FCA | Public | Continuous |
| PRA Rulebook (relevant payments sections) | PRA | Public | Continuous |
| PSRs 2017, EMRs 2011, MLRs 2017, SAMLA, IFR (UK onshored) | HMT / FCA | Public | Per-version |
| OFSI consolidated sanctions list + guidance | HMT / OFSI | Public | Continuous (real-time) |
| OFAC SDN list + sectoral sanctions | US Treasury | Public | Continuous (real-time) |
| EU Consolidated List | EC | Public | Continuous |
| HMT Consolidated List | UK Treasury | Public | Continuous |
| UN Security Council Sanctions | UN | Public | Periodic |
| FATF Recommendations + Interpretive Notes | FATF | Public | Per-update |
| BIS CPMI publications | BIS | Public | Periodic |
| FinCEN guidance | FinCEN | Public | Continuous |
| Travel Rule guidance per jurisdiction | Per regulator | Public | Periodic |

## Internal — Bank-specific

| Source | Owner | Sensitivity | Freshness |
|---|---|---|---|
| Payment hub mapping tables (canonical → rail-specific) | Payments Engineering | Internal | Continuous |
| Internal validation library | Payments Engineering | Internal | Continuous |
| Reconciliation SOPs (per rail) | Operations | Internal | Per-release |
| Dispute SOPs (per rail) | Operations | Internal | Per-release |
| Sanctions playbook + escalation matrix | Compliance / Sanctions Ops | Confidential | Per-release |
| AML / FIU reporting procedures | Compliance | Confidential | Per-release |
| Incident postmortems for payment incidents | SRE / Payments Ops | Confidential | Continuous |
| Internal regulatory interpretation memos | Compliance | Internal/Confidential | Continuous |
| Customer onboarding KYC procedures | KYC Ops | Confidential | Per-release |
| Correspondent banking nostro/vostro agreements | Treasury | Confidential | Per-agreement |
| RMA matrix (SWIFT bilateral) | Payments Engineering | Internal | Continuous |
| Card scheme certification artifacts | Cards | Restricted (per scheme) | Per-cert |

## Reference Data

| Source | Owner | Sensitivity | Freshness |
|---|---|---|---|
| BIC directory (ISO 9362) | SWIFT | Public | Monthly |
| IBAN structures (ISO 13616) | ISO + national | Public | Periodic |
| ISO 4217 currency codes | ISO | Public | Periodic |
| ISO 3166 country codes | ISO | Public | Periodic |
| LEI database | GLEIF | Public | Continuous |
| RBI IFSC directory | RBI | Public | Continuous |
| Bank's correspondent network directory | Treasury | Internal | Continuous |

---

## Freshness Overrides (vs. master matrix)

Payments deviates from the master freshness matrix in these places:

| Source | Freshness Target | Method |
|---|---|---|
| Sanctions lists | Real-time | Push-driven; never poll-only |
| NPCI / scheme operating circulars | Within 1h of publication | Member portal scrape + email parsing |
| RBI press releases | Within 30 min | RSS + scraping |
| Incident postmortems | On publish | Internal workflow event |
| Scheme bulletins (Visa, Mastercard) | Within 4h | Member portal scrape |

---

## Open Questions

- [ ] Confirm member-portal access credentials and ingestion authorization for NACHA, SWIFT, Visa, Mastercard.
- [ ] Confirm internal owner for sanctions list ingestion (KB vs. dedicated screening engine).
- [ ] Identify any sources behind paywall / vendor contracts that need procurement decisions.
