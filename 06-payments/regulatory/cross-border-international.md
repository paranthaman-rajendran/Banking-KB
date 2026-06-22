# Cross-Border International Payments — Regulatory Requirements

International / cross-border payment regulation is the **intersection of multiple jurisdictions** + global standards bodies. A payment engine processing a single MT103 / pacs.008 from `Bank A in Country X` to `Bank B in Country Y` must satisfy: sender-country rules, receiver-country rules, correspondent-bank-country rules, currency-country rules, sanctions regimes of every involved jurisdiction, and FATF-aligned Travel Rule data.

> Companion: per-jurisdiction deep-dives in this folder (USA, UK, Europe, Singapore, China, Japan).
> Engine-mapping: [engine-compliance-matrix.md](engine-compliance-matrix.md).

---

## Global Standards Bodies

| Body | Scope | What Engines Must Track |
|---|---|---|
| **FATF (Financial Action Task Force)** | AML / CFT recommendations; Travel Rule | 40 Recommendations + INRs; Recommendation 16 (Travel Rule) is most operational |
| **BIS CPMI** | Payment, clearing, settlement principles (PFMI); G20 cross-border roadmap | PFMI compliance for SIPS-designated systems; G20 2027 targets on cost / speed / transparency / access |
| **IOSCO** | Securities + co-publishes with CPMI on FMIs | Relevant where payment-vs-payment / DvP applies |
| **ISO** | ISO 20022 messaging; ISO 4217 currency; ISO 9362 BIC; ISO 13616 IBAN; ISO 17442 LEI | Mandatory message + identifier standards across CBPR+, SEPA, HVPS+ |
| **SWIFT (Cooperative)** | Network operator + standards profiles (CBPR+, HVPS+, gpi, MT) | Annual SWIFT SR; CBPR+ co-existence ends Nov 2025 for cross-border |
| **Wolfsberg Group** | Industry standard on correspondent banking due diligence | Wolfsberg Correspondent Banking Due Diligence Questionnaire (CBDDQ) |
| **G20 + FSB** | Cross-border payments roadmap targets | 2027 targets: 75% of payments < 1h; cost ≤ 1%; transparency mandatory |
| **OECD** | Tax-related: CRS (Common Reporting Standard) + FATCA convergence | Tax reporting on relevant flows |

---

## FATF Recommendation 16 — Travel Rule

**Mandatory** information that must accompany a cross-border transfer above the threshold (typically USD/EUR 1,000 — confirm per jurisdiction):

### Originator
- Name
- Account number (or unique transaction reference if no account)
- Address (or national ID, customer ID, date and place of birth)

### Beneficiary
- Name
- Account number (or unique transaction reference)

### Engine implication
The payment hub must:
1. Block / reject outbound cross-border payments missing required fields.
2. Hold inbound cross-border payments missing required fields for repair / inquiry.
3. Carry the information through the full message chain — no field stripping at intermediary hops.
4. Log Travel Rule completeness for every cross-border payment.

ISO 20022 fields:
- `Debtor` (name, postal address, organisation/private ID, country of residence)
- `DebtorAccount`
- `DebtorAgent` (BIC)
- `Creditor`, `CreditorAccount`, `CreditorAgent`
- `UltimateDebtor` / `UltimateCreditor` when applicable

SWIFT MT (legacy, sunsetting Nov 2025 for cross-border):
- Field 50K / 50A / 50F (Ordering Customer)
- Field 59 / 59A / 59F (Beneficiary)
- Field 70 (Remittance — but not for Travel Rule completeness)

---

## Sanctions Screening — Multi-Regime Reality

A cross-border payment must be screened against **every applicable regime**, not just the home country's:

| Regime | Operator | Applies When |
|---|---|---|
| OFAC SDN + sectoral | US Treasury | USD anywhere in the chain; US person / entity involved; US territory |
| EU Consolidated List | EU Commission | EU jurisdiction at any leg |
| HMT / OFSI | UK Treasury | GBP, UK-touching |
| UN Security Council | UN | Mandatory globally; member states implement |
| SECO (Switzerland) | Swiss government | CHF or CH-touching |
| MAS (Singapore) | MAS | SGD or SG-touching |
| AUSTRAC + DFAT (Australia) | DFAT autonomous + UNSC | AUD, AU-touching |
| FINTRAC / Global Affairs (Canada) | Canada | CAD, CA-touching |
| Country-specific (e.g., Iran, North Korea programs) | Per country | Per program |
| Bank-internal high-risk list | Bank-controlled | Always |

### Engine implication
- Pre-payment, real-time deterministic screening on all parties (debtor, creditor, intermediary agents) and free-text fields.
- USD-touching payments must screen even when neither end is US-domiciled — the USD nostro chain pulls them in.
- Hits go to investigator queue; 50001-class operational SLA for retail real-time rails.
- List freshness target: sub-hour from publication.
- Audit trail: every screening event logged with list version, hit decision, investigator.

---

## Correspondent Banking Due Diligence (Wolfsberg + FATF + Local)

Required for any correspondent relationship:

- **CBDDQ** (Wolfsberg Correspondent Banking Due Diligence Questionnaire) — industry-standard intake.
- **Enhanced Due Diligence (EDD)** when respondent is in higher-risk jurisdiction.
- Beneficial ownership identification on respondent.
- Periodic refresh (typically annually; sooner if risk profile changes).
- **Nested correspondent** — do you allow respondent's customers' customers to clear through you? Most banks prohibit beyond a clear known-respondent chain.

### Engine implication
- The hub must know the correspondent relationship for every BIC it routes through.
- It must be able to **reject payments routed through a non-approved correspondent**.
- It must apply differential controls (lower amount thresholds, tighter screening) for higher-risk corridor flows.

---

## Travel Rule for Crypto / VASP Sector (FATF 16 Extended)

FATF extended Recommendation 16 to Virtual Asset Service Providers (VASPs) in 2019. While most traditional payment engines don't process crypto, banks increasingly receive/send fiat that **interfaces with VASP flows** (on-/off-ramp).

- VASP-originated fiat in must carry equivalent Travel Rule data.
- Bank-side risk policies usually classify VASP-touching flows as higher risk.

### Engine implication
- Tag VASP-corridor payments distinctly for downstream AML monitoring.

---

## Tax-Driven Reporting

| Regime | Scope | What's Reported |
|---|---|---|
| **FATCA** (US) | US persons with foreign accounts | Account holders' US status; reportable accounts; annual to IRS |
| **CRS** (OECD) | Tax residency of account holders across CRS-signatory countries | Account holders + balances + flows; annual to local tax authority |
| **Section 871(m)** etc. | US withholding on certain financial flows | Withholding on dividends-equivalent payments |
| **Various per-country withholding regimes** | E.g., interest on cross-border deposits | As per local law |

### Engine implication
- The hub must capture tax-relevant data fields (account holder tax status) and route flows to the bank's tax reporting platform.

---

## Currency Controls

Some currencies are deliverable / non-deliverable:

| Currency Class | Engine Treatment |
|---|---|
| Fully convertible (USD, EUR, GBP, JPY, CHF, AUD, CAD, SGD) | Standard cross-border flow |
| Restricted (CNY/RMB, INR, RUB, KRW) | Onshore / offshore split; specific scheme constraints; documentation requirements |
| Sanctioned / programme-restricted | Blocked unless OFAC general licence applies (or equivalent) |

Examples:
- **CNY** — onshore (CNH offshore via Hong Kong / Singapore / London hubs) — see [china.md](china.md).
- **INR** — non-fully-convertible; LRS/FEMA constraints — see [../regulatory.md](../regulatory.md) India section.
- **RUB** — heavy sanctions controls.

### Engine implication
- Currency-specific routing tables.
- Onshore/offshore branch differentiation for restricted currencies.
- Block / hold logic for restricted programs.

---

## ISO 20022 — Mandatory for Cross-Border

| Operator | Cutover |
|---|---|
| SWIFT (CBPR+) | Co-existence ends **November 2025** — MX-only from then |
| FedWire | Migrated (2024 / 2025; verify current state) |
| CHAPS | ISO 20022 since 2023 |
| TARGET2 / T2 | ISO 20022 since March 2023 |
| CHIPS | ISO 20022 since 2024 |
| HK RTGS (CHATS) | ISO 20022 migration in progress (verify cutover) |
| Singapore MEPS+ | ISO 20022 migration in progress |
| Japan Zengin / BOJ-NET | ISO 20022 migration on programme |

### Engine implication
- ISO 20022-native message handling on the hub is no longer optional for cross-border.
- Field-richness implications: structured creditor / debtor must be propagated end-to-end.
- "Lossy translation" risk during MT→MX co-existence — engines must avoid lossy intermediate hops.

---

## G20 Cross-Border Roadmap Targets (2027)

The G20-mandated, FSB-coordinated programme has four headline targets:

| Target | 2027 Goal |
|---|---|
| **Cost** | ≤ 1% of payment value (retail global average); zero cost > 3% |
| **Speed** | 75% credited to end beneficiary within 1 hour; 100% within 1 business day |
| **Access** | All end-users have at least one option for sending and receiving cross-border |
| **Transparency** | Clear info on charges, FX, time |

This is driving:
- ISO 20022 standardisation
- Instant-rail cross-border linkages (UPI ↔ PayNow, FedNow ↔ scheme bridges, BIS Project Nexus)
- Pre-validation of beneficiary (CoP-style) becoming a cross-border expectation

### Engine implication
- Hubs must surface charge transparency.
- Hubs must integrate with cross-border instant linkages where available.
- Time-to-credit telemetry must be measurable end-to-end.

---

## Operational Compliance Topics

### gpi Tracker
SWIFT gpi provides a **UETR-keyed E2E tracker**. Adopting gpi (now mandatory for many SWIFT BICs) is the operational backbone for the transparency mandate.

### Confirmation of Payee (cross-border)
Emerging at corridor level (e.g., UK Pay.UK CoP for inbound). Engines must integrate when available.

### Pre-validation Services
SWIFT Payment Pre-validation (PPv): API-based beneficiary verification before the payment is sent. Reduces investigations.

### Beneficiary fraud + investigation
- camt.027 (Claim Non-Receipt) / camt.029 (Resolution of Investigation) / camt.087 (Request to Modify) over SWIFT.
- Bilateral comms for non-SWIFT rails.
- SLAs per scheme.

---

## What a Payment Engine Must Do — Cross-Border Checklist

| Capability | Reason |
|---|---|
| ISO 20022 native processing | CBPR+ Nov 2025 cutover; SEPA, FedNow, RTP, CHAPS, TARGET2 already there |
| MT ↔ MX translation (CBPR+ compliant) | Co-existence handling for any non-migrated counterparties |
| Travel Rule field validation (block missing) | FATF Rec 16 enforcement |
| Multi-regime sanctions screening | OFAC + EU + HMT + UN + local |
| Correspondent BIC governance | Wolfsberg CBDDQ-driven routing tables |
| Currency-specific routing (CNH onshore/offshore, INR, etc.) | Restricted-currency compliance |
| UETR generation + propagation | gpi + audit trail |
| gpi tracker integration | Transparency target |
| Charge transparency disclosure | G20 + customer-protection rules |
| Pre-validation API support (where available) | STP improvement |
| Audit trail of every screening + transformation event | Reg requirement universal |
| Field-loss prevention at intermediary hops | Travel Rule + customer-protection |
| Tax data capture for reporting | FATCA / CRS |
| Quarantine + investigation workflow | camt.027 / 029 / 087 + manual repair |

---

## Sources to Ingest

- FATF 40 Recommendations + INRs (especially R.10, R.11, R.16, R.20)
- FATF Guidance on Risk-Based Approach + Wire Transfers
- BIS CPMI publications including PFMI and Cross-Border Payments programme outputs
- G20 Cross-Border Payments Roadmap + FSB progress reports
- Wolfsberg CBDDQ + Wolfsberg Trade Finance Principles
- SWIFT CBPR+ Usage Guidelines (annual)
- SWIFT gpi rulebook
- OECD CRS implementation handbook
- US Treasury IRS FATCA guidance
- ISO 20022 Message Definition Reports

---

## Open Questions

- [ ] Confirm the bank's correspondent banking risk policy and CBDDQ refresh cadence.
- [ ] Confirm currency policy on restricted currencies (especially CNY onshore / offshore arrangements).
- [ ] Confirm gpi tracker subscription state and UETR enforcement at all entry points.
- [ ] Confirm CBPR+ Nov 2025 readiness for the bank's BICs.
- [ ] Confirm SWIFT Payment Pre-validation adoption.
