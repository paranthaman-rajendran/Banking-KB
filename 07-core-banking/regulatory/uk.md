# UK Core Banking — Regulatory Activities

What the CBS at a UK-operating bank must do to satisfy the UK regulatory regime: prudential (PRA), conduct (FCA), payment system (PSR), competition (CMA / PSR), and central bank (BoE). Plus post-Brexit-onshored EU rules.

> Companion: payments side at [../../06-payments/regulatory/uk.md](../../06-payments/regulatory/uk.md).

---

## Authorities (CBS Lens)

| Authority | CBS Touchpoint |
|---|---|
| **Bank of England (BoE)** | Monetary policy; CHAPS operator; central bank reserves; FPC macro-prudential |
| **PRA (Prudential Regulation Authority)** | Banking prudential supervision — capital, liquidity, ops resilience, large exposures, RRP |
| **FCA (Financial Conduct Authority)** | Conduct supervision — consumer protection, market integrity, competition |
| **PSR (Payment Systems Regulator)** | Payment systems competition + specific directions (SD18 APP fraud, SD20 CoP) |
| **CMA** | Open Banking origin (Retail Banking Market Investigation Order 2017) |
| **HMRC** | Tax — income tax, corporation tax, FATCA UK side, CRS UK side |
| **ICO (Information Commissioner's Office)** | Data protection — UK GDPR + DPA 2018 |
| **HMT / OFSI** | Sanctions implementation + enforcement |
| **NCA (National Crime Agency)** | FIU — SAR submissions |
| **FOS (Financial Ombudsman Service)** | Consumer dispute resolution |
| **FSCS (Financial Services Compensation Scheme)** | Deposit + investor compensation |
| **TPR (The Pensions Regulator)** | Where bank touches pensions |
| **SRA + ICAEW + etc.** | Where bank operates regulated client-money services |

---

## Customer Identification + KYC

### Money Laundering Regulations 2017 (MLRs)
- Risk-based CDD on customer onboarding.
- EDD for high-risk (PEPs, high-risk countries, complex structures, correspondent relationships).
- SDD for lower-risk where applicable.
- Ongoing monitoring throughout the relationship.
- Beneficial Ownership identification (25% threshold for corporates; UBO at all levels for trusts).

### Joint Money Laundering Steering Group (JMLSG) Guidance
- Industry guidance on MLR implementation.
- HMT-approved.
- Sectoral subsections.

### Engine Impact
- CIF schema with full KYC fields + verification audit trail.
- UBO data on corporate / trust customers.
- Periodic refresh batch jobs (tier-based cadence — annual for high-risk).
- PEP + sanctions + adverse-media screening at CIF level.

---

## Conduct — FCA Handbook (Selected)

### BCOBS — Banking: Conduct of Business Sourcebook
- Pre-contract information disclosure.
- Account-opening information.
- Operational information (statements, advance notice of changes).
- Restricted reasons for terminating account / refusing services.
- Notification of changes to interest rates, fees, terms.

### CASS — Client Assets Sourcebook
- For banks handling client money (often investment / private banking adjacent).
- Segregation of client money from bank's own.
- Daily client money calculations.
- Annual CASS audit.

### CONC — Consumer Credit Sourcebook
- Consumer credit conduct rules.
- Pre-contract disclosures.
- Affordability assessment.
- Forbearance + debt-collection rules.

### MCOB — Mortgages and Home Finance Conduct
- Mortgage advice + sales standards.
- Affordability assessment.
- Pre-contract disclosures.

### PRIN — Principles for Businesses
- 11 (now 12 with Consumer Duty) principles.
- Includes Consumer Duty (Principle 12 — outcomes-based).

### Engine Impact
- Pre-contract disclosure generation.
- Notification of changes (statement + advance notice).
- Account-restriction logic + reason codes.
- Affordability assessment integration.
- CASS-applicable accounts segregated in GL + balance reporting.

---

## Consumer Duty (FCA, July 2023)

- Outcomes-based supervisory framework.
- Four outcomes: Products + services; Price + value; Consumer understanding; Consumer support.
- Cross-cutting rules: act in good faith; avoid foreseeable harm; enable + support customers.
- Senior Managers + Certification Regime accountability.
- Annual Board attestation.

### Engine Impact
- Customer journey instrumentation.
- Outcomes monitoring data (foreseeable harm indicators, product / customer profitability).
- Forbearance + vulnerable-customer support flagging.
- MI reporting at outcome level.
- Fair value assessment per product (annual).

---

## Vulnerable Customers (FG21/1)

- FCA's finalised guidance on treating vulnerable customers fairly.
- Drivers of vulnerability: health, life events, resilience, capability.
- Tailored services + communications.

### Engine Impact
- Vulnerability flag on CIF.
- Channel + product adjustments.
- Specialist queues / processes.

---

## Deposit Insurance — FSCS

- GBP 85,000 per depositor, per FCA-authorised institution.
- Temporary high balances: GBP 1M for up to 6 months (life events).
- Includes deposits + ISAs + some other products.
- Bank pays levy.

### Engine Impact
- FSCS-eligibility tagging per account.
- Aggregation across accounts for FSCS limit.
- Annual FSCS Single Customer View (SCV) — daily-runnable extract of all customer balances.
- Annual SCV audit.

---

## Senior Managers and Certification Regime (SMCR)

- Senior Managers personally accountable for areas they manage.
- Certification Regime for staff who could cause harm.
- Conduct Rules for all staff.

### Engine Impact
- User access tied to certified roles.
- Audit trail per user attributed to certified staff.
- Annual recertification.

---

## Operational Resilience

### FCA/PRA Operational Resilience Policy (PS21/3, effective 31 March 2025)
- Identify Important Business Services (IBS).
- Set Impact Tolerance per IBS.
- Self-assessment.
- Scenario testing.
- Board attestation.

### PRA SS1/21 — Operational Resilience
- Detail on impact tolerance + scenario testing.

### PRA SS2/21 — Outsourcing + Third-Party Risk
- Outsourcing arrangements + TPP risk management.

### Engine Impact
- IBS-classified system + dependency.
- Impact tolerance metrics (RTO / RPO).
- Scenario test artefacts.
- DR + active-active for IBS-classified.

---

## Data Privacy

### UK GDPR + DPA 2018
- Lawful basis for processing.
- Data Subject Rights (access, rectification, erasure, portability, etc.).
- 72h breach notification to ICO.
- DPO appointment for many banks.
- DPIA for high-risk processing.

### Engine Impact
- Customer data right APIs (access / portability / erasure).
- 72h breach reporting pipeline.
- Lawful-basis tagging per processing.
- DPIA register.

---

## Open Banking (CMA Order 2017 + PSD2-onshored + FCA Handbook)

- CMA9 banks (largest 9 UK banks) mandated.
- AISP / PISP / CBPII access via Open Banking APIs.
- VRP — Sweeping (free, CMA-mandated) + Commercial.
- OBIE (Open Banking Implementation Entity) standards.

### Engine Impact
- Open Banking API estate.
- VRP consent management.
- Transaction-data API.
- Dynamic registration of TPPs.

---

## Sanctions — OFSI

- UK Sanctions List (post-Brexit; separate from EU list).
- Real-time list integration.
- Frozen asset reporting (twice-yearly + ad-hoc).
- True-positive reporting to OFSI within tight timelines.

### Engine Impact
- Sanctions screening at CIF level + transaction level.
- Asset-freeze register.
- OFSI reporting pipeline.

---

## Tax — HMRC

| Reporting | Notes |
|---|---|
| **Interest income reporting** | Banks report to HMRC (no equivalent of 1099 customer-facing; system-level reporting) |
| **R185 (Trust interest)** | On request |
| **CRS** | Annual extract per OECD CRS |
| **FATCA UK side** | Annual extract per UK-US IGA |
| **ISA reporting** | Annual to HMRC |
| **CT61 (yearly tax return for interest withholding)** | Where applicable |
| **Bank Levy / Surcharge** | UK-specific bank profit tax |

### Engine Impact
- Tax-residency capture per customer.
- Annual reporting extracts.
- ISA-specific tracking (annual allowance per fiscal year — April 6).

---

## Capital + Regulatory Reporting

### Basel III via PRA Rulebook
- RWA + Capital + LCR + NSFR.
- Implementation under PRA Rulebook.

### COREP (Common Reporting)
- Pan-EU capital + risk reporting (UK-onshored).
- Multiple templates: capital adequacy, large exposures, leverage, liquidity.

### FINREP (Financial Reporting)
- Quantitative financial information.

### PRA Returns
- PRA101–110 series + others.
- Returns specific to UK supervisory framework.

### Internal Capital Adequacy Assessment Process (ICAAP)
- Annual bank-internal capital assessment.

### Internal Liquidity Adequacy Assessment Process (ILAAP)
- Annual liquidity assessment.

### Recovery and Resolution Plan (RRP)
- Annual refresh.
- BoE-led for resolution.

### BoE / PRA Stress Test
- Annual / biennial.

### Engine Impact
- Massive data extract for regulatory filings.
- Per-RWA-bucket categorisation.
- HQLA classification.
- Counterparty + sector + country exposure aggregation.

---

## Specific Schemes / Products

### ISA — Individual Savings Account
- Annual allowance (currently GBP 20,000 across types).
- Cash, Stocks & Shares, Lifetime, Junior, Innovative Finance variants.
- Annual reporting to HMRC.
- Customer-tracking of ISA subscriptions per tax year.

### Help to Buy / Lifetime ISA bonuses
- Government bonus on Lifetime ISA contributions.

### Engine Impact
- ISA-type tagging per account.
- Annual allowance tracking per customer per tax year.
- HMRC extracts.

---

## Dormant Accounts

### Dormant Assets Scheme
- Banks transfer dormant accounts (typically > 15 years inactive) to Reclaim Fund Ltd.
- Reclaim Fund pays out customer claims.

### Engine Impact
- Dormancy classification batch.
- Pre-transfer customer outreach.
- Annual transfer + reporting.
- Customer reclaim handling post-transfer.

---

## CBS Year-End Activities — UK Specific

| Activity | Driver |
|---|---|
| Calendar year-end fiscal close (most banks) | 31 December |
| ISA tax-year reset | 6 April |
| Annual ISA HMRC reporting | After 6 April |
| Annual CRS / FATCA extract | March / April |
| Pillar 3 disclosure publication | Per PRA timeline |
| ICAAP / ILAAP refresh | Per supervisory cycle |
| RRP annual refresh | BoE timeline |
| BoE / PRA stress test | When called |
| Annual FSCS SCV file | Annual |
| Annual customer Privacy / T&C notice | Per FCA + UK GDPR |
| Consumer Duty annual Board attestation | Annual FCA-mandated |
| Dormant Asset Scheme transfer | Annual |

---

## CBS Compliance Checklist — UK

| Capability | Driver |
|---|---|
| CIF with full KYC + UBO + tax residency | MLRs 2017 |
| PEP + sanctions + adverse media screen at CIF | MLRs 2017 + SAMLA |
| OFSI sanctions list real-time integration | SAMLA |
| OFSI frozen asset reporting | OFSI |
| MLR EDD workflow + ongoing monitoring | MLRs 2017 |
| FCA BCOBS pre-contract + ongoing disclosures | BCOBS |
| Consumer Duty outcomes telemetry + fair-value assessment | FCA Consumer Duty |
| Vulnerable customer flag + tailored support | FG21/1 |
| FSCS SCV daily-runnable | FSCS |
| FSCS eligibility tagging per account | FSCS |
| ISA tax-year tracking + annual allowance | HMRC |
| CRS + FATCA annual extracts | HMRC |
| Open Banking APIs (AISP / PISP / CBPII / VRP) | PSRs 2017 + CMA |
| CASS segregation where applicable | CASS |
| UK GDPR data subject right APIs + 72h breach pipeline | UK GDPR |
| SMCR-aligned access control + audit | SMCR |
| Operational resilience IBS metrics + scenario test | PS21/3 |
| Pillar 3 + COREP + FINREP + PRA returns extract | PRA Rulebook |
| ICAAP / ILAAP data feed | PRA |
| Dormant Asset Scheme transfer workflow | Dormant Assets Act |
| Reclaim Fund customer claim handling | Dormant Assets Act |
| Bank Levy / Surcharge calculation | Tax |

---

## Sources to Ingest

- PRA Rulebook
- FCA Handbook (PRIN, BCOBS, CONC, MCOB, CASS, SYSC, SUP)
- FCA Consumer Duty Policy Statements + Finalised Guidance
- FCA Vulnerable Customer Guidance FG21/1
- PRA Supervisory Statements (especially SS1/21, SS2/21)
- PSRs 2017, EMRs 2011, MLRs 2017, SAMLA
- UK GDPR + Data Protection Act 2018
- Joint Money Laundering Steering Group (JMLSG) Guidance
- FSCS Single Customer View Rules + Compensation Sourcebook
- CMA Open Banking Order 2017 + OBIE standards
- HMRC ISA Manager Guidance Notes
- HMRC FATCA + CRS guidance
- BoE Operational Resilience materials
- Dormant Assets Act + Reclaim Fund materials
- Internal: bank's PRA / FCA supervisory engagement record, JMLSG-aligned procedures, FSCS SCV process docs, Consumer Duty fair-value assessments

---

## Open Questions

- [ ] Confirm PRA / FCA dual-regulation scope (only PRA-regulated for tier-1).
- [ ] Confirm CMA9 status (mandates Open Banking obligations).
- [ ] Confirm FSCS SCV runnability + audit cycle.
- [ ] Confirm ISA management programme + HMRC extracts.
- [ ] Confirm operational resilience IBS inventory + tolerances.
- [ ] Confirm Consumer Duty fair-value assessment cadence.
- [ ] Confirm Dormant Asset Scheme transfer pipeline.
