# USA Payments — Regulatory Requirements

US payments regulation is **layered**: federal-level (Fed, OCC, FDIC, CFPB, FinCEN, OFAC), **scheme-level** (NACHA, TCH), and **state-level** (money transmitter licensing). A payment engine for the US must comply with all three layers.

> Companion rail file: [../rails/domestic-usa.md](../rails/domestic-usa.md)

---

## Authorities

| Authority | Scope | Engine Impact |
|---|---|---|
| **Federal Reserve** | Operates FedWire, FedNow, FedACH, Check Services; issues Regs E, J, CC, II; supervises member banks | Operating circulars + Reg compliance built into rail adapters |
| **OCC** | Supervises national banks | Operational risk + third-party risk supervision affecting vendor management |
| **FDIC** | Supervises state non-member banks; deposit insurance | Deposit account servicing requirements |
| **CFPB** | Consumer financial protection | Reg E disclosures + error resolution; APP fraud reimbursement evolution |
| **FinCEN** | BSA / AML enforcement | SAR / CTR filings; Travel Rule; beneficial ownership |
| **OFAC** | Sanctions screening | Real-time list ingestion + screening; OFAC reporting |
| **NACHA** | ACH rulebook | Annual rule updates the ACH engine must track |
| **The Clearing House (TCH)** | RTP + CHIPS rulebooks | Per-scheme adapter compliance |
| **State Banking Regulators** | Money Transmitter Licensing (MTL); state-level UDAP | License footprint per state of operation |
| **NMLS** | National Mortgage Licensing System (also used for MSB / MTL registration) | Registration tracking |
| **CFTC + SEC** | Limited payments scope, but for cross-asset / derivatives-adjacent payments | Tax + reporting overlap |
| **NCUA** | Federal credit union supervisor | Where bank serves CU sector |

---

## Core Regulations

### Regulation E (12 CFR 1005)
Consumer protection for electronic fund transfers.

- Unauthorized EFT — consumer liability capped (USD 50 / 500 / unlimited tiered by notification timing).
- Error resolution: 10 business days standard, extension to 45 days if provisional credit issued.
- Disclosures: initial, change-in-terms, periodic statements.
- Pre-authorized EFT (recurring debit) — mandate documentation + revocation.

**Engine impact**:
- Engine + downstream channels must produce required disclosures.
- Error reporting flow + provisional credit logic.
- Mandate storage + revocation handling.

### Regulation J (12 CFR 210)
Governs FedWire Funds Service and FedACH.

- Subpart A: FedWire — finality at receipt by Fed; sender bank guarantees the wire.
- Subpart B: FedACH operating terms.

**Engine impact**:
- FedWire adapter must honour finality (no reversal logic — only recall by mutual agreement).
- FedACH adapter terms baked in.

### Regulation CC (12 CFR 229)
Funds availability + Check 21.

- Funds-availability schedules; next-business-day for most deposits.
- Check 21 + Image Replacement Documents (IRDs).
- Exception holds + customer notice.

**Engine impact**:
- Posting engine must enforce availability holds.
- Check imaging path + IRD generation.

### Regulation II (12 CFR 235) — Durbin Amendment
Debit interchange + routing.

- Cap on debit interchange for FIs > USD 10B in assets.
- At-least-two-unaffiliated-network routing requirement — extended by CFPB to card-not-present in recent clarifications.

**Engine impact**:
- Card issuer-side: dual-network capability per debit BIN.
- Merchant / acquirer side: routing logic for unaffiliated network choice.

### Bank Secrecy Act (BSA)
Foundation of US AML / CFT regulation.

- Currency Transaction Report (CTR) — USD 10,000 cash transactions.
- Suspicious Activity Report (SAR) — pattern-based.
- Travel Rule (US implementation) — USD 3,000 threshold for wire originator + beneficiary info.
- Customer Identification Program (CIP) requirements.
- Beneficial ownership identification (Corporate Transparency Act — implementation evolving).

**Engine impact**:
- CTR + SAR detection: AML + transaction monitoring layer.
- Travel Rule field enforcement on cross-border wires.
- BO data capture + retention.

### FinCEN Travel Rule (US implementation of FATF R.16)
- Threshold: USD 3,000 (lower than international USD/EUR 1,000 baseline; US has independent rule).
- Required fields: originator name, address, account number, beneficiary name, account number.
- Applies to fund transfers including FedWire, CHIPS, ACH IAT, SWIFT cross-border.

**Engine impact**:
- Field validation block / hold for missing data on outbound + flagged repair for inbound.

### OFAC Sanctions
Real-time enforcement.

- SDN (Specially Designated Nationals) list + sectoral programs (Russia, Iran, North Korea, Venezuela, etc.).
- 50% Rule — entities owned ≥ 50% by SDN are themselves blocked (cumulatively).
- Secondary sanctions reach — non-US persons can be sanctioned for dealings with SDN.
- OFAC Recordkeeping — 5-year minimum.

**Engine impact**:
- Pre-payment deterministic screening on all parties + free-text + scheme IDs.
- Hits go to investigator with strict timeline.
- Blocked-property reporting + rejected transaction reporting.

### Consumer Financial Protection Act + UDAAP
- "Unfair, Deceptive, Abusive Acts or Practices" — broad enforcement lever.
- CFPB Circulars on APP fraud at scale (Zelle pressure, 2023+).

**Engine impact**:
- Disclosures aligned with UDAAP defensibility.
- Fraud reimbursement policy explicit.

---

## Scheme Rulebooks

### NACHA Operating Rules
- Annual cycle (March release typical).
- Rules on SEC codes, return windows, ODFI / RDFI obligations, Third-Party Sender, Account Validation Rule.
- Non-compliance triggers per-violation fines + reputational risk.

**Engine impact**:
- ACH engine must implement current SEC code semantics + return rules.
- Annual upgrade discipline.

### TCH RTP Operating Rules
- Real-time payments scheme rulebook.
- USD 10M per-txn cap (raised Feb 2025).
- Mandatory ISO 20022; specific cancellation rules.

### TCH CHIPS Rules
- Netted high-value scheme rules.
- ISO 20022 since 2024.
- Prefunding obligations.

### FedNow Service Operating Procedures
- Federal Reserve OC 8 + Service Description.
- 24x7x365 instant; USD 500k default cap.
- RfP supported; cancellation rules defined.

---

## State Money Transmitter Licensing (MTL)

US-unique layer: most non-bank PSPs need state-by-state money transmitter licenses (sometimes 49-state coverage).

- **Surety bond** per state.
- **Net worth requirements** per state.
- **Permissible investments** + segregation of customer funds.
- **State examinations** + reporting.
- **NMLS-coordinated** licensing.
- **MSB registration** with FinCEN federally + state MTLs.

**Engine impact**:
- Bank-as-a-Service / sponsor-bank arrangements typically wrap fintech under the bank's charter to avoid MTL stack — engine routing + customer-of-customer accounting needs separation.
- State-level disclosures may be required at customer journey.

---

## Data + Cybersecurity Requirements

| Regime | Scope |
|---|---|
| **Gramm-Leach-Bliley Act (GLBA)** | Customer financial information privacy + safeguards |
| **NYDFS Part 500** | NY State cybersecurity rules for financial institutions |
| **State privacy laws** (CCPA, CPRA, etc.) | State-level consumer privacy rights |
| **FFIEC IT Examination Handbook** | Federal-level cyber / IT supervisory guidance |
| **CISA + NIST CSF** | Recommended frameworks; some sector regulators mandate |

**Engine impact**:
- Encryption at rest + in transit baseline.
- Access logging + audit per FFIEC guidance.
- Customer data exfil monitoring.

---

## CFPB Section 1033 — Personal Financial Data Rights
Open Banking-style regulation in the US.

- Issued Oct 2024.
- Consumer right to access + share their financial data.
- Phased implementation.

**Engine impact**:
- Data access APIs.
- Consent + revocation flows.
- Data exit / portability.

---

## CFPB on APP Fraud (Zelle / Wire Fraud)
- 2023+ active CFPB pressure on big banks for APP / wire fraud reimbursement.
- Not yet a UK PSR-style mandatory split; voluntary EWS / bank-level reimbursement expansion in process.

---

## What a US Payment Engine Must Do — Checklist

| Capability | Driver |
|---|---|
| FedACH + EPN connectivity with full SEC code library | NACHA + Reg J |
| Same-Day ACH 3-window scheduling | NACHA |
| Account Validation for WEB debits | NACHA |
| ODFI return monitoring + threshold alerting | NACHA |
| FedWire with Reg J finality semantics | Reg J |
| ISO 20022 native for FedWire / FedNow / RTP / CHIPS | Operator mandates |
| FedNow + RTP dual connectivity (and routing logic) | Coverage |
| OFAC real-time screening (SDN + sectoral + 50%) | OFAC |
| Travel Rule USD 3,000 enforcement | FinCEN |
| BSA SAR / CTR detection | FinCEN |
| Reg E error resolution + provisional credit | Reg E |
| Reg CC availability hold logic | Reg CC |
| Reg II dual-network debit routing | Reg II |
| State MTL respect (for fintech sponsor-bank arrangements) | State law |
| Audit trail per FFIEC + immutable retention | FFIEC + BSA |
| Section 1033 data access APIs (roadmap) | CFPB |

---

## Sources to Ingest

- 12 CFR Parts 1005 (Reg E), 210 (Reg J), 229 (Reg CC), 235 (Reg II)
- Federal Reserve Operating Circulars 5, 6, 8
- FedNow Service Description + Operating Circular 8
- NACHA Operating Rules + Guidelines (annual)
- TCH RTP Operating Rules + CHIPS Rules
- FinCEN regulations + BSA examination manual
- OFAC SDN + sectoral lists (real-time)
- CFPB Bulletins + Circulars
- CFPB Section 1033 final rule + amendments
- State MTL statutes + NMLS guidance
- NYDFS Part 500
- FFIEC IT Examination Handbook
- Internal: bank's BSA compliance manual, OFAC playbook, state MTL footprint

---

## Open Questions

- [ ] Confirm bank's federal supervisor (Fed / OCC / FDIC) and state footprint.
- [ ] Confirm sponsor-bank arrangements for fintech partners (drives MTL exposure).
- [ ] Confirm Section 1033 readiness roadmap.
- [ ] Confirm BSA / AML compliance officer reporting to engine team.
- [ ] Confirm CFPB APP fraud reimbursement policy and operational state.
