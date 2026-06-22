# Cross-Border Payment Rails

Cross-border payments are dominated by **SWIFT** (correspondent banking model) with growing share for **alt rails** (SEPA Inst, FedNow corridor pilots, RippleNet, networked instant rails via NPCI/Pix MoUs).

> Sub-domain: `CrossBorder`
> Default sensitivity: `Confidential` (transaction data); `Internal` (scheme rulebooks)

---

## Rail Comparison

| Rail | Geography | Model | Settlement | Typical Speed | Standard |
|---|---|---|---|---|---|
| SWIFT (correspondent) | Global | Message-only (banks settle bilaterally via nostro/vostro) | T+0 to T+2 (FX + correspondent chain) | Minutes to days | SWIFT MT → ISO 20022 MX |
| SWIFT gpi | Global | Tracker-enhanced SWIFT | Same as SWIFT, with E2E tracking | Faster gpi banks: minutes | SWIFT MT/MX |
| SEPA Credit Transfer (CT) | EU + EEA + UK | Pan-European credit transfer | Same day | < 1 business day | ISO 20022 (pacs.008) |
| SEPA Inst (SCT Inst) | EU + EEA | Instant pan-European | Real-time | < 10s | ISO 20022 (pacs.008) |
| ACH (NACHA) | US domestic + some Intl | Batched ACH | Same-day ACH or next-day | Hours to next day | NACHA ACH format |
| FedWire | US | RTGS | Real-time gross | Minutes | ISO 20022 (FedWire ISO migration in progress) |
| CHIPS | US | Netted, high-value | EOD net + intraday optimization | Intraday | ISO 20022 (since 2024) |
| RippleNet | Selective corridors | Pre-funded / xRapid | Near real-time | Seconds | Proprietary |
| Card-on-Rails (Visa Direct, Mastercard Send) | Global | Push-to-card via card scheme | Real-time message; settlement via card scheme | Minutes | ISO 8583 + scheme APIs |
| BIS Project Nexus / mBridge | Pilot | Multilateral instant linkages | Real-time | Seconds (pilot) | ISO 20022 |

---

## SWIFT — Correspondent Banking Model

**Operator**: SWIFT (a Belgian cooperative; messaging only, NOT a settlement system)

```
Ordering Customer
    → Sender Bank
    → (Intermediary Bank(s) via correspondent network)
    → Beneficiary Bank
    → Beneficiary Customer
```

Each hop carries an FX leg, charges, and time. SWIFT gpi (Global Payments Innovation) adds a UETR (unique end-to-end transaction reference) and an E2E tracker, with member-bank SLAs.

### Message Types (legacy MT — sunsetting Nov 2025 for cross-border payments)

| MT | Purpose |
|---|---|
| MT103 | Single customer credit transfer |
| MT103 STP | Straight-through processing variant |
| MT202 | General financial institution transfer |
| MT202COV | Cover payment for an underlying MT103 |
| MT199 / MT299 | Free-format text messages |
| MT900 / MT910 | Debit / credit confirmation |
| MT940 / MT942 / MT950 | Statement messages (EOD / interim / cash mgmt) |

### ISO 20022 successors (MX)

| MX | Purpose | MT equivalent |
|---|---|---|
| `pacs.008` | Customer credit transfer | MT103 |
| `pacs.009` | FI-to-FI credit transfer | MT202 |
| `pacs.009.cov` | Cover payment | MT202COV |
| `camt.054` | Debit / credit notification | MT900/910 |
| `camt.053` | Bank-to-customer statement | MT940 |
| `camt.052` | Bank-to-customer report | MT942 |

**SWIFT CBPR+ migration**: in-flight co-existence ends November 2025. From that point, cross-border payments are MX-only over SWIFT FINplus. Domestic high-value (e.g., TARGET2, FedWire) on their own schedules.

---

## SEPA

Single Euro Payments Area — 36 countries (EU + EEA + UK + others).
Operator scheme: EPC (European Payments Council); processed by CSMs (Clearing & Settlement Mechanisms) like STEP2, EBA Clearing, RT1, TIPS.

### Schemes
- **SEPA CT** — credit transfer, max EUR 999,999,999.99, < 1 business day
- **SEPA DD** — direct debit (Core + B2B variants)
- **SCT Inst** — instant credit transfer, < 10s, < EUR 100,000 (limit raised periodically; check EPC for current)
- **OCT Inst** (proposed) — one-leg-out instant cross-border for EUR

EU Instant Payments Regulation (IPR) — November 2024 came into force. Requires every PSP in EU/EEA offering CT to also offer SCT Inst, with no premium on price.

---

## US — ACH, FedWire, FedNow, CHIPS

### ACH (NACHA)
- Operator: Federal Reserve + The Clearing House (EPN)
- Batched; standard ACH (1–2 days) and Same-Day ACH (intraday windows)
- Format: NACHA file format (legacy)

### FedWire Funds Service
- Operator: Federal Reserve
- RTGS, real-time gross, finality
- High value, time-critical
- ISO 20022 migration completed for FedWire in 2025 (verify current state)

### FedNow
- Operator: Federal Reserve
- Real-time, 24x7x365, instant credit transfer
- Live since July 2023
- ISO 20022 (pacs.008/009) native

### CHIPS
- Operator: The Clearing House
- Netted, high-value
- ISO 20022 migrated 2024

---

## Compliance Overlay for Cross-Border

Every cross-border payment runs through compliance gates:
- **Sanctions screening** — OFAC (US), EU Consolidated List, HMT (UK), UN, plus bank's internal list
- **AML transaction monitoring** — pattern detection per FATF Recommendations
- **CTF / dual-use screening** for trade-finance-linked payments
- **Travel Rule** — originator + beneficiary information completeness (FATF Rec 16; enforced via SWIFT field requirements)
- **Country-risk policy** — bank's internal high-risk corridor list
- **PEP screening** — politically exposed person checks
- **Tax reporting** — FATCA/CRS for relevant flows

Sanctions hits go to investigators in real time; the payment is held until cleared.

---

## Cost & Pricing

Cross-border payments still carry meaningful cost vs. domestic:
- Interchange / scheme fees + FX spread + correspondent lifting fees
- BIS / G20 roadmap targets: ≤ 1% cost, < 1h speed, transparency by 2027

This drives interest in instant rail linkages (UPI↔PayNow, UPI↔Pix MoUs) as alternatives to correspondent SWIFT.

---

## Sources to Ingest

- SWIFT Standards MT Reference Manual (per release year)
- SWIFT CBPR+ Translation Rules + Usage Guidelines
- EPC SEPA Rulebooks (CT, DD, Inst)
- NACHA Operating Rules and Guidelines
- Federal Reserve Operating Circulars (5, 6, 8)
- BIS CPMI / IOSCO PFMI publications
- FATF Recommendations (especially 16 — Travel Rule)
- Bank-internal: nostro/vostro reconciliation SOPs, correspondent agreement KYC files, sanctions playbook

---

## Open Questions

- [ ] Confirm SWIFT MX migration status across all critical corridors as of cutover.
- [ ] FedWire ISO 20022 — confirm migration completion date.
- [ ] Internal stance on RippleNet / xRapid usage.
- [ ] UPI international corridors live (SG, FR, UAE, etc.) — current list and reciprocity model.
