# CBS Compliance Matrix — US / UK / Singapore / China

Cross-jurisdiction view: for each CBS compliance requirement, which jurisdictions impose it and what specific drivers apply. Use as a coverage map when assessing a CBS (Finacle, Flexcube, T24, BaNCS, Vault, FIS, Fiserv, etc.) against the bank's geographic footprint.

> Per-jurisdiction detail: [usa.md](usa.md), [uk.md](uk.md), [singapore.md](singapore.md), [china.md](china.md).

---

## Requirement → Jurisdiction Map

### Customer Identity + KYC + UBO

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **CIP at account opening (identifying info + verification)** | BSA / USA PATRIOT Act | MLRs 2017 | MAS Notice 626 | AML Law |
| **Risk-based CDD/EDD/SDD** | BSA + FFIEC | MLRs 2017 + JMLSG | MAS Notice 626 | PBoC / NFRA |
| **Beneficial Owner (UBO) at corporate entities** | FinCEN BO Rule (2024) | MLRs 2017 (PSC Register) | MAS Notice 626 | AML Law + Real-Name |
| **PEP screening + ongoing** | BSA | MLRs 2017 | MAS Notice 626 | AML Law |
| **Real-Name verification** | Implied by CIP | Implied | Implied | Explicit mandate |
| **Ongoing monitoring** | BSA | MLRs 2017 | MAS Notice 626 | AML Law |
| **Periodic refresh by risk tier** | BSA / FFIEC | MLRs 2017 | MAS Notice 626 | PBoC AML |

### Deposit Account Regulations

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Truth-in-Savings / APY disclosure** | Reg DD | BCOBS | MAS BCOBS-equivalent | PBoC rules |
| **Funds availability / Reg CC** | Reg CC | Bacs scheme rules | MAS / scheme rules | PBoC / NFRA |
| **Change in T&C notice** | Reg DD + GLBA | BCOBS | FAA + MAS | PBoC |
| **Annual statement requirements** | Reg DD + GLBA | BCOBS | MAS | PBoC |
| **Joint / minor account rules** | State law | Per jurisdiction | MAS | PBoC |

### Lending Regulations

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **APR / cost-of-credit disclosure** | Reg Z | CONC | MAS FAA / Banking Act | PBoC / NFRA |
| **Anti-discrimination** | Reg B (ECOA) | UK Equality Act | PDPA / banking rules | PRC laws |
| **Mortgage-specific (Loan Estimate, Closing)** | RESPA + Reg X | MCOB | MAS rules | NFRA |
| **Right of rescission** | Reg Z | CONC | MAS / Banking Act | Per product |
| **Credit reporting** | Reg V (FCRA) | UK GDPR + credit-bureau rules | PDPA + credit-bureau rules | PBoC Credit Reference Centre |
| **Affordability assessment** | Reg Z + CRA | CONC + Consumer Duty | MAS responsible lending | NFRA |
| **Adverse action notice** | Reg B | FCA + CONC | MAS | NFRA |
| **Anti-money laundering on lending book** | BSA | MLRs 2017 | MAS Notice 626 | AML Law |
| **Open Banking lending data access** | Section 1033 | PSRs 2017 / CMA | SGFinDex | Developing |

### Deposit Insurance

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Coverage** | FDIC USD 250k | FSCS GBP 85k | SDIC SGD 100k | DIFMC RMB 500k |
| **Eligibility tagging** | FDIC categories | FSCS Single Customer View | SDIC | DIFMC |
| **Aggregation per depositor** | FDIC categories | FSCS SCV | SDIC | DIFMC |
| **Annual scheme contribution** | FDIC quarterly | FSCS levy | SDIC premium | DIFMC premium |
| **Disclosure to customer** | FDIC sign | FSCS disclosure | SDIC disclosure | DIFMC disclosure |

### Consumer Protection

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Error resolution (EFT / unauthorised)** | Reg E (10/45 days) | PSRs 2017 (D+1 refund) | MAS / PSN | PBoC |
| **Consumer Duty / outcomes-based** | CFPB UDAAP | FCA Consumer Duty | MAS FAA | NFRA |
| **Vulnerable customer treatment** | CFPB / state | FCA FG21/1 | MAS / informal | NFRA |
| **Privacy notice** | GLBA + state | UK GDPR + DPA 2018 | PDPA | PIPL |
| **Right to access / portability / erasure** | State (CCPA / CPRA) | UK GDPR | PDPA | PIPL |

### Tax Reporting

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Customer-facing tax certs** | 1099 + 1098 + 5498 | Not standard (system-level to HMRC) | Annual cert as needed | Per arrangement |
| **Withholding mechanism** | Backup withholding (Form W-9) | CT61 if applicable | Withholding tax | Withholding |
| **FATCA** | Domestic + IGAs | HMRC pipeline | IRAS pipeline | STA pipeline |
| **CRS** | N/A (US not CRS signatory) | HMRC pipeline | IRAS pipeline | STA pipeline |
| **ISA / SRS-style tax wrappers** | Not applicable | ISA (HMRC tracking) | SRS (IRAS) | Not applicable |
| **Tax-residency capture** | Standard | Standard | Standard | Standard |

### Sanctions

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Primary list** | OFAC SDN + sectoral | OFSI Consolidated | MAS Notices | National |
| **Secondary sanctions exposure** | US OFAC global reach | EU + UN | UN | OFAC indirect (USD chain) |
| **List integration cadence** | Real-time | Real-time | Real-time | Real-time |
| **Frozen-asset reporting** | OFAC | OFSI | MAS | National |
| **CIF-level screening** | Mandatory | Mandatory | Mandatory | Mandatory |
| **5-year recordkeeping** | OFAC | SAMLA | MAS | AML Law (5+ years) |

### AML / FIU Reporting

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **SAR / STR** | FinCEN SAR | NCA SAR | STRO STR | PBoC AML Bureau |
| **Cash transaction reports** | CTR > USD 10k | Not standard | Threshold-based | LTR > RMB 50k cash |
| **Travel Rule** | FinCEN USD 3k | MLRs Travel Rule | MAS Notice 626 | AML Law |
| **Independent AML audit** | BSA + FFIEC annual | MLRs (proportional) | MAS Notice 626 annual | PBoC annual |

### Cybersecurity + Operational Resilience

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Cybersecurity programme** | FFIEC + NYDFS Part 500 | FCA / PRA op-res | MAS TRM | CSL |
| **Multi-factor authentication** | NYDFS Part 500 + best practice | FCA / PRA | MAS Cyber Hygiene | CSL |
| **Incident reporting (regulator)** | NYDFS 72h + FFIEC | FCA / PRA + ICO 72h | MAS BCM + PDPC 3-day | CSL incident reporting |
| **Critical operations / IBS classification** | FFIEC + Fed/OCC/FDIC interagency | PS21/3 + SS1/21 | MAS BCM | CII designation |
| **Annual independent test** | Penetration testing + audit | TLPT (if DORA-equivalent) | MAS TRM annual self-assess | Annual cyber audit |
| **3rd-party / outsourcing risk** | SR 13-19 + FFIEC | SS2/21 | MAS Notice 658 | CSL + 3rd-party rules |

### Data Privacy + Cross-Border

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Privacy law** | GLBA + state (CCPA/CPRA) | UK GDPR + DPA 2018 | PDPA | PIPL |
| **Breach notification** | State-level + NYDFS 72h | ICO 72h | PDPC 3-day | CAC + CN-specific |
| **Cross-border data transfer** | Largely permissive | Adequacy / SCC / BCR | PDPA cross-border | PIPL security assessment / SCC / certification |
| **Data localisation for FIs** | Not mandated | Not mandated | Implicit via secrecy + outsourcing | **Strict** CSL / DSL |
| **Data subject rights** | State-only | UK GDPR | PDPA | PIPL |

### Capital + Regulatory Reporting

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Basel III implementation** | Fed + OCC + FDIC | PRA Rulebook | MAS Notice 637 | NFRA measures |
| **LCR + NSFR** | Fed | PRA Rulebook | MAS 649 / 652 | NFRA |
| **Stress test** | CCAR + DFAST | PRA / BoE | MAS internal | PBoC + NFRA |
| **Call Reports / equivalent** | FFIEC 031/041 | PRA returns + COREP/FINREP | MAS Notice 656 | NFRA returns |
| **HMDA-equivalent** | HMDA | Not directly | Not directly | Not directly |
| **CRA-equivalent** | CRA | Not directly | Not directly | NFRA financial inclusion |
| **Pillar 3 disclosure** | Required | Required | Required | Required |
| **ICAAP** | Yes | Yes | Yes | Yes |
| **ILAAP** | Yes | Yes | Yes | Yes |
| **RRP / Living Wills** | Required (large) | BoE-led | MAS | NFRA |

### Dormant Accounts + Escheatment

| Requirement | US | UK | SG | CN |
|---|---|---|---|---|
| **Dormancy state machine** | State-by-state | Standard | MAS-aligned | PBoC |
| **Customer outreach** | State-specific | Bank policy + Dormant Asset Act | Bank policy | PBoC |
| **Transfer to scheme** | State Unclaimed Property | Reclaim Fund | None (bank holds) | PBoC scheme |
| **Annual reporting** | State-specific | Dormant Asset Scheme | MAS reporting | PBoC reporting |

### Specific Products

| Product | US | UK | SG | CN |
|---|---|---|---|---|
| **Tax-advantaged savings wrappers** | IRA / 401k linked | ISA (annual allowance) | SRS (annual contribution) | Not directly |
| **Retirement-linked accounts** | IRA + 401k | Pension SIPP-related | CPF-linked | National pension |
| **CBDC** | Limited Fed research | BoE design phase | MAS Project Orchid + others | **e-CNY live pilot** |
| **Mortgage** | Reg X + RESPA + HMDA | MCOB | MAS HDB-related | NFRA + PBoC |
| **Credit Card** | CARD Act + Reg Z | CONC + FCA | MAS FAA | PBoC + NFRA |

---

## CBS Feature Coverage Lens

For each CBS evaluation, build a feature matrix per requirement × jurisdiction. For each cell mark:

| Marker | Meaning |
|---|---|
| ✅ Built-in | CBS ships the feature; configuration only |
| 🔧 Configurable | Available through bank-side configuration / customisation |
| 🧩 Integration | Requires third-party integration (e.g., regulatory reporting tool, KYC platform) |
| ❌ Missing | Not supported; programme work needed |

Aim for ✅ or 🔧 on every cell of the bank's footprint. 🧩 is acceptable when integration partner is robust + bank has integration capability. ❌ is a programme risk.

---

## Quick Per-Jurisdiction Reference

| Jurisdiction | CBS Watchpoint (Top) | Open Banking | Tax Reporting | Data Posture | Sanctions |
|---|---|---|---|---|---|
| **US** | State-level escheatment + multi-state MTL for fintechs; CCAR data feed | Section 1033 (rolling) | 1099 + 1098 + 5498 + FATCA | State-by-state privacy | OFAC global reach |
| **UK** | FSCS SCV + Consumer Duty fair value | PSRs + CMA Open Banking + VRP | HMRC system-level + CRS + FATCA | UK GDPR | OFSI standalone |
| **SG** | MAS TRM annual self-assessment + outsourcing Notice 658 | SGFinDex | FATCA + CRS + SRS | PDPA | MAS standalone + UN-aligned |
| **CN** | CSL CII + data localisation + SAFE BoP + multi-regime sanctions (for USD chain) | Developing | FATCA + CRS to STA | PIPL + CSL + DSL (strict) | CN national + OFAC indirect |

---

## How To Use This Matrix

When evaluating a CBS for a bank operating in US + UK + SG + CN:
1. For each cell in this matrix, score the CBS as ✅ / 🔧 / 🧩 / ❌.
2. Aggregate: ❌ cells in the bank's footprint = programme risk.
3. 🧩 cells where the integration partner isn't already in the bank's stack = procurement decision.
4. 🔧 cells where customisation is heavy = TCO impact.

The decision rarely turns on a single CBS being "complete"; it turns on **how the gaps line up against the bank's footprint and existing partner ecosystem**.

---

## Open Questions

- [ ] Confirm bank's CBS evaluation criteria weighting.
- [ ] Confirm bank's footprint per cell of the matrix.
- [ ] Confirm acceptable level of customisation per requirement.
- [ ] Confirm vendor-management process for 🧩 integrations.
- [ ] Identify any cells where ❌ exists in current CBS and is on the modernisation backlog.
