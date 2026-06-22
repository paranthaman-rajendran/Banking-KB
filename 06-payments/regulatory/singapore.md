# Singapore Payments — Regulatory Requirements

Singapore's payments regulation is unified under **MAS (Monetary Authority of Singapore)** and the **Payment Services Act 2019 (PS Act)**. The MAS is one of the most prescriptive central banks globally for technology and operational risk management.

> Singapore is a hub for cross-border payments — large correspondent USD + offshore CNH + ASEAN gateway flows.

---

## Authorities

| Authority | Scope | Engine Impact |
|---|---|---|
| **MAS (Monetary Authority of Singapore)** | Central bank, regulator, supervisor — single authority for banks + capital markets + insurance + payments | Direct supervisor; rules + Notices; MEPS+ + FAST operators |
| **ABS (Association of Banks in Singapore)** | Industry body | PayNow / FAST scheme operation |
| **NITC (National IT Council)** + IMDA | Tech / data governance | Data + tech oversight |
| **PDPC (Personal Data Protection Commission)** | Personal Data Protection Act enforcement | PDPA compliance |
| **STRO (Suspicious Transaction Reporting Office)** | FIU — under Commercial Affairs Department | STR submissions |

---

## Core Regulations

### Payment Services Act 2019 (PS Act)
The unifying framework for payment services since Jan 2020.

- Single licensing regime for:
  - Account issuance.
  - Domestic money transfer.
  - Cross-border money transfer.
  - Merchant acquisition.
  - E-money issuance.
  - Digital payment token services (crypto-adjacent).
- Three license tiers: **Money-changing license**, **Standard Payment Institution (SPI)**, **Major Payment Institution (MPI)**.
- MPI required when activity thresholds breached (e.g., SGD 5M average monthly e-money float).
- Safeguarding of customer funds for e-money / payment activities.

**Engine impact**:
- License-aware activity routing.
- Float / customer money safeguarding accounting.

### MAS Notice PSN01 — Prevention of Money Laundering and Countering Financing of Terrorism
- AML / CFT requirements for Payment Service Providers.
- CDD, EDD, ongoing monitoring.
- STR pipeline to STRO.

### MAS Notice PSN02 — Prevention of Money Laundering (Crypto / DPT)
- Specific AML for Digital Payment Token services.

### Banking Act + MAS Notice 626 (for banks)
- Bank-specific AML, CDD, EDD.

### MAS Notice on Cyber Hygiene + MAS TRM Guidelines
- **Technology Risk Management (TRM) Guidelines** — updated periodically; comprehensive framework for IT risk in financial institutions.
- Outsourcing notice (Notice 658) — third-party risk management.
- Cyber hygiene: 6 mandatory practices (authentication, password, malware protection, system patching, network perimeter, etc.).

**Engine impact**:
- Engine operations must align with TRM Guidelines (development lifecycle, testing, change management, incident response).
- Critical system / public-facing system controls.
- Outsourcing notification + assessment.

### Personal Data Protection Act (PDPA)
- Consent + purpose limitation.
- Data breach notification (72h to PDPC for severe; PDPC notification + individual notification thresholds).
- DPO requirement.

**Engine impact**:
- Customer data handling.
- Breach reporting pipeline.

### Sanctions
- MAS-issued sanctions Notices (typically aligned with UNSC + autonomous MAS designations).
- MAS Notice on Targeted Financial Sanctions.
- Application to financial institutions including PSPs.

**Engine impact**:
- MAS sanctions list ingestion + screening alongside UN, US, EU, UK.

---

## Payment Schemes

### FAST (Fast And Secure Transfers)
- 24x7 retail credit transfer between SG banks.
- ISO 20022 migration in progress.
- Per-FI caps; default high enough to cover most retail.

### PayNow
- Overlay on FAST.
- Aliases: mobile number, NRIC / FIN, UEN (Unique Entity Number for businesses).
- PayNow Corporate for B2B + PayNow QR.
- **PayNow ↔ UPI (India)** corridor live (Feb 2023).
- **PayNow ↔ DuitNow (Malaysia)** corridor live.
- **PayNow ↔ PromptPay (Thailand)** corridor live.
- Multiple other ASEAN corridors in roll-out.

### MEPS+ (MAS Electronic Payment System)
- RTGS for SGD.
- Direct participants are MAS-account-holding FIs.

### GIRO
- Direct debit + standing instruction.
- Bacs-equivalent.

### Cheque Truncation System (CTS)
- Image-based cheque clearing.

### eGIRO
- Digitised GIRO mandate setup over PayNow rails.

---

## Cross-Border Hub Role

Singapore is structurally a **regional cross-border hub**:
- Offshore CNH (Chinese yuan) settlement hub.
- USD correspondent banking centre.
- ASEAN payment gateway via PayNow corridors and BIS Project Nexus pilots.
- Wholesale CBDC pilots (Project Ubin, Project Orchid).

**Engine impact**:
- Multi-currency liquidity at scale.
- Cross-border instant linkage adapter library.

---

## BIS Project Nexus
SG is one of the pilot countries for Project Nexus — a multi-country instant payments hub linking IN, MY, PH, SG, TH. Production launch path TBD.

---

## What a Singapore Payment Engine Must Do — Checklist

| Capability | Driver |
|---|---|
| FAST adapter (with ISO 20022 readiness) | MAS + ABS scheme rules |
| PayNow overlay + alias resolution (mobile / NRIC / UEN) | ABS scheme |
| PayNow corridor adapters (UPI, DuitNow, PromptPay, etc.) | Cross-border instant rails |
| MEPS+ RTGS adapter | MAS |
| GIRO + eGIRO mandate handling | Scheme |
| CTS image clearing for SGD cheques | Scheme |
| PS Act activity-aware licensing routing | PS Act |
| Safeguarding of customer e-money / PI float | PS Act |
| MAS Notice PSN01 / PSN02 + Notice 626 AML compliance | MAS notices |
| STR pipeline to STRO | AML regs |
| MAS sanctions screening + UN + US + EU + UK | MAS notices + global |
| TRM Guidelines compliance (change mgmt, BCP, testing, incident response) | MAS TRM |
| Outsourcing Notice 658 vendor governance | MAS |
| PDPA data handling + breach notification | PDPC |
| Multi-currency support (SGD + USD + CNH at minimum) | Hub role |
| Wholesale CBDC interface readiness (roadmap) | MAS pilots |

---

## Sources to Ingest

- Payment Services Act 2019 + subsidiary legislation
- MAS Notices: PSN01, PSN02, 626 (banks), 658 (outsourcing), Cyber Hygiene Notice
- MAS Technology Risk Management Guidelines (current revision)
- MAS Business Continuity Management Guidelines
- ABS scheme rules — FAST, PayNow (incl. corporate, QR, corridor rules)
- MEPS+ Operating Rules
- GIRO + eGIRO scheme rules
- CTS rules
- Personal Data Protection Act + PDPC Advisory Guidelines
- MAS sanctions notices + UN designations
- BIS Project Nexus + Project Ubin / Orchid publications
- Internal: bank's MAS supervisory engagement record, TRM compliance attestations, outsourcing register

---

## Open Questions

- [ ] Confirm PS Act license tier(s) held.
- [ ] Confirm PayNow corridor portfolio + roadmap (UPI / DuitNow / PromptPay / others).
- [ ] Confirm TRM Guidelines compliance posture (annual self-assessment).
- [ ] Confirm CNH offshore settlement arrangements + counterparty banks.
- [ ] Confirm wholesale CBDC pilot participation state.
