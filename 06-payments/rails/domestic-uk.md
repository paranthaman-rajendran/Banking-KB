# Domestic UK Payment Rails

Authoritative references: **Pay.UK Scheme Rules (FPS, Bacs, Image Clearing)**, **Bank of England CHAPS Reference Manual**, **PSR specific directions**, **Payment Services Regulations 2017**, **FCA Handbook (BCOBS, SUP, SYSC, CASS for client money)**, **HMT sanctions guidance**.

> Sub-domain: `DomesticUK`
> Owner: Payments Product + Operations (UK)
> Default sensitivity: `Internal` (scheme rules); `Confidential` (transaction data, PII)

---

## At-a-Glance Comparison

| Rail | Operator | Settlement Model | Window | Typical Use | Limit |
|---|---|---|---|---|---|
| Faster Payments (FPS) | Pay.UK | RTGS-style on net deferred basis | 24x7x365 | Retail credit transfers, push, Open Banking | GBP 1M scheme cap (FI may apply lower) |
| CHAPS | Bank of England | RTGS, real-time gross | ~22h/business day | High value, time-critical, property, treasury | No limit |
| Bacs Direct Credit | Pay.UK | Deferred net (3-day cycle) | Business days | Payroll, supplier payments | None |
| Bacs Direct Debit | Pay.UK | Deferred net (3-day cycle) | Business days | Recurring bills, subscriptions, mandates | None |
| Image Clearing System (ICS) | Pay.UK | Image exchange + Bacs settlement | Business days | Cheques | None |
| LINK | LINK Scheme | Net settlement via CHAPS | 24x7 | ATM cash withdrawal | Issuer-set |
| Card networks (UK) | Visa, Mastercard, Amex | Auth → clearing → net settle | 24x7 | POS, e-comm, contactless | Issuer-set |
| Open Banking — PISP | OBIE / FCA | Initiates over FPS (typically) | 24x7 | Account-to-account at consent layer | FPS / scheme cap |
| Variable Recurring Payments (VRP) | OBIE / commercial APIs | FPS underneath | 24x7 | "Sweeping" + commercial VRP | Per consent + FPS cap |

Always cite the latest Pay.UK / BoE / FCA publication when quoting limits.

---

## Faster Payments Service (FPS)

**Operator**: Pay.UK (Pay.UK Ltd, formerly New Payment System Operator).
**Live**: 2008. **Migration target**: New Payments Architecture (NPA) — ISO 20022 native, multi-year rollout.
**Model**: Near real-time credit (seconds), deferred net settlement (three settlement cycles/day via RTGS).
**Standard**: ISO 8583-derived (legacy); ISO 20022 under NPA.
**Scheme cap**: GBP 1,000,000 per transaction; FIs may set lower limits.

### Architecture
```
Sender Customer → Sender FI → FPS Central Infrastructure (Pay.UK)
                                    → Receiver FI → Receiver Customer
```

### Variants
- **SIP** — Single Immediate Payment (the workhorse)
- **Forward-Dated Payment** — scheduled future payment
- **Standing Order** — recurring SIP
- **DCA / Return** — return of incorrectly-routed
- **CoP (Confirmation of Payee)** — mandatory name-check at payment initiation

### NPA — New Payments Architecture
Pay.UK's multi-year migration of FPS (and ultimately Bacs) to a single ISO 20022-native platform. Materially affects:
- Message structure (free text → structured)
- Validation rules
- Confirmation of Payee evolution
- Fraud telemetry sharing

---

## CHAPS — Clearing House Automated Payment System

**Operator**: Bank of England (since 2017 — direct operation, previously CHAPS Clearing Company).
**Model**: RTGS, real-time gross, final, irrevocable. Settlement on BoE's books.
**Window**: Currently ~05:00 — 18:00 GMT business days (verify current schedule).
**Standard**: ISO 20022 (since 2023, replacing MT103/MT202).

### Key Points
- Final and irrevocable. Recovery for misdirection by mutual agreement only.
- Used for: house purchase completions, treasury, corporate large-value, inter-bank.
- BoE charges per-transaction; FIs typically pass through with margin.

### Recent Changes
- **Purpose codes** mandatory for many message types post-ISO 20022 migration.
- **Structured creditor/debtor** required — collapses an old loophole around free-text fields.

---

## Bacs — Direct Credit & Direct Debit

**Operator**: Pay.UK.
**Model**: Three-day cycle: Day 1 input → Day 2 process → Day 3 settle.
**Standard**: Bacs-specific (legacy) — NPA roadmap targets ISO 20022.

### Direct Credit
- Bulk credit transfers: payroll, supplier payments, pensions, government disbursement.
- 3-day cycle. T-2 input for T value.
- Replaced by FPS for many use cases but still preferred for high-volume scheduled credits.

### Direct Debit
- Customer-mandated pull: utility bills, subscriptions, insurance.
- Direct Debit Guarantee — full immediate refund if money taken in error, no questions asked.
- Mandate types: Standard, Paperless (AUDDIS — Automated Direct Debit Instruction Service).
- ARUDD / ARUCS / ADDACS reason codes for unpaid / cancelled / amended.

### Direct Debit Guarantee Implications
The Guarantee is a defining UK feature. Refunds are **immediate and unconditional** at the customer's bank, with recovery from the originator subsequently. This shapes risk and dispute economics.

---

## Image Clearing System (ICS)

**Operator**: Pay.UK.
**Model**: Cheque images exchanged digitally; settlement via Bacs.
**Live**: 2017 (national rollout 2018).

### Key Points
- Cheque clearing reduced from 6 working days to 1 working day under ICS.
- Image is the legal record (Cheques Act amendments).
- Volumes are falling rapidly but cheque clearing infrastructure remains live.

---

## LINK — ATM Network

**Operator**: LINK Scheme.
**Model**: Net settlement via CHAPS; ISO 8583-style messages between issuer and acquirer.
**Reach**: All UK consumer card-issuing banks (effectively).

### Recent Topics
- ATM access concerns — LINK + Cash Access UK addressing access in underserved areas.
- Free-to-use vs. pay-to-use ATM economics.

---

## Card Payments (UK Context)

Scheme rails are the same as global (Visa, Mastercard, Amex). UK-specific:

- **Mandatory contactless** acceptance at most merchants.
- **Contactless limit**: GBP 100 per single transaction since October 2021 (verify if changed).
- **3DS v2** for online: PSD2-derived SCA enforcement.
- **Interchange caps** — UK retains EU-style interchange caps post-Brexit (Interchange Fee Regulation IFR onshored).
- **Authorised Push Payment (APP) fraud** — distinct concern from card fraud; see PSR mandate below.

---

## Open Banking & VRP

**Authority**: Created by CMA Retail Banking Order 2017; ongoing regulatory steward is the **Open Banking Implementation Entity (OBIE)** and the **FCA**.

### PISP — Payment Initiation Service Provider
Authorized third party initiates a payment from a customer's account, typically over FPS.

### VRP — Variable Recurring Payments
- **Sweeping VRP** — mandated by CMA9; bank-funded customer's own accounts. Free.
- **Commercial VRP** — for paid-for use cases (e.g., subscription billing alternative to Direct Debit). Bilateral commercial terms; ongoing development with regulators / scheme.

### CoP — Confirmation of Payee
- Required for FPS, CHAPS, Bacs Direct Credit (rollout in phases).
- Pay.UK-operated central CoP service.
- Customer-presenting bank checks the proposed beneficiary name against the receiving bank's records before allowing the payment.

---

## APP Fraud Reimbursement (PSR Mandate)

**Authority**: Payment Systems Regulator (PSR).
**Effective**: 7 October 2024.
**Scope**: FPS and CHAPS — domestic, GBP.
**Reimbursement cap**: GBP 415,000 per claim (reduced from earlier proposal of GBP 85,000 floor with higher cap; verify current value).
**Funding**: 50/50 between sending and receiving PSPs.
**Customer excess**: PSPs may apply a GBP 100 claim excess (optional).
**Vulnerable customer exemption**: No excess or threshold applies for vulnerable customers.

This is a **structural shift**: receiving FIs are now jointly liable for APP fraud, creating strong incentives for receiver-side fraud detection.

---

## Regulators & Authorities (UK Payments)

| Body | Scope |
|---|---|
| **Bank of England** | CHAPS operator; RTGS Renewal Programme; payment systems oversight |
| **FCA** | Authorisation and conduct supervision of PSPs, EMIs, banks; Open Banking conduct; consumer protection |
| **PRA** | Prudential supervision of dual-regulated banks + significant payment institutions |
| **PSR (Payment Systems Regulator)** | Competition + economic regulation of payment systems; CoP, APP fraud, interchange |
| **Pay.UK** | Operator of FPS, Bacs, ICS, CoP central service |
| **HMT (HM Treasury)** | Sanctions regime; financial services legislation |
| **OFSI (Office of Financial Sanctions Implementation)** | HMT's sanctions enforcement arm |
| **ICO** | Data protection regulator (UK GDPR + DPA 2018) |
| **NCA (National Crime Agency)** | Financial Intelligence Unit; SARs (Suspicious Activity Reports) |
| **Cifas** | Industry fraud database |
| **FOS (Financial Ombudsman Service)** | Consumer dispute resolution |
| **FSCS** | Deposit / investor compensation scheme |

---

## Key Regulations

| Regulation | Scope |
|---|---|
| **Payment Services Regulations 2017 (PSRs 2017)** | UK-onshored PSD2 derivative; PSP authorisation, SCA, consumer protections |
| **Electronic Money Regulations 2011 (EMRs)** | E-money issuer authorisation |
| **Money Laundering Regulations 2017 (MLRs)** | AML / CFT compliance for FIs |
| **Financial Services and Markets Act 2000 (FSMA)** + **2023 amendments** | Foundation for FCA / PRA regulation |
| **Sanctions and Anti-Money Laundering Act 2018 (SAMLA)** | Post-Brexit sanctions framework |
| **UK GDPR + DPA 2018** | Data protection |
| **Cheques Acts** (as amended) | Image clearing legal basis |
| **Interchange Fee Regulation (IFR)** (onshored) | Card interchange caps |
| **Consumer Duty (FCA, July 2023)** | Higher standard of customer outcomes; significant for payments customer journeys |
| **PSR specific directions** (e.g., SD18 on APP fraud, SD20 on CoP) | Binding directions on scheme participants |

---

## Distinctive UK Features (vs. US / EU)

| Feature | UK | Why It Matters |
|---|---|---|
| Confirmation of Payee | Mandatory, central operator | Reduces APP fraud, reshapes UX |
| APP Fraud Reimbursement | Mandatory 50/50 PSP split | Shifts liability profile materially |
| Direct Debit Guarantee | Unconditional refund | Distinct from EU SDD Core / B2B return rules |
| Faster Payments scheme cap | GBP 1M, FI sub-limits | Higher than EU SCT Inst cap (EUR 100k now lifted in EU IPR) |
| Consumer Duty overlay | FCA-specific | Adds outcome-based supervision lens above PSRs 2017 |
| Single national CoP service | Pay.UK | Operationally distinct from anywhere else |

---

## Operational Patterns

### Cut-offs (Typical, FI-dependent)
| Rail | Typical Cut-off |
|---|---|
| FPS | 24x7 (no cut-off) |
| CHAPS | ~18:00 GMT business days |
| Bacs DC / DD | T-2 input for T value |
| ICS | EOD business days |

### Reconciliation
- FPS: daily reconciliation against Pay.UK net settlement at BoE.
- CHAPS: real-time, BoE settlement record is the canonical source.
- Bacs: 3-day cycle, with multi-day reconciliation file (BACS Returns, ARUDD/ARUCS/ADDACS).

### Sanctions Screening
- Pre-payment screening at payment initiation against OFSI consolidated list, OFAC, EU, UN.
- Post-Brexit, UK runs its own sanctions list — distinct from EU's. Dual-screening required for many flows.
- True-positive hits are HMT/OFSI reportable.

---

## Sources to Ingest

- Pay.UK scheme rules (FPS, Bacs, ICS, CoP)
- Pay.UK NPA programme documentation
- BoE CHAPS Reference Manual + RTGS Renewal updates
- PSR specific directions (SD18, SD20, etc.) + policy statements
- FCA Handbook (BCOBS, SYSC, SUP, CASS, FINMAR) and FCA payments-relevant policy statements
- PRA Rulebook (Capital, Liquidity, Operational Resilience)
- PSRs 2017, EMRs 2011, MLRs 2017, SAMLA, IFR (onshored)
- OFSI consolidated sanctions list (real-time) + guidance
- NCA SAR guidance
- Internal: bank's FPS / CHAPS / Bacs operations runbooks, CoP routing tables, APP fraud reimbursement procedure, Consumer Duty payments mapping

---

## Open Questions

- [ ] Confirm bank's CHAPS direct participant status (or settlement agent arrangement).
- [ ] Confirm internal FPS sub-limits and reasoning (per scheme cap is GBP 1M).
- [ ] Confirm CoP coverage of all relevant message types in the bank's product set.
- [ ] APP Fraud Reimbursement operational status — claims handling team, evidence packages, defence-of-PSP processes.
- [ ] NPA migration internal plan — affects message-translation chunks in the KB.
- [ ] Open Banking / VRP commercial usage — drives KB content on consent management.
