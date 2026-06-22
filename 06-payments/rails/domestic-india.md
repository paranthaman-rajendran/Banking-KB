# Domestic India Payment Rails

Authoritative reference: **RBI Master Directions on Payment Systems** + **NPCI Operating Circulars**. The content below is a working summary; canonical answers must cite the underlying circular.

> Sub-domain: `DomesticIN`
> Owner: Payments Product + Operations
> Default sensitivity: `Internal` (rulebooks are non-public; transaction data is `Confidential`)

---

## At-a-Glance Comparison

| Rail | Operator | Settlement | Window | Max Value (Retail) | Typical Use |
|---|---|---|---|---|---|
| NEFT | RBI | Deferred net (half-hourly batches) | 24x7 (since Dec 2019) | No upper limit (per-bank cap) | Retail credit transfers |
| RTGS | RBI | Real-time gross | 24x7 (since Dec 2020) | INR 2 lakh minimum (no upper limit) | High-value, time-critical |
| IMPS | NPCI | Real-time, deferred settlement | 24x7 | INR 5 lakh per txn | Retail, P2P, mobile |
| UPI | NPCI | Real-time via IMPS rails | 24x7 | INR 1 lakh (standard), up to INR 5 lakh for specific use cases | P2P, P2M, merchant |
| AePS | NPCI | Real-time | 24x7 | INR 10,000 per txn | Rural / BC-led withdrawal |
| NACH | NPCI | Batched | Business days | Per-mandate | Recurring, mandates |

Limits change frequently. Always cite the latest NPCI circular.

---

## NEFT — National Electronic Funds Transfer

**Operator**: Reserve Bank of India (RBI)
**Model**: Deferred Net Settlement, half-hourly settlement batches
**Window**: 24x7x365 since 16 December 2019
**Messages**: Internal RBI format (not SWIFT; will migrate to ISO 20022 per RBI roadmap)

Key points:
- Per-transaction value is unrestricted at the system level; individual banks set internal limits.
- Beneficiary credit by next batch; failure-return is mandatory within 2 hours of the next settlement.
- Charges: zero for online retail since 2020 (RBI directive).

---

## RTGS — Real-Time Gross Settlement

**Operator**: RBI
**Model**: Real-Time Gross Settlement (final, irrevocable per transaction)
**Window**: 24x7x365 since 14 December 2020
**Minimum value**: INR 2,00,000 (retail-facing)

Key points:
- Final settlement on RBI's books; no clearing risk between sender and receiver.
- ISO 20022-based RTGS in production since 2021 (one of the earlier RBI migrations).
- Used for high-value corporate, treasury, and inter-bank settlement.

---

## IMPS — Immediate Payment Service

**Operator**: NPCI
**Model**: Real-time message → real-time fund movement → deferred inter-bank settlement
**Window**: 24x7x365
**Channels**: Mobile (MMID + Mobile #), IFSC + Account, Aadhaar

Key points:
- Successor to NEFT for retail real-time use; underlies UPI's settlement.
- Per-txn limit currently INR 5 lakh.
- Each member bank settles through NPCI's net position on a deferred basis.

---

## UPI — Unified Payments Interface

**Operator**: NPCI
**Model**: Real-time API overlay on IMPS rails; final settlement via NPCI net positions to RBI
**Window**: 24x7x365
**Key entities**: PSPs (Payment Service Providers), TPAPs (Third-Party App Providers), Banks, NPCI

### UPI architecture (simplified)

```
Payer App (TPAP)
    → Payer PSP Bank
    → NPCI UPI Switch
    → Payee PSP Bank
    → Payee App / Account
```

### Variants
- **UPI 123Pay** — feature-phone, IVR-based
- **UPI Lite** — offline, small-value (< INR 500)
- **UPI Lite X** — NFC-based offline
- **UPI International** — cross-border merchant acceptance (NPCI rollouts to SG, FR, etc.)
- **AutoPay (e-mandate)** — recurring debits, RBI's recurring transactions framework

### Key Policy Anchors
- NPCI's UPI Procedural Guidelines + Operating Circulars
- RBI's Master Direction on Prepaid Payment Instruments (where wallets interact)
- RBI's regulations on PA/PG (Payment Aggregators / Gateways)
- 30% volume cap on individual TPAPs (deferred enforcement — confirm current status before quoting)

---

## AePS — Aadhaar-enabled Payment System

- Withdrawal, balance enquiry, mini-statement via BC (Business Correspondent) using Aadhaar + biometric.
- High in rural reach, scrutinized for fraud — RBI tightened limits and reconciliation requirements.

---

## NACH — National Automated Clearing House

- Batched credit (e.g., dividend, salary disbursement) and debit (recurring mandates: SIP, EMI, utility).
- Successor to ECS.
- Mandate registration via paper or e-NACH (online with bank auth).
- APBS (Aadhaar Payments Bridge System) is a NACH variant for DBT (Direct Benefit Transfer).

---

## BBPS — Bharat Bill Payment System

- Standardized bill aggregation rail (electricity, gas, telecom, etc.).
- Two-tier: BBPCU (NPCI) + BBPOUs (member operating units).

---

## Operational Concerns

| Concern | Rail | Note |
|---|---|---|
| Dispute model | UPI | Through PSP → bank → NPCI Dispute Mgmt System (DMS); SLAs per NPCI circular |
| Reversal model | NEFT/RTGS | RTGS final and irrevocable — recovery is via mutual agreement only |
| Chargeback | UPI | Limited window; defined dispute reason codes |
| Failure rates | All | Reported in NPCI monthly stats; UPI ~0.5% TD (Technical Decline) typical |
| KYC | All | Sender bank's KYC governs; receiver KYC implied via account ownership |

---

## Sources to Ingest

- RBI Master Direction on Payment System Operators
- RBI circulars on NEFT/RTGS 24x7 and zero-charge regimes
- NPCI Procedural Guidelines (UPI, IMPS, AePS, NACH)
- NPCI Operating Circulars (rolling — subscribe to updates)
- Internal: bank's payments platform technical docs, dispute SOPs, reconciliation runbooks

---

## Open Questions

- [ ] Confirm current per-txn limits (these change often — never quote from this doc without checking the latest circular).
- [ ] UPI cap on individual TPAP — current status of the 30% rule.
- [ ] Cross-border UPI corridors live as of today.
