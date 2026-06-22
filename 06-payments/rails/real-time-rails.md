# Real-Time / Instant Payment Rails

Domestic instant rails have proliferated since UPI's 2016 launch. Most are ISO 20022 native, 24x7x365, sub-10s P95, and increasingly linked cross-border via bilateral or multilateral arrangements.

> Sub-domain: `RealTimeRails`

---

## Country Coverage (Production)

| Country | Rail | Operator | Live Since | ISO 20022 | Cap (Retail) |
|---|---|---|---|---|---|
| India | UPI | NPCI | 2016 | Internal | INR 1L standard (higher for specific use cases) |
| India | IMPS | NPCI | 2010 | No | INR 5L |
| UK | Faster Payments (FPS) | Pay.UK | 2008 (ISO 20022 from NPA) | Yes (NPA-in-progress) | GBP 1M (varies by scheme) |
| EU | SCT Inst | EPC / EBA CLEARING (RT1), Eurosystem (TIPS) | 2017 | Yes (pacs.008) | EUR 100,000 (raised) |
| EU | TIPS | Eurosystem | 2018 | Yes | Per SCT Inst |
| US | FedNow | Federal Reserve | Jul 2023 | Yes | USD 500,000 max per txn (configurable) |
| US | RTP (TCH) | The Clearing House | 2017 | Yes | USD 1M (raised from 100k) |
| Brazil | Pix | Banco Central do Brasil | Nov 2020 | Yes (subset) | None (operator + user defined) |
| Australia | NPP / PayTo | NPP Australia | 2018 | Yes | None standard cap |
| Singapore | PayNow / FAST | ABS / MAS | 2017 | Yes (FAST in-flight) | Bank-set |
| Thailand | PromptPay | NITMX / BoT | 2017 | Yes | Bank-set |
| Indonesia | BI-FAST | Bank Indonesia | 2021 | Yes | IDR 250M |
| Japan | Zengin / Zengin More | Japanese Bankers Assoc | 2018 (24x7) | ISO 20022 migration in progress | JPY 1 oku for some |
| Saudi Arabia | Sarie | SAMA | 2021 | Yes | None standard |

Verify caps and limits against the operator's latest circular before quoting.

---

## Cross-Border Instant Linkages

Bilateral and multilateral linkages allowing two instant rails to settle cross-border in near real-time:

| Corridor | Status |
|---|---|
| UPI ↔ PayNow (IN ↔ SG) | Live (Feb 2023) |
| UPI ↔ FedNow (IN ↔ US) | Discussion / MoU (verify status) |
| UPI ↔ Pix (IN ↔ BR) | MoU (verify production status) |
| UPI ↔ UAE IPP (IN ↔ AE) | Live for selected use cases |
| UPI ↔ France (selected merchant acceptance) | Live |
| BIS Project Nexus | Multi-country IPS hub — IN, MY, PH, SG, TH; production target TBD |
| BIS Project mBridge | Wholesale CBDC-linked cross-border (CN, HK, TH, AE) |

These corridors typically operate on:
1. Pre-funded nostro on each rail.
2. ISO 20022 message conversion at the corridor switch.
3. Per-corridor FX rate setting + transparency.

---

## Common Operational Patterns

### Address-based resolution
- UPI VPA (`name@bank`)
- Pix Keys (CPF, email, phone, random UUID)
- PayNow (mobile, NRIC, UEN)
- FedNow uses standard FI routing (no alias)

### Push & Pull
- All instant rails support push (credit transfer).
- Pull (mandate / autopay / VRP) is supported by some — UPI AutoPay, Pix Automático (in rollout), PayTo (AU), VRP (UK).

### Refund & Dispute
Instant ≠ irrevocable. Most rails define:
- Reversal request windows (e.g., UPI: dispute via DMS within defined SLA)
- Exception handling for failed credits (auto-reversal expected within minutes)
- Fraud chargeback paths — varies by rail; weaker than card schemes

### Authentication
- UPI: device binding + UPI PIN
- Pix: bank app + biometric
- FedNow: PSP-defined; usually multi-factor
- SCT Inst: bank-level; PSD2 SCA applies

---

## Why Instant Is Different (for the KB)

| Dimension | Non-instant | Instant |
|---|---|---|
| Dispute window | Days/weeks | Seconds to hours |
| Fraud blast radius | Bounded by settlement window | Funds moved immediately, hard to claw back |
| Customer expectation | "Will arrive eventually" | "It's there now" |
| Reconciliation | Batched, EOD | Real-time, continuous |
| Sanctions screening latency | Pre-settlement | Pre-authorization, sub-second |

Implication: a Payments KB serving Operations needs **runbook chunks indexed for sub-second retrieval**, not 3-second LLM-mediated answers. See [../README.md#payments-vs-capital-markets](../README.md) for governance implications.

---

## Sources to Ingest

- NPCI UPI Operating Circulars + Procedural Guidelines
- EPC SCT Inst Rulebook
- Pay.UK FPS / NPA documentation
- Federal Reserve FedNow Operating Circular 8 + Service Description
- Banco Central do Brasil — Pix regulations and Pix Foco circulars
- BIS Project Nexus and mBridge published papers
- Internal: instant payments incident postmortems, fraud playbooks

---

## Open Questions

- [ ] Confirm current state of UPI cross-border corridors (this changes fast).
- [ ] Internal incident threshold definitions for "instant rail outage" (e.g., NPCI degraded vs. down).
- [ ] Mapping of internal alert taxonomy to operator-published incident codes.
