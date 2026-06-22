# UK Payments — Regulatory Requirements

UK payments regulation is **post-Brexit onshored** from EU PSD2 + EU-derived rules, **plus** UK-unique additions: mandatory Confirmation of Payee, APP Fraud Reimbursement, the Consumer Duty overlay, and Pay.UK / PSR scheme governance.

> Companion rail file: [../rails/domestic-uk.md](../rails/domestic-uk.md)

---

## Authorities

| Authority | Scope | Engine Impact |
|---|---|---|
| **Bank of England (BoE)** | CHAPS operator; RTGS oversight; PRA parent | CHAPS adapter compliance; RTGS Renewal Programme |
| **FCA (Financial Conduct Authority)** | PSP / bank conduct supervision; Open Banking; Consumer Duty | PSP authorisation + supervisory; Consumer Duty embedded in customer journeys |
| **PRA (Prudential Regulation Authority)** | Prudential supervision of dual-regulated banks + significant PIs | Capital / liquidity / operational resilience requirements |
| **PSR (Payment Systems Regulator)** | Competition + economic regulation of payment systems; specific directions (SDs) | SD18 APP fraud; SD20 CoP; future SDs |
| **Pay.UK** | Operator of FPS, Bacs, ICS, CoP central service | Scheme rules + CoP integration mandatory |
| **HMT (HM Treasury)** | Sanctions regime; financial services legislation | Sanctions list ingestion + statutory law |
| **OFSI** | HMT's sanctions enforcement arm | Real-time list integration |
| **ICO** | Data protection regulator | UK GDPR + DPA 2018 |
| **NCA (National Crime Agency)** | FIU; SAR submissions | SAR pipeline |
| **Cifas** | Industry fraud database | Cifas integration for fraud share |
| **FOS (Financial Ombudsman Service)** | Consumer dispute resolution | Dispute outcomes drive policy + tooling |
| **FSCS** | Deposit / investor compensation scheme | Deposit-side coverage |

---

## Core Regulations

### Payment Services Regulations 2017 (PSRs 2017)
UK-onshored PSD2 derivative — the foundation.

- PSP authorisation (incl. Authorised Payment Institutions, Small PIs, EMIs).
- **Strong Customer Authentication (SCA)** — two factors from inherence / possession / knowledge.
- **Open Banking** — PISP / AISP / CBPII access.
- Transparency: pre-contract, contract, post-execution information.
- Liability allocation for unauthorised transactions.

**Engine impact**:
- SCA enforcement at payment initiation.
- Open Banking APIs exposed to authorised TPPs.
- Unauthorised transaction handling (typically full refund within 1 business day).

### Electronic Money Regulations 2011 (EMRs)
- E-money issuer authorisation + safeguarding requirements.
- Customer funds safeguarded (segregation or insurance).

**Engine impact**:
- For e-money issuers, safeguarding posting + reconciliation segregated.

### Money Laundering Regulations 2017 (MLRs)
- Risk-based AML / CFT.
- CDD, EDD, source-of-funds verification.
- SAR submission to NCA.

**Engine impact**:
- AML / TM layer triggers + thresholds aligned.
- SAR pipeline to NCA.

### Financial Services and Markets Act 2000 (FSMA) + 2023 Amendments
- Foundation for FCA / PRA regulation.
- 2023 amendments give regulators more flexibility post-Brexit.

### Sanctions and Anti-Money Laundering Act 2018 (SAMLA)
- Post-Brexit sanctions framework.
- UK runs its own list — **distinct from EU's** — requiring dual screening for many flows.
- OFSI enforces; reporting obligation on financial sanctions exposure.

**Engine impact**:
- UK sanctions list ingestion + screening — separate from EU + US.
- True-positive reporting to OFSI.

### UK GDPR + Data Protection Act 2018
- Equivalent to EU GDPR (adequacy decision in force; verify current state).
- Lawful basis, data subject rights, breach reporting.

**Engine impact**:
- Customer data handling + retention.
- Right to erasure + portability.

### Cheques Acts (as amended)
- Legal basis for Image Clearing System (ICS).

### Interchange Fee Regulation (IFR) — Onshored
- Card interchange caps onshored from EU.
- 0.2% debit + 0.3% credit consumer card caps for domestic + intra-UK.

**Engine impact**:
- Card scheme settlement reflects interchange caps.

---

## PSR Specific Directions (SDs) — Operationally Critical

| SD | Scope | Engine Impact |
|---|---|---|
| **SD18** | APP Fraud Reimbursement | Effective 7 Oct 2024; sending + receiving PSPs share liability 50/50; max claim cap (currently GBP 415,000 per claim — verify current); applies to FPS + CHAPS domestic GBP |
| **SD20** | Confirmation of Payee | Mandatory CoP integration at point of payment initiation for FPS, CHAPS, Bacs DC at most PSPs |
| **SD19** etc. | Per direction | Per direction |

**Engine impact (SD18)**:
- Receiving PSP fraud risk now matters operationally.
- Claims-handling workflow + evidence packaging.
- Optional customer excess (GBP 100); not for vulnerable customers.
- 5-business-day reimbursement target.

**Engine impact (SD20)**:
- CoP integration at customer journey + corporate H2H.
- Match / close-match / no-match outcome handling.
- Customer must consent or override before "close-match" or "no-match" payments proceed.

---

## Consumer Duty (FCA, July 2023)
- Outcomes-based supervisory framework.
- Four outcomes: products + services, price + value, consumer understanding, consumer support.
- Cross-cutting rules.
- Requires regular outcome monitoring + senior management accountability.

**Engine impact**:
- Customer journeys (initiate / fail / dispute) must produce outcomes-aligned data.
- MI / monitoring at outcome level.

---

## SMCR — Senior Managers and Certification Regime
- Personal accountability for senior managers in regulated firms.

**Engine impact**:
- Engine ownership clarity at senior management level.
- Audit trail support for management responsibilities.

---

## Open Banking + VRP
- CMA Retail Banking Order 2017 → mandated Open Banking.
- CMA9 banks (incl. legacy Big 4 + Santander, Nationwide, RBS group, etc.) mandated.
- **Sweeping VRP** — free, mandated by CMA.
- **Commercial VRP** — bilateral commercial; rolling out.

**Engine impact**:
- Open Banking APIs (account access, payment initiation).
- VRP consent handling + audit.

---

## DORA-Equivalent + Operational Resilience
- FCA / PRA operational resilience policy (effective 31 March 2025 for "important business services").
- Impact tolerance per important business service.
- Self-assessment + scenario testing.

**Engine impact**:
- Payment processing is universally an "important business service" — full op-resilience programme applies.
- Failover testing + impact tolerance breach reporting.

---

## Pay.UK Scheme Rules

| Scheme | Scope |
|---|---|
| **FPS** | Faster Payments Service — 24x7, < 10s, GBP 1M cap |
| **Bacs** | Direct Credit + Direct Debit — 3-day cycle |
| **ICS** | Image Clearing System — cheques |
| **CoP** | Confirmation of Payee — central service |
| **NPA** | New Payments Architecture (FPS migration target — ISO 20022) |

Pay.UK publishes rule updates that PSPs must implement.

---

## BoE CHAPS Reference Manual
- Operating rules for CHAPS.
- ISO 20022 native since 2023.
- Mandatory purpose codes.
- Direct participant connectivity rules.

---

## SCA — Strong Customer Authentication (PSRs 2017 + FCA RTS)

| Factor Category | Examples |
|---|---|
| Inherence | Fingerprint, face, voice |
| Possession | Device-bound credential, hardware token |
| Knowledge | PIN, password |

Two factors from different categories required for most online + remote payments.

Exemptions:
- Low-value contactless (< GBP 100 cumulative threshold).
- Trusted beneficiary (whitelist).
- Transaction risk analysis (TRA) — for issuers with low fraud rates.
- Corporate exemption (secure corporate channels).

**Engine impact**:
- SCA enforcement at issuer + acquirer side.
- Exemption claim mechanics.

---

## Sanctions Screening — UK Specifics

- OFSI Consolidated List (separate from EU list).
- Dual screening required for any flow touching EU + UK.
- True-positive reporting to OFSI within tight timelines.
- Frozen assets reporting (twice-yearly + ad-hoc).

---

## What a UK Payment Engine Must Do — Checklist

| Capability | Driver |
|---|---|
| FPS adapter with CoP integration | Pay.UK rules + SD20 |
| CHAPS adapter with ISO 20022 + purpose codes | BoE CHAPS Reference Manual |
| Bacs DC + DD with 3-day cycle + ARUDD / ARUCS / ADDACS handling | Bacs scheme rules |
| Direct Debit Guarantee handling (immediate refund) | Bacs scheme + customer rights |
| ICS image flow | Cheques Act + Pay.UK ICS rules |
| OFSI sanctions screening (separate from EU + US) | SAMLA |
| FCA SCA + RTS-aligned authentication enforcement | PSRs 2017 |
| Open Banking PISP / AISP / VRP support | PSRs 2017 + CMA Order |
| SD18 APP Fraud Reimbursement workflow (50/50 split) | PSR SD18 |
| SD20 CoP outcome handling | PSR SD20 |
| MLR-aligned AML / TM + SAR pipeline to NCA | MLRs 2017 |
| Reg E-equivalent unauthorised transaction handling | PSRs 2017 |
| GDPR data subject rights | UK GDPR |
| Operational resilience scenario testing | FCA / PRA op res policy |
| Consumer Duty outcome telemetry | FCA Consumer Duty |
| Interchange caps applied (IFR onshored) | IFR |
| Cifas data sharing for fraud | Industry standard |

---

## Sources to Ingest

- Pay.UK FPS, Bacs, ICS, CoP scheme rules
- Pay.UK NPA programme docs
- BoE CHAPS Reference Manual + RTGS Renewal Programme
- PSR SDs (SD18, SD19, SD20, etc.) + policy statements
- FCA Handbook (BCOBS, SYSC, SUP, CASS, FINMAR, PRIN)
- FCA Consumer Duty Policy Statement + Finalised Guidance
- PRA Rulebook (relevant payments + op-res)
- PSRs 2017, EMRs 2011, MLRs 2017, SAMLA, IFR (onshored)
- OFSI Consolidated Sanctions list + guidance
- NCA SAR guidance
- UK GDPR + DPA 2018 + ICO guidance
- FCA + PRA Operational Resilience Policy Statements
- Internal: bank's PSR SD compliance procedures, APP fraud claim playbook, CoP integration playbook, Consumer Duty payments outcome mapping

---

## Open Questions

- [ ] Confirm bank's CHAPS direct participant status.
- [ ] Confirm SD18 APP fraud claim-handling team + funding policy.
- [ ] Confirm Consumer Duty outcomes mapping to payments customer journeys.
- [ ] Confirm Op Resilience Important Business Service mapping for payments.
- [ ] Confirm Open Banking + VRP commercial roll-out roadmap.
