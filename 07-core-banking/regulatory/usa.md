# USA Core Banking — Regulatory Activities

What the CBS at a US-operating bank must do to satisfy the layered US regulatory regime: federal-level (Fed, OCC, FDIC, CFPB, FinCEN, OFAC, IRS), state-level (state banking regulators, NMLS, NYDFS), and supervisory frameworks (FFIEC, BSA Exam Manual).

> Companion: payments side at [../../06-payments/regulatory/usa.md](../../06-payments/regulatory/usa.md).

---

## Authorities (CBS Lens)

| Authority | CBS Touchpoint |
|---|---|
| **Federal Reserve Board (FRB)** | Reg D / E / J / CC / DD / Z; Bank supervision (state member banks); HMDA reporting; CCAR / DFAST stress test inputs |
| **OCC** | National bank supervision; OCC Heightened Standards; Operating Subsidiaries; Bulletins |
| **FDIC** | Deposit insurance; state non-member bank supervision; risk-based pricing |
| **CFPB** | Consumer protection — Reg E (EFT), Reg Z (TILA), Reg DD (TIS), Reg X (RESPA), Reg V (FCRA), Section 1033 |
| **FinCEN** | BSA enforcement — CIP, CDD/EDD, BO Reporting, SAR/CTR filing |
| **OFAC** | Sanctions (intersects with payments, but also customer-level screening at CIF) |
| **IRS** | Tax reporting — 1099 series, 1098, FATCA, withholding |
| **NCUA** | Federal credit union supervisor |
| **State Banking Regulators** | State-chartered banks; state-level consumer protection; escheatment |
| **NYDFS** | NY-specific; Part 500 (cybersecurity); 23 NYCRR 200 (cyber + consumer) |
| **FFIEC** | Inter-agency examination guidance; IT Examination Handbook |
| **PCAOB** | Public company audit oversight (CBS data feeds external audit) |

---

## Customer Identification + KYC (CIP / CDD / BO)

### CIP — Customer Identification Program
- BSA / USA PATRIOT Act-mandated.
- Required information at account opening: name, address, DOB, government ID number (SSN, ITIN, passport for non-US).
- Verification methods (documentary + non-documentary).

### CDD — Customer Due Diligence
- Risk-based approach.
- Identify ongoing transaction monitoring profile.
- Periodic refresh.

### Beneficial Ownership Reporting (FinCEN BO Rule)
- Final rule (2024-onwards rollout; verify current state).
- Requires reporting on entities' beneficial owners (≥ 25%) and controlling persons.
- Affects KYB at account opening + ongoing.

### Sanctions + PEP Screening at CIF
Distinct from payment-level screening — the CIF itself is screened on:
- Account opening.
- Periodic refresh (continuous).
- On adverse media events.

### Engine Impact
- CIF schema must hold all CIP fields + verification audit trail.
- BO data must be stored + refreshed.
- Risk rating must be re-computed on event triggers.
- Periodic refresh batch jobs.

---

## Deposit Account Regulations

### Regulation D (12 CFR 204) — Reserve Requirements
- Historical 6-transaction limit on savings accounts (largely relaxed during COVID; many banks still impose).
- Reserve requirement at Fed (currently zero since March 2020).
- CBS classifies accounts as transaction / non-transaction.

### Regulation DD (12 CFR 1030) — Truth in Savings (TIS)
- Annual Percentage Yield (APY) disclosure.
- Account opening disclosure.
- Change-in-terms notices.
- Periodic statement disclosures.
- Annual notice for tiered-rate accounts.

### Regulation CC (12 CFR 229) — Funds Availability + Check 21
- Next-business-day for most deposits.
- Exception holds with notice.
- Substitute checks (IRDs).
- Hold periods + reasons documented.

### Regulation E (12 CFR 1005) — Electronic Fund Transfers
- Account opening disclosure (initial + change).
- Periodic statement requirements.
- Error resolution: 10 business days standard, 45 days extension with provisional credit.
- Unauthorized EFT liability: USD 50 / 500 / unlimited tiered by notification timing.

### Engine Impact
- Account opening packet generation (multi-document).
- APY calculation per product configuration.
- Hold logic + customer notification.
- Error-resolution workflow + provisional credit posting.
- Period-end statement generation with required disclosures.

---

## Lending Regulations

### Regulation Z (12 CFR 1026) — Truth in Lending Act (TILA)
- APR disclosure.
- Right of rescission (3 days for principal residence).
- Open-end (revolving) vs closed-end disclosure differences.
- Schumer Box for credit cards.
- Periodic statement requirements.
- Billing error resolution.

### Regulation B (12 CFR 1002) — Equal Credit Opportunity Act (ECOA)
- Anti-discrimination in credit decisions.
- Adverse action notice within 30 days of decision.
- Spousal signature restrictions.

### Regulation X (12 CFR 1024) — RESPA (Mortgage)
- Good Faith Estimate / Loan Estimate.
- Settlement Statement (HUD-1 / Closing Disclosure).
- Servicing transfer disclosures.
- Force-placed insurance rules.

### Regulation V (12 CFR 1022) — FCRA
- Credit reporting accuracy.
- Adverse action notices.
- Customer ability to dispute.
- Identity theft processes.

### Home Mortgage Disclosure Act (HMDA)
- Annual reporting of mortgage applications + decisions.
- Demographic data on applicants.
- Loan Application Register (LAR).

### Community Reinvestment Act (CRA)
- Bank's record of meeting credit needs in its assessment area.
- Examination + rating.
- CBS feeds geo-coded lending data.

### CARD Act (2009)
- Credit card consumer protections.
- Rate change restrictions.
- Late fee caps.
- Over-limit opt-in.

### Engine Impact
- Loan origination workflow with multi-document disclosures.
- APR calculation per product.
- Adverse action engine + reason codes.
- HMDA LAR generation + submission.
- CRA geo-data tagging.
- Right of rescission tracking.

---

## Deposit Insurance — FDIC

- USD 250,000 per depositor, per insured bank, per account ownership category.
- Categories: single, joint, retirement, revocable trust, irrevocable trust, employee benefit, government, corporation / partnership / unincorporated.
- Bank pays risk-based assessments quarterly.
- Annual reporting on insured deposit base.

### Engine Impact
- Insurance category tagging per account.
- Aggregation per depositor per category.
- Disclosure on account opening + statement.
- Annual FDIC Call Report deposits-detail extract.

---

## Bank Secrecy Act (BSA) + AML

| Requirement | CBS Activity |
|---|---|
| **CIP at account opening** | CIF data capture + verification audit trail |
| **CDD ongoing monitoring** | Periodic refresh + risk re-rating |
| **CTR — Currency Transaction Report** | Cash transactions > USD 10k aggregated per customer per day |
| **SAR — Suspicious Activity Report** | Pattern detection — AML system consumes CBS transaction data |
| **Travel Rule (USD 3,000)** | Originator/beneficiary data captured + propagated on outbound wires |
| **5-Year recordkeeping** | BSA documentation retention |
| **Beneficial Owner (FinCEN BO Rule, 2024)** | Entity-customer BO data captured + verified |

---

## Privacy

### Gramm-Leach-Bliley Act (GLBA)
- Customer financial information protection.
- Annual Privacy Notice (Reg P).
- Safeguards Rule.
- Opt-out for sharing with non-affiliated 3rd parties.

### State Privacy Laws
- CCPA / CPRA (California), Virginia, Colorado, others.
- Per-state right to know, delete, opt-out.

### Engine Impact
- Privacy preference per customer.
- Annual notice distribution.
- Data export for CCPA requests.
- Deletion / suppression workflows.

---

## Cybersecurity & Operational Resilience

### NYDFS Part 500 (23 NYCRR 500)
- Cybersecurity programme; CISO appointment.
- Annual certification by senior officer.
- Multi-factor authentication.
- Encryption of NPI in transit + at rest.
- Incident notification within 72 hours.
- 3rd-party risk management.

### FFIEC IT Examination Handbook
- Inter-agency guidance: governance, infrastructure, operations, audit, business continuity, retail payment systems, wholesale payment systems, AIO.
- Examined by federal banking regulator.

### Interagency Operational Resilience Guidance (Oct 2023)
- Banks classified by risk profile.
- Critical operations identified.
- Impact tolerance for disruptions.

### SR Letters (Fed Supervisory)
- **SR 11-7** — Model Risk Management.
- **SR 13-19** — Third-Party Risk.
- **SR 23-4** — ICT Risk.
- Many others.

### Engine Impact
- Encryption at rest + in transit.
- MFA on all admin + sensitive customer access.
- Comprehensive logging + immutable audit trail.
- Incident detection + reporting pipeline.
- DR + active-active for critical operations.

---

## Tax Reporting

| Form | Coverage | Threshold |
|---|---|---|
| **1099-INT** | Interest income | USD 10 generally |
| **1099-DIV** | Dividend income | USD 10 |
| **1099-B** | Brokerage proceeds | All |
| **1099-MISC / 1099-NEC** | Miscellaneous / non-employee comp | USD 600 |
| **1098** | Mortgage interest paid | USD 600 |
| **1098-T** | Tuition | All |
| **1098-E** | Student loan interest | USD 600 |
| **5498** | IRA contributions | All |
| **1042-S** | Withholding on foreign persons' US source income | All |
| **W-9 / W-8 series** | Tax-status validation forms (filed by customer) | At onboarding + refresh |

### FATCA — Foreign Account Tax Compliance Act
- Foreign FIs report US-person accounts; US FIs identify foreign accounts.
- Annual reporting.
- Withholding penalty (30%) on non-compliant payments.

### Engine Impact
- Tax-status data on CIF.
- Annual 1099 / 1098 etc. generation + mailing.
- Backup withholding logic for unverified TINs.
- FATCA classification + extract.

---

## CFPB-Specific (Recent)

### Section 1033 — Personal Financial Data Rights
- Finalised October 2024.
- Phased compliance (largest banks first).
- Free, secure consumer + authorized 3rd-party access to financial data via APIs.
- FDX-aligned in practice.

### Junk Fees + Overdraft
- CFPB rules on overdraft fees (Dec 2024; verify current).
- NSF fee restrictions.
- Late fee caps on credit cards.

### Larger Participants Rule (Digital Wallets)
- CFPB supervisory authority over large non-bank wallet apps.

### Engine Impact
- API estate for Section 1033 compliance.
- Fee schedule re-design for caps.
- Consumer data access + audit.

---

## Capital + Regulatory Reporting

### Basel III Capital
- Risk-weighted assets (RWA) computation.
- Tier 1 + Total Capital ratios.
- Leverage ratio.
- LCR (Liquidity Coverage Ratio).
- NSFR (Net Stable Funding Ratio).

### CCAR (Comprehensive Capital Analysis and Review)
- Annual stress test for large banks (USD 100B+).
- Capital action plan submission.

### DFAST (Dodd-Frank Act Stress Test)
- Stress scenarios from Fed.
- Quantitative + qualitative review.

### Call Reports (FFIEC 031 / 041)
- Quarterly Reports of Condition and Income.
- Detailed balance sheet + income statement data.
- Schedule RC + RI + many supplementary schedules.

### FR Y-9C / Y-9LP
- Holding company reports.

### FR 2052a
- Liquidity reporting (daily for very large banks).

### Engine Impact
- Massive data extract for regulatory filings.
- Categorisation per regulatory schema (HQLA classification, RWA bucketing, etc.).
- Audit-defensible data lineage.
- Per-product, per-counterparty, per-segment aggregation.

---

## State-Level

### NYDFS Cybersecurity (already covered above)

### State Escheatment / Unclaimed Property
- Each state has its own dormancy + reporting rules.
- Holder reports filed annually (varies by state — Mar / Apr / Jul / Nov common).
- Different dormancy periods per state per account type.
- Multi-state national banks file multi-state reports.

### State Money Transmitter Licensing (MTL)
- Affects sponsor-bank arrangements — fintech downstream customers may be in states where bank holds MTL or relies on bank-charter shield.

### Engine Impact
- Multi-state escheatment workflow.
- State-by-state reporting templates.
- MTL coverage mapping for fintech partners.

---

## Dormancy + Escheatment

- Dormancy threshold per state (typically 3–7 years).
- Pre-escheatment customer notice (statutory).
- Annual escheatment file generation.
- Funds transfer to state Unclaimed Property programme.
- Post-escheatment customer reclaim handling.

---

## CBS Year-End Activities — US Specific

| Activity | Driver |
|---|---|
| 1099-INT / 1098 / 1099-B / 1098-T / E generation | IRS by 31 Jan |
| Reg P annual privacy notice | GLBA |
| Reg DD APY annual notice | Where applicable |
| State escheatment file generation | Per state calendar |
| FDIC year-end deposit report | Quarterly Call Report |
| FATCA annual extract | IRS / Bank Secrecy Act |
| CCAR / DFAST submission | Fed timeline (Apr/Jun typical) |
| HMDA LAR submission | CFPB by 1 March |
| CRA performance evaluation prep | OCC / FDIC / FRB |
| Annual model validation cycle | SR 11-7 |

---

## CBS Compliance Checklist — US

| Capability | Driver |
|---|---|
| CIF schema with full CIP fields + verification audit | BSA / USA PATRIOT Act |
| BO data on entity customers | FinCEN BO Rule |
| Continuous OFAC + PEP + sanctions screening on CIF | OFAC + BSA |
| Reg E error-resolution workflow + provisional credit | Reg E |
| Reg DD APY computation + annual notice | Reg DD |
| Reg CC funds availability hold logic | Reg CC |
| Reg Z APR calc + adverse action engine | Reg Z + Reg B |
| HMDA LAR data capture + extract | HMDA |
| CRA geo-coded lending data | CRA |
| FATCA classification + 1042-S | FATCA |
| 1099 series tax cert generation | IRS |
| GLBA annual privacy notice | GLBA |
| NYDFS Part 500 controls (where applicable) | NYDFS |
| FDIC insurance category tagging + aggregation | FDIC |
| Multi-state escheatment workflow | State law |
| Call Report extract | FFIEC 031/041 |
| CCAR / DFAST data feed | Fed |
| Section 1033 API estate | CFPB |
| SR 11-7 model documentation | Fed |
| Operational resilience controls | FFIEC + Fed/OCC/FDIC interagency |

---

## Sources to Ingest

- 12 CFR — Federal banking regulations (Parts 204, 210, 226 / 1026, 229, 235, 1002, 1005, 1024, 1030)
- BSA Examination Manual
- FinCEN regulations + BO Rule
- FFIEC IT Examination Handbook
- NYDFS Part 500 + 23 NYCRR 200
- CFPB Section 1033 final rule + amendments
- Federal Reserve SR Letters (especially 11-7, 13-19, 23-4)
- FDI Act + FDIC regulations
- IRS Pub 1220 (1099 specs), FATCA guidance
- HMDA + CRA regulations
- OCC Bulletins
- State banking laws + state unclaimed property laws
- Internal: bank's BSA compliance manual, OFAC playbook, state MTL footprint, FFIEC self-assessment

---

## Open Questions

- [ ] Confirm federal supervisor (FRB / OCC / FDIC) + state footprint.
- [ ] Confirm Section 1033 readiness roadmap + tier.
- [ ] Confirm FinCEN BO Rule implementation state for entity customers.
- [ ] Confirm FATCA + CRS pipeline ownership.
- [ ] Confirm CCAR / DFAST data feed maturity.
- [ ] Confirm state-by-state escheatment workflow.
- [ ] Confirm NYDFS Part 500 applicability + certification cycle.
