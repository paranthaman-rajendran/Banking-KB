# Singapore Core Banking — Regulatory Activities

What the CBS at a Singapore-operating bank must do to satisfy MAS — the unified financial regulator. MAS is one of the most prescriptive central banks globally for technology + operational risk; CBS implementations are heavily examined.

> Companion: payments side at [../../06-payments/regulatory/singapore.md](../../06-payments/regulatory/singapore.md).

---

## Authorities (CBS Lens)

| Authority | CBS Touchpoint |
|---|---|
| **MAS (Monetary Authority of Singapore)** | Single authority: banking + capital markets + insurance + payments; Notices + Guidelines |
| **SDIC (Singapore Deposit Insurance Corporation)** | Deposit insurance scheme administrator |
| **STRO (Suspicious Transaction Reporting Office)** | FIU; STR submissions |
| **PDPC (Personal Data Protection Commission)** | PDPA enforcement |
| **IRAS (Inland Revenue Authority of Singapore)** | Tax — FATCA, CRS, withholding |
| **ABS (Association of Banks in Singapore)** | Industry body — operates FAST, PayNow with MAS |

---

## Banking Act

The foundational statute for licensed banks in Singapore. Sets:
- License categories (full, wholesale, offshore — historically; restructured).
- Capital adequacy + liquidity baseline.
- Banking secrecy + duty of confidentiality.
- Investments + exposure limits.
- Audit + reporting.

### Engine Impact
- License-aware product routing.
- Banking secrecy controls on customer data.
- Large exposure tracking.

---

## Customer KYC + AML — MAS Notice 626 (Banks)

The dominant AML/CFT directive for banks. Covers:
- CDD + EDD + SDD.
- Risk-based approach.
- Beneficial ownership.
- PEP screening.
- High-risk customer EDD.
- Ongoing monitoring.
- Periodic refresh.
- STR submission to STRO.

(MAS Notice PSN01 covers payment service providers — analogous to Notice 626 for banks.)

### Engine Impact
- CIF schema with full CDD fields + verification audit trail.
- UBO data on entity customers (25% threshold + controlling persons).
- PEP + sanctions + adverse media screening at CIF + periodic refresh.
- Risk rating per customer driving EDD vs SDD treatment.
- STR pipeline to STRO.

---

## Banking Secrecy

Section 47 of Banking Act — strict customer information confidentiality. Exceptions are statutory (court order, MAS-specified, customer consent).

### Engine Impact
- Customer data access controls.
- Audit trail of every access.
- Information-sharing controls.
- Cross-border data flows scrutiny.

---

## MAS TRM Guidelines — Technology Risk Management

One of the most comprehensive central-bank TRM regimes globally. Covers:
- Risk governance + IT risk framework.
- IT controls (access, change, lifecycle, incident, BCP).
- IT operations + outsourcing.
- Customer-facing system controls.
- Critical system protections.
- Cybersecurity expectations.

### Notice on Cyber Hygiene
6 mandatory practices:
1. Securing administrative accounts.
2. Application of security patches.
3. Establishing secure configuration.
4. Strengthening user authentication.
5. Protecting against malware.
6. Establishing network perimeter defences.

### Engine Impact
- CBS deployment must align to TRM Guidelines.
- Annual self-assessment.
- Change-management process.
- Incident reporting pipeline.
- BCP + DR design.

---

## MAS Notice 658 — Outsourcing

- Notification + risk assessment before material outsourcing.
- Right-to-audit for MAS.
- Sub-contracting visibility.
- Annual review of outsourced arrangements.

### Engine Impact
- Vendor risk programme integration (CBS vendors, hosting, ITSPs).
- Outsourcing register.
- MAS notification flow.

---

## Personal Data Protection Act (PDPA)

- Consent + purpose limitation + notification.
- Data breach notification (within 3 calendar days of significant breach to PDPC + affected individuals).
- DPO appointment mandatory.
- Cross-border transfer rules.

### Engine Impact
- Customer data right APIs.
- Consent capture + management.
- 3-day breach notification pipeline.
- Cross-border transfer compliance.

---

## Deposit Insurance — SDIC

- Coverage: SGD 100,000 per depositor per Scheme member (raised from SGD 75,000 in 2024).
- Includes individuals + non-bank depositors (some excluded — banks, government, etc.).
- Bank pays risk-differential premiums.
- Insurance includes deposits + some structured deposits.

### Engine Impact
- SDIC eligibility tagging per account.
- Per-depositor aggregation.
- Annual SDIC contribution data.
- Customer disclosure on opening + statement.

---

## Financial Advisers Act (FAA)

- Where bank provides investment advice or sells investment products.
- Conduct + competency standards.

### Engine Impact
- Advisory-product tagging.
- Suitability assessment records.

---

## Sanctions

- MAS-administered sanctions Notices (typically UN-aligned + autonomous).
- MAS Notice on Targeted Financial Sanctions applicable to FIs.
- Real-time list integration.
- True-positive reporting to MAS.

### Engine Impact
- MAS sanctions list ingestion alongside UN / US / EU / UK.
- CIF + transaction screening.
- MAS reporting pipeline.

---

## Tax — IRAS

| Reporting | Notes |
|---|---|
| **FATCA** | Annual to IRAS (UK-US IGA equivalent) |
| **CRS** | Annual to IRAS per OECD CRS |
| **Withholding tax** | Where applicable |

### Engine Impact
- Tax-residency capture at onboarding + refresh.
- Annual FATCA + CRS extracts.

---

## Operational Resilience — Business Continuity Management (BCM)

### MAS BCM Guidelines
- BCM framework: governance, risk assessment, BCP, testing, training, review.
- Regular testing (typically annual).
- Critical service identification.
- Per-product, per-system recovery objectives.

### Engine Impact
- DR + active-active for critical systems.
- BCP test artefacts.
- Annual BCP refresh.

---

## Capital + Reporting

### Basel III (MAS-implemented)
- RWA + Capital + LCR + NSFR.
- MAS Notice 637 (Risk-Based Capital Adequacy Requirements for Singapore-incorporated banks).
- MAS Notice 649 (LCR).
- MAS Notice 652 (NSFR).

### Regulatory Returns
- MAS-prescribed returns (multiple per supervisory cycle).
- Statistical returns to MAS.
- Liquidity stress test inputs.

### Engine Impact
- Per-RWA-bucket categorisation.
- HQLA classification.
- Counterparty + sector + country aggregation for returns.

---

## Specific Products

### SRS (Supplementary Retirement Scheme)
- Tax-advantaged retirement savings account.
- Annual contribution limit (currently SGD 15,300 for Singaporeans/PRs; SGD 35,700 for foreigners; verify current).
- Withdrawal rules.

### CPF (Central Provident Fund)
- Mandatory retirement scheme; bank may handle linked accounts.
- Specific reporting.

### Investment products
- MAS-prescribed pre-sale documentation.
- Suitability assessment.

### Engine Impact
- SRS account-type tagging + contribution tracking.
- CPF-linked account workflows.
- Pre-sale documentation flow for investment products.

---

## Dormant Accounts

- Dormancy period varies (typically 6 years).
- Customer outreach before classification.
- Continued safekeeping (no central scheme like UK Reclaim Fund).

### Engine Impact
- Dormancy classification batch.
- Customer outreach workflows.

---

## CBS Year-End Activities — Singapore Specific

| Activity | Driver |
|---|---|
| Calendar year-end (most banks; some June 30) | Bank choice |
| Annual FATCA + CRS extracts to IRAS | March / April |
| SRS contribution year-end reconciliation | Calendar year |
| Annual MAS BCP refresh + test artefacts | Annual |
| Annual MAS TRM self-assessment | Annual |
| Annual outsourcing register review | MAS Notice 658 |
| Annual Internal Capital Adequacy + Liquidity self-assessment | MAS supervisory cycle |
| Annual Independent AML audit | MAS Notice 626 |
| Annual customer Privacy / T&C refresh | PDPA + bank policy |

---

## CBS Compliance Checklist — Singapore

| Capability | Driver |
|---|---|
| CIF with full CDD + UBO + tax residency | MAS Notice 626 |
| PEP + sanctions + adverse media screen at CIF | MAS Notice 626 + MAS Sanctions |
| MAS sanctions list real-time integration | MAS Notices |
| EDD workflow + risk-tiered refresh cadence | MAS Notice 626 |
| Banking secrecy controls | Banking Act s.47 |
| SDIC eligibility tagging + aggregation | SDIC |
| FATCA + CRS extracts to IRAS | IRAS |
| SRS account-type tracking + contribution limit | IRAS |
| MAS TRM-aligned controls (change mgmt, BCP, monitoring) | MAS TRM |
| MAS Cyber Hygiene 6 practices | MAS |
| Outsourcing register + MAS notification | MAS Notice 658 |
| PDPA consent + DSR + 3-day breach notification | PDPA |
| MAS BCM testing + critical service mapping | MAS BCM |
| MAS Notice 637 (capital) data feed | MAS Notice 637 |
| LCR / NSFR data feed | MAS Notices 649 / 652 |
| Annual independent AML audit support | MAS Notice 626 |
| Dormant account workflow | Bank policy + Banking Act |
| Cross-jurisdictional data flows (PIPL / GDPR / PDPA) | Multi-regime |

---

## Sources to Ingest

- Banking Act + subsidiary legislation
- MAS Notices: 626 (banks), PSN01/02 (PSPs), 637 (capital), 649 (LCR), 652 (NSFR), 658 (outsourcing), 656 (regulatory returns)
- MAS Cyber Hygiene Notice
- MAS Technology Risk Management Guidelines (current revision)
- MAS Business Continuity Management Guidelines
- Personal Data Protection Act + PDPC Advisory Guidelines
- Financial Advisers Act + MAS Notices on FA conduct
- SDIC Act + scheme rules
- IRAS FATCA + CRS guidance + SRS rules
- MAS sanctions notices
- Internal: MAS supervisory engagement records, TRM annual self-assessment, BCP test artefacts, outsourcing register

---

## Open Questions

- [ ] Confirm banking license tier + scope.
- [ ] Confirm MAS supervisory engagement cadence + recent thematic reviews.
- [ ] Confirm TRM compliance posture (annual self-assessment status).
- [ ] Confirm SDIC contribution + reporting cadence.
- [ ] Confirm cross-border data transfer mechanism (PDPA + CN PIPL + EU GDPR).
- [ ] Confirm CN entity if applicable (PIPL cross-border arrangement).
