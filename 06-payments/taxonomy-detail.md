# Payments — Taxonomy Detail

Deeper breakdown of the `Payments` domain. Used to drive `sub_domain` and `product_class` metadata values during ingestion.

> Parent: [../01-taxonomy/taxonomy.md](../01-taxonomy/taxonomy.md)

---

## Sub-Domain Codes

| Code | Display Name | Geography Default |
|---|---|---|
| `DomesticIN` | Domestic Payments — India | IN |
| `DomesticEU` | Domestic Payments — EU (incl. SEPA Inst) | EU |
| `DomesticUS` | Domestic Payments — US (ACH, FedWire, FedNow, RTP, CHIPS) | US |
| `DomesticUK` | Domestic Payments — UK (FPS, CHAPS, Bacs, ICS) | UK |
| `CrossBorder` | Cross-Border Payments | GLOBAL |
| `RealTimeRails` | Real-Time / Instant Payment Rails | GLOBAL |
| `Cards` | Card Payments & Networks | GLOBAL |
| `WalletsBNPL` | Wallets, BNPL, Embedded Finance | GLOBAL |
| `Reconciliation` | Reconciliation & Settlement Ops | GLOBAL |

---

## Product Classes (free-tag `product_class`)

### Domestic India (`DomesticIN`)
- `NEFT` — National Electronic Funds Transfer (deferred net, 24x7 since 2019)
- `RTGS` — Real-Time Gross Settlement (high value, 24x7 since 2020)
- `IMPS` — Immediate Payment Service (24x7, mobile-first)
- `UPI` — Unified Payments Interface (real-time, mobile-first, dominant rail)
- `UPILite` — Offline-capable UPI for small-value payments
- `AePS` — Aadhaar-enabled Payment System (rural, BC-led)
- `NACH` — National Automated Clearing House (mandates, recurring)
- `BBPS` — Bharat Bill Payment System

### Domestic USA (`DomesticUS`)
- `ACH_Standard` — NACHA-rules batched ACH (T+1 / T+2)
- `ACH_SameDay` — Same-Day ACH (3 windows, USD 1M cap)
- `ACH_IAT` — International ACH Transaction (cross-border ACH with Travel Rule fields)
- `FedWire` — Federal Reserve RTGS (high value, final, irrevocable)
- `FedNow` — Federal Reserve instant rail (24x7, live July 2023)
- `RTP_TCH` — The Clearing House Real-Time Payments (instant, USD 10M cap)
- `CHIPS` — TCH netted high-value (USD correspondent dominant)
- `Check21_IRD` — Image Replacement Document under Check 21
- `Zelle` — EWS-operated overlay (settles via RTP/FedNow/ACH)
- `PINDebit_STAR_NYCE_etc` — PIN debit networks (Reg II routing)

### Domestic UK (`DomesticUK`)
- `FPS` — Faster Payments Service (Pay.UK, 24x7, GBP 1M cap)
- `CHAPS` — BoE RTGS (final, irrevocable, high value)
- `Bacs_DC` — Bacs Direct Credit (3-day cycle, payroll / supplier)
- `Bacs_DD` — Bacs Direct Debit (mandates, Direct Debit Guarantee)
- `ICS` — Image Clearing System (cheque images)
- `LINK` — UK ATM network
- `CoP` — Confirmation of Payee (central Pay.UK service)
- `VRP_Sweeping` — Sweeping Variable Recurring Payments (Open Banking, CMA9 mandate)
- `VRP_Commercial` — Commercial Variable Recurring Payments
- `Open_Banking_PISP` — PSD2-derived Payment Initiation Services

### Cross-Border (`CrossBorder`)
- `SWIFT_MT103` — Single customer credit transfer
- `SWIFT_MT202` — General financial institution transfer
- `SWIFT_MT202COV` — Cover payment for MT103
- `SWIFT_MT199` — Free format
- `SWIFT_MT940/MT950` — Statement messages
- `SWIFT_MX` — ISO 20022 successors (pacs.008, pacs.009, etc.)
- `SEPA_CT` — SEPA Credit Transfer
- `SEPA_DD` — SEPA Direct Debit
- `SEPA_INST` — SEPA Instant Credit Transfer
- `ACH_CCD/PPD/WEB` — NACHA ACH variants
- `FedWire` — US large-value RTGS
- `CHIPS` — Clearing House Interbank Payments System
- `RippleNet` — Alt rail (limited adoption)

### Real-Time Rails (`RealTimeRails`)
- `UPI` (IN)
- `FPS` — Faster Payments Service (UK)
- `TIPS` — TARGET Instant Payment Settlement (EU)
- `SCT_Inst` — SEPA Credit Transfer Instant (EU)
- `FedNow` (US, live since 2023)
- `Pix` (BR)
- `NPP` — New Payments Platform (AU)
- `PayNow` (SG)
- `PromptPay` (TH)

### Cards (`Cards`)
- `Visa`, `Mastercard`, `Amex`, `RuPay`, `Diners`, `JCB`, `UnionPay`
- `Tokenization` — network tokens, device tokens
- `3DS_v2` — 3-D Secure 2.x authentication
- `EMV_Contact`, `EMV_Contactless`, `EMV_QR`

---

## Message Standards Cross-Reference

| Standard | Used By | Status |
|---|---|---|
| ISO 20022 | SWIFT MX, SEPA, FedNow, TIPS, UPI internal | Migration ongoing — SWIFT CBPR+ co-existence ends Nov 2025 |
| SWIFT MT | Legacy SWIFT (MT103, MT202, MT940, etc.) | Sunset for cross-border payments Nov 2025 |
| ISO 8583 | Card schemes (Visa, Mastercard, RuPay) | Active, long-tail |
| NACHA Operating Rules | US ACH | Active, annual updates |
| EPC Rulebooks | SEPA CT/DD/Inst | Active, periodic updates |

See [standards/](standards/) for per-standard detail.

---

## Settlement Models

| Model | Examples | Implication |
|---|---|---|
| RTGS (Real-Time Gross) | RTGS (IN), FedWire (US), TARGET2 (EU) | Final, irrevocable, high value |
| DNS (Deferred Net Settlement) | NEFT (IN), legacy ACH (US) | Batched, lower liquidity demand |
| Instant / 24x7 | UPI, FedNow, FPS, SCT Inst | Real-time, retail-focused, dispute model differs |
| Card networks (interchange-based) | Visa, Mastercard | Authorization → clearing → settlement, T+1 or longer |

---

## Open Questions for Knowledge Sign-off

- [ ] Confirm whether `DomesticEU` and `DomesticUS` should be sub-domains or sit under `CrossBorder` for non-EU/US banks.
- [ ] Is `Reconciliation` a sub-domain of Payments or of Operations? Today it sits in both.
- [ ] Cards — sub-domain of Payments or its own domain? (Volume justifies separation.)
- [ ] Wallets/BNPL — keep in Payments or split to a `EmbeddedFinance` domain?
