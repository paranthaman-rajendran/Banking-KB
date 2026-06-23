# China Core Banking — Regulatory Activities

What the CBS at a China-operating bank must do to satisfy the centrally-directed Chinese regulatory regime: PBoC (central bank), NFRA (banking supervisor), SAFE (FX administration), CAC (cybersecurity + data), and several others. China has the most prescriptive **data localisation + cybersecurity** regime in this set; foreign banks face additional cross-border data + ownership constraints.

> Companion: payments side at [../../06-payments/regulatory/china.md](../../06-payments/regulatory/china.md).

---

## Authorities (CBS Lens)

| Authority | CBS Touchpoint |
|---|---|
| **PBoC (People's Bank of China)** | Central bank; payment systems (CNAPS, CIPS); foreign exchange (with SAFE); AML enforcement; e-CNY operator |
| **NFRA (National Financial Regulatory Administration)** | Banking + insurance supervision (replaced CBIRC + parts of PBoC in 2023) |
| **SAFE (State Administration of Foreign Exchange)** | FX management + cross-border capital controls + RCPMIS reporting |
| **CAC (Cyberspace Administration of China)** | CSL / DSL / PIPL enforcement; data cross-border review |
| **MIIT (Ministry of Industry and Information Technology)** | Telecom + IT licensing; data |
| **STA (State Taxation Administration)** | Tax — FATCA, CRS, withholding |
| **PBoC AML Bureau** | FIU for STR submissions |
| **CFETS (China Foreign Exchange Trade System)** | FX trade infrastructure |
| **CSRC (China Securities Regulatory Commission)** | Adjacent for capital-markets-touching |

---

## Customer Identification — KYC

### PBoC + NFRA AML Regulations
Implements the **Anti-Money Laundering Law of the PRC** + **Counter-Terrorism Financing Law**:
- Customer Identification Procedures.
- Risk-based CDD + EDD.
- Periodic review.
- PEP screening.
- Beneficial Ownership (PRC-specific definitions; 25% common but check applicable rule for entity type).

### Real-Name Account Opening
- All bank accounts must be opened in the customer's real name.
- ID verification mandatory.
- For corporates: business licence + legal representative ID + UBO.

### Engine Impact
- CIF schema with full CDD + real-name verification audit trail.
- UBO data on corporate customers.
- PEP + sanctions screening at CIF.
- Mandatory STR submission to PBoC AML Bureau.

---

## Non-Bank Payment Institutions Regulations (2024)

Effective May 2024; replaced earlier PBoC Order [2010] No.2:
- Two activity types: payment processing + stored value account.
- Higher capital + governance requirements for non-bank PSPs.
- Customer fund custody at PBoC-supervised custodian.

*Mostly relevant for non-bank PSPs; for banks, it's contextual.*

---

## Cybersecurity Law (CSL, 2017)

Foundational cybersecurity law:
- **Critical Information Infrastructure (CII)** designation for major financial systems — payment systems, core banking systems typically classify as CII.
- **MLPS (Multi-Level Protection Scheme)** — graded cybersecurity controls Level 1 through Level 5.
- **Data localisation** for CII operators — data of PRC residents must stay in PRC.
- Cross-border data export security assessment required.

### Engine Impact
- CBS classified as CII — full Level 3 or 4 MLPS controls.
- Data residency enforcement — PRC customer / transaction data stays in PRC.
- Annual cybersecurity protection self-assessment + audit.

---

## Data Security Law (DSL, 2021)

- Data classification: ordinary, important, core / state-related.
- **Important data** export requires security assessment by CAC.
- **Core data** has stricter restrictions.
- Annual data security risk assessment for "important data" handlers.

### Engine Impact
- Data classification inventory across CBS schema.
- Cross-border data transfer compliance.
- Annual data security risk assessment.

---

## Personal Information Protection Law (PIPL, 2021)

China's GDPR-equivalent:
- Consent + purpose limitation.
- Data subject rights.
- Cross-border transfer: security assessment, SCC-equivalent, or PIP certification.
- Annual compliance audit.
- Sensitive personal information additional protections (biometric, financial info classed).

### Engine Impact
- Customer data right APIs.
- Consent capture per processing purpose.
- Cross-border transfer mechanism per processing flow.
- Annual PIPL compliance audit support.

---

## Anti-Money Laundering Law of the PRC

- Banks + non-bank FIs + crypto exchanges subject.
- Customer Identification Programme.
- Records retention.
- STR + LTR (Large-Value Transaction Report — RMB 50,000 cash equivalent threshold; verify current).
- Sanctions screening + freeze.

### Engine Impact
- CIF data capture + verification.
- LTR + STR pipelines to PBoC AML Bureau.
- 5-year records retention (longer for higher-risk).

---

## Foreign Exchange Regulations — SAFE

SAFE-administered cross-border controls:
- Annual individual foreign exchange quota — USD 50,000 per person.
- Corporate cross-border flows categorised by purpose (trade vs capital account).
- Capital account convertibility is restricted — payments tied to genuine trade / approved capital flow.
- **BoP (Balance of Payments) reporting** — every cross-border payment categorised per code.
- **RCPMIS** — international receipt + payment statistical system.

### Engine Impact
- Per-transaction BoP code capture.
- Per-individual FX quota tracking.
- Corporate trade documentation validation.
- Per-payment SAFE reporting integration.

---

## Sanctions

China runs its own sanctions list (limited compared to US/EU/UK). **Critical**: US OFAC + EU sanctions can reach CN-based entities indirectly via USD/EUR chain → secondary sanctions effect.

### Engine Impact
- Multi-regime screening (CN + UN + US OFAC + EU + UK for USD-touching).
- CN-specific designations.

---

## Bank Account Management Rules

PBoC + NFRA prescribe:
- Account-opening verification.
- Single account per customer category (general accounts vs basic depository accounts).
- Account opening certificate / permit.
- Reporting of new accounts to PBoC.

### Engine Impact
- Per-account-category enforcement.
- PBoC account-opening reporting integration.

---

## Tax — State Taxation Administration

| Reporting | Notes |
|---|---|
| **FATCA** | Annual via STA to IRS (China is FATCA Model 1 IGA-equivalent) |
| **CRS** | Annual to STA (CN is CRS signatory) |
| **Withholding tax** | On interest + dividend per source rules |

### Engine Impact
- Tax-residency capture per customer + ongoing.
- Annual FATCA / CRS extracts to STA.

---

## Deposit Insurance — Deposit Insurance Fund

- Coverage: RMB 500,000 per depositor per insured institution (one of the largest globally relative to per-capita income).
- Administered by Deposit Insurance Fund Management Company (DIFMC) under PBoC.
- Annual premium per insured bank.

### Engine Impact
- Eligibility tagging per account.
- Per-depositor aggregation.
- Annual premium computation.

---

## Capital + Reporting

### NFRA Capital Rules (Basel III implementation in China)
- Capital adequacy ratio.
- Tier 1 + Total Capital ratios.
- Leverage + LCR + NSFR.
- Implementation: NFRA-issued measures (formerly CBIRC measures).

### Regulatory Returns
- Comprehensive set of monthly + quarterly + annual returns.
- All required in Chinese language to regulator-mandated formats.

### Stress Testing
- Regular industry-wide + bank-internal.
- PBoC + NFRA-led.

### Engine Impact
- Per-asset-class regulatory categorisation.
- Massive data extract pipeline.
- Chinese-language reporting outputs.

---

## e-CNY — Digital Yuan

PBoC's CBDC. Banks participating in pilot integrate as **operating institutions** that distribute e-CNY to customers.

### Engine Impact (For Participating Banks)
- e-CNY wallet linkage to customer account.
- e-CNY transaction processing.
- Interoperability with deposits.
- Reporting per PBoC e-CNY pilot guidance.

---

## Foreign Bank Specific

Foreign banks operating in China typically run a **separately licensed CN subsidiary** (locally incorporated bank) or **branch** with localised tech stack.

### Specific Restrictions
- Ownership caps + governance requirements (relaxed in recent years).
- Localised cybersecurity programme.
- Data localisation strictly enforced.
- Cross-border data flows to global head office require PIPL + DSL compliance.
- Often deployed on local cloud (Alibaba Cloud, Tencent Cloud, AWS Beijing/Ningxia, Azure China — operated by local partners).

### Engine Impact
- Separately deployed CBS instance.
- Data sovereignty enforced.
- Limited / no synchronisation to global CIF.

---

## Dormant Accounts

- PBoC-prescribed dormancy rules.
- Long-dormant balances may be transferred to specific accounts at PBoC.

### Engine Impact
- Dormancy classification per PBoC rules.
- Customer outreach + transfer workflow.

---

## CBS Year-End Activities — China Specific

| Activity | Driver |
|---|---|
| Calendar year-end (31 Dec — all banks) | Fixed |
| Annual FATCA + CRS extracts to STA | March / April |
| Annual SAFE BoP reconciliation | SAFE |
| Annual CSL cybersecurity protection audit | CSL |
| Annual data security risk assessment | DSL |
| Annual PIPL compliance audit | PIPL |
| Annual independent AML audit | PBoC AML Bureau |
| Annual NFRA capital + regulatory returns | NFRA |
| Annual deposit insurance premium | DIFMC |
| Annual e-CNY pilot reporting (if participating) | PBoC |
| Year-end CNY-FCNR equivalent valuations | FX-impacted |

---

## CBS Compliance Checklist — China

| Capability | Driver |
|---|---|
| CIF with full real-name CDD + UBO + tax residency | AML Law + PBoC |
| PEP + sanctions + adverse media screening at CIF | AML Law |
| Multi-regime sanctions screening (CN + UN + US OFAC + EU + UK) | Mixed |
| LTR + STR pipeline to PBoC AML Bureau | AML Law |
| Per-transaction BoP code capture | SAFE |
| Per-individual FX quota enforcement | SAFE |
| Corporate cross-border documentation validation | SAFE |
| SAFE RCPMIS reporting integration | SAFE |
| CSL Critical Information Infrastructure controls (MLPS Level 3/4) | CSL |
| Data localisation enforcement (CN data in PRC) | CSL |
| DSL data classification + cross-border export controls | DSL |
| PIPL consent + cross-border transfer compliance | PIPL |
| Annual cybersecurity + data + PIPL audits | CSL / DSL / PIPL |
| Annual FATCA + CRS extracts to STA | STA |
| Deposit Insurance Fund eligibility tagging + premium computation | DIFMC |
| e-CNY interface (if participating) | PBoC |
| Bank Account Management Rules — account-category enforcement | PBoC |
| NFRA capital + regulatory returns (Chinese language) | NFRA |
| Chinese-language disclosures + customer communications | Local practice |
| Cross-border data flow management with global parent | PIPL + DSL |
| 5-year+ records retention | AML Law |

---

## Sources to Ingest

- Law of the People's Bank of China
- Banking Supervision Law + NFRA measures
- Anti-Money Laundering Law of the PRC + implementing measures
- Counter-Terrorism Financing Law
- Cybersecurity Law (2017) + implementing rules + MLPS standards
- Data Security Law (2021)
- Personal Information Protection Law (2021)
- SAFE foreign exchange regulations + BoP code catalogue
- Non-Bank Payment Institutions Regulations (2024)
- PBoC e-CNY pilot guidance
- NFRA capital adequacy + liquidity rules
- Deposit Insurance Regulations
- PRC sanctions designations
- STA FATCA + CRS guidance
- Internal: CN entity compliance manual, SAFE reporting pipeline docs, data classification inventory, MLPS certification

---

## Open Questions

- [ ] Confirm CN entity license type + scope (subsidiary vs branch).
- [ ] Confirm CBS deployment posture (local cloud / on-prem / hyperscaler-CN-region).
- [ ] Confirm MLPS classification + level for CBS.
- [ ] Confirm PIPL cross-border transfer mechanism (security assessment / SCC / PIP certification).
- [ ] Confirm e-CNY pilot participation.
- [ ] Confirm CN entity tax-residency model + FATCA / CRS reporting state.
- [ ] Confirm CN-region data flow to global parent + compliance basis.
