# Europe / EU Payments — Regulatory Requirements

EU payments regulation has three centres of gravity: **PSD2 → PSD3/PSR** (conduct + Open Banking), **Instant Payments Regulation (IPR)** (real-time mandate), and **EU AML Package** (CFT). Plus GDPR for data and DORA for operational resilience.

> Companion rails: SEPA / SCT Inst / TIPS — see [../rails/cross-border.md](../rails/cross-border.md) and [../rails/real-time-rails.md](../rails/real-time-rails.md).

---

## Authorities

| Authority | Scope | Engine Impact |
|---|---|---|
| **European Commission** | Legislation: PSD2, PSD3 + PSR, IPR, EU AML Reg, GDPR, DORA, MiCA, DMA | Mandatory regulations + ITS / RTS rulemaking |
| **European Central Bank (ECB)** | Operates TARGET2 (T2), TIPS; Eurosystem oversight; ECB Banking Supervision (SSM) | Direct supervisor for significant banks; T2 + TIPS adapter rules |
| **European Banking Authority (EBA)** | Regulatory Technical Standards (RTS), Implementing Technical Standards (ITS) | RTS on SCA, AML / CFT, fraud reporting |
| **European Payments Council (EPC)** | Scheme rulebooks for SEPA CT, SDD, SCT Inst | Scheme adapter compliance |
| **EBA CLEARING** | Pan-EU CSMs: STEP2 (SCT/SDD), RT1 (SCT Inst) | Direct CSM connectivity |
| **National Competent Authorities (NCAs)** | Per-country supervisory authorities | National-level supervision (e.g., BaFin DE, AMF FR, CSSF LU, Bank of Italy, ACPR FR) |
| **AMLA — EU Anti-Money Laundering Authority** | New EU AML authority (operational from 2025) | Direct supervision of high-risk obliged entities |
| **EU Council + EEAS** | EU sanctions regimes | Real-time list integration |

---

## Core Regulations

### PSD2 — Payment Services Directive 2 (Directive 2015/2366)
Foundation since 2016 (Jan 2018 transposition).

- PSP authorisation categories: Credit Institutions, EMIs, Payment Institutions.
- **Strong Customer Authentication (SCA)**.
- **Open Banking** — AISP (Account Information), PISP (Payment Initiation), CBPII.
- Transparency: pre + post-execution information.
- Liability allocation; unauthorised transaction handling.

**Engine impact**:
- SCA at initiation.
- Open Banking APIs to TPPs.
- D+1 refund for unauthorised transactions.

### PSD3 + PSR (in legislative process)
- Splits PSD2 into a Directive (PSD3 — authorisation) and a Regulation (PSR — conduct rules).
- Expected to refine SCA exemptions, fraud liability allocation, Open Finance scope.
- Final text + transposition timing under negotiation; verify current state.

### Instant Payments Regulation (IPR) — Reg. (EU) 2024/886
**Effective**: Came into force November 2024 (phased application).

- All EU/EEA PSPs offering Euro credit transfers must also offer **SCT Instant** at the same price (no premium).
- Receiving capability: from a phased date (typically 9 months after entry into force).
- Sending capability: from a later phase.
- IBAN / Name verification ("Verification of Payee" — VoP) mandatory before SCT Inst execution.

**Engine impact**:
- SCT Inst adapter on day one for EUR-offering PSPs.
- VoP integration (EU equivalent of UK CoP).
- Price parity enforcement.

### EU AML Package
Comprehensive 2024 package replacing the AMLD series:

- **Single AML Rulebook (AML Regulation)** — directly applicable across EU.
- **AMLD6** — Directive on the new supervisory architecture.
- **EU AMLA** — new central authority, operational from 2025.
- **Travel Rule for Crypto** — extended to VASPs.

**Engine impact**:
- Common AML rules across EU.
- Beneficial ownership registers + access.
- Crypto VASP integration on fiat on-/off-ramps.

### GDPR — Regulation (EU) 2016/679
- Data protection foundation.
- Lawful basis, consent, data subject rights, breach reporting (72h to NCA), DPO requirement, DPIA for high-risk processing.

**Engine impact**:
- Lawful basis for payment data processing.
- Customer data rights flows.
- 72h breach reporting pipeline.

### DORA — Digital Operational Resilience Act
**Effective**: 17 January 2025.

- Operational resilience for financial entities + ICT third-party providers.
- ICT risk management framework.
- ICT incident reporting (major incident → competent authority within tight windows).
- Threat-led penetration testing (TLPT) for significant entities.
- Critical ICT third-party providers under direct oversight.

**Engine impact**:
- Payment processing IT under DORA scope.
- Incident reporting pipeline.
- Vendor (Finastra, Volante, Oracle, etc.) management under DORA third-party oversight.

### MiCA — Markets in Crypto-Assets Regulation
- Crypto asset issuer + service provider authorisation.
- E-money tokens + asset-referenced tokens.
- Relevant where bank touches stablecoin / crypto flows.

### Interchange Fee Regulation (Reg. (EU) 2015/751)
- Caps on consumer card interchange (0.2% debit, 0.3% credit).

### EMD2 — Electronic Money Directive
- E-money issuer authorisation framework.
- Safeguarding requirements.

---

## EBA Regulatory Technical Standards (RTS)

### RTS on SCA + Common Secure Communication
- Defines acceptable SCA factors.
- Defines exemptions: low-value, trusted beneficiary, TRA, corporate, recurring.
- Defines requirements for dedicated Open Banking interface.

### RTS on Fraud Reporting (PSD2)
- Standardised fraud data reporting from PSPs to NCAs.

### Other relevant
- RTS on cooperation + information exchange (PSD2).
- ITS on data submission.

---

## EPC Scheme Rulebooks

| Scheme | Notes |
|---|---|
| SCT (SEPA Credit Transfer) | Standard EUR credit transfer; ISO 20022 (pacs.008) |
| SDD Core (SEPA Direct Debit Core) | Consumer mandate-driven debit |
| SDD B2B | Business-to-business direct debit (different return rules) |
| SCT Inst | < 10s, EUR 100k cap raised by IPR |

EPC publishes annual rulebook releases; PSPs must implement on time.

---

## TARGET2 / T2 + TIPS

- **TARGET2 / T2** — Eurosystem RTGS (consolidated platform since March 2023; ISO 20022 native).
- **TIPS** — TARGET Instant Payment Settlement; Eurosystem real-time rail; pan-Eurozone.
- **T2S** — TARGET2-Securities (out of payments scope, but reuses settlement bus).

**Engine impact**:
- Direct or indirect participant connectivity.
- ISO 20022 native required.

---

## SCA — Strong Customer Authentication (EU)

Same conceptual structure as UK SCA:

| Factor | Examples |
|---|---|
| Inherence | Biometrics |
| Possession | Device-bound credential |
| Knowledge | PIN, password |

Exemptions per EBA RTS on SCA: low-value, trusted beneficiary, TRA, corporate, recurring.

---

## Sanctions Regimes (EU)

- **EU Consolidated List** — published by EC.
- **National implementations** by member states.
- **Dual screening** for EU + US + UK common practice on cross-border.

---

## Cross-Border Within EU vs. Outside

- Intra-EU EUR payments — SEPA-eligible; treated as domestic.
- Intra-EU non-EUR or non-SEPA — fall back to cross-border rules.
- Out-of-EU — full cross-border + Travel Rule + sanctions stack.

---

## Operational Resilience + DORA Specifics

| Requirement | Engine Impact |
|---|---|
| ICT risk management framework | Documented controls + reviews |
| Major ICT incident reporting | Tight reporting windows |
| TLPT (Threat-led Penetration Testing) | Red-team exercises for significant entities |
| Critical ICT third-party register | Vendor catalogue submission |
| Oversight of critical third parties | Direct EU oversight of major vendors |
| Information sharing | Voluntary intelligence sharing frameworks |

---

## What an EU Payment Engine Must Do — Checklist

| Capability | Driver |
|---|---|
| SEPA SCT + SDD Core + B2B adapter | EPC rulebooks |
| **SCT Inst on day one** + VoP | IPR (mandatory) |
| TIPS + EBA RT1 + STEP2 connectivity | EU CSM ecosystem |
| TARGET2 / T2 with ISO 20022 | Eurosystem |
| EBA RTS-aligned SCA enforcement + exemptions | PSD2 |
| Open Banking APIs (AISP / PISP / CBPII) | PSD2 |
| EU sanctions screening (Consolidated + national) | EU + member states |
| EU AML Rulebook compliance | AML Reg |
| GDPR data handling + DSR + 72h breach reporting | GDPR |
| DORA ICT risk + incident reporting + TLPT | DORA |
| Interchange caps applied | IFR |
| Fraud reporting standardised to NCA | EBA RTS |
| VASP / MiCA interface (if applicable) | MiCA |
| Multi-currency for non-EUR | SCT only covers EUR |

---

## Sources to Ingest

- PSD2 (Directive 2015/2366) + EBA RTS / ITS
- PSD3 + PSR proposals + tracked changes (state in flux)
- Instant Payments Regulation (EU 2024/886)
- EU AML Regulation + AMLD6 + AMLA founding regulation
- GDPR + EDPB guidance
- DORA (Reg. (EU) 2022/2554) + RTS / ITS
- MiCA (Reg. (EU) 2023/1114)
- Interchange Fee Regulation (Reg. (EU) 2015/751)
- EPC Rulebooks (SCT, SDD Core, SDD B2B, SCT Inst — annual)
- ECB TARGET2 / TIPS documentation
- EU Consolidated Sanctions List
- Per-NCA guidance (BaFin, AMF, CSSF, etc.)
- Internal: bank's IPR readiness assessment, DORA programme docs, EU sanctions playbook

---

## Open Questions

- [ ] Confirm IPR phase compliance state for the bank.
- [ ] Confirm DORA programme status (in-scope significant institution → TLPT roadmap).
- [ ] Confirm VoP (Verification of Payee) vendor or in-house build.
- [ ] Confirm EU AML Rulebook readiness and AMLA reporting line.
- [ ] Confirm PSD3 / PSR readiness as text stabilises.
