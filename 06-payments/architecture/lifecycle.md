# Payment Lifecycle in Large Banks

End-to-end stages of a payment in a tier-1 bank. Each stage is a discrete responsibility executed by one or more systems, with defined controls, SLAs, and exception paths.

> Companion: [systems-landscape.md](systems-landscape.md) maps the stages below to system categories; [payment-engines.md](payment-engines.md) names the commercial products that implement these stages.

---

## Lifecycle Map

```
                     ┌──────────────────────────────────────────────────┐
                     │                  CHANNELS                         │
                     │  Branch • Internet • Mobile • Corporate Host-to-  │
                     │  Host • API • Open Banking • ATM • POS • SWIFT FI │
                     └────────────────────────┬─────────────────────────┘
                                              │
                                              ▼
   ┌──────────────────────────────────────────────────────────────────────┐
   │  1. Initiation / Capture                                              │
   │  2. Pre-validation (syntax, identifiers, calendar)                    │
   │  3. Enrichment (rate, fees, beneficiary lookup, BIC/IBAN/IFSC)        │
   │  4. Authorization (entitlement, mandate, signing)                     │
   │  5. Funding check (intraday liquidity, customer balance)              │
   │  6. Fraud screening                                                   │
   │  7. Sanctions screening                                               │
   │  8. AML screening / transaction monitoring                            │
   │  9. Compliance + regulatory checks (Travel Rule, jurisdiction)        │
   │ 10. Routing decision (rail selection)                                 │
   │ 11. Format transformation (canonical → rail-specific)                 │
   │ 12. Submission to clearing/scheme                                     │
   │ 13. Clearing (scheme processing)                                      │
   │ 14. Settlement (inter-bank, on operator books)                        │
   │ 15. Posting (debit + credit on customer / suspense / GL)              │
   │ 16. Notification (customer + counterparty + regulator)                │
   │ 17. Reconciliation (nostro / vostro / scheme nets)                    │
   │ 18. Reporting (regulatory + MI + audit)                               │
   │ 19. Exception handling (returns, repairs, investigations)             │
   │ 20. Dispute / chargeback / refund                                     │
   │ 21. Archival                                                          │
   └──────────────────────────────────────────────────────────────────────┘
```

Steps 1–12 are typically pre-posting and can fan out across many systems within seconds. Steps 13–17 are settlement / post-settlement. Steps 18–21 are sustaining.

---

## Stage Detail

### 1. Initiation / Capture
The payment is created by the originator — customer (retail / corporate), system (recurring debit), or internal process (treasury sweep).

| Channel | Capture System |
|---|---|
| Internet / Mobile | Digital banking platform |
| Branch | Branch / teller system |
| Corporate | Host-to-host file (NACHA, ISO 20022, MT) + SWIFT for Corporates (S4C) |
| API | Open API gateway |
| Open Banking PISP | PISP front-end → ASPSP API |
| ATM / POS | Card terminal / acquirer |
| SWIFT FI-to-FI | SWIFT Alliance Gateway inbound |

The payment is materialised into the bank's **canonical payment record** (often called the canonical order, IPM record, or payment object).

### 2. Pre-validation
Syntax, mandatory field presence, value-date calendar, currency support, identifier format (IBAN, BIC, IFSC, account number checksum). Failures bounce back to the channel before any cost is incurred downstream.

### 3. Enrichment
- Beneficiary / counterparty lookup (BIC directory, LEI, internal CIF).
- FX rate sourcing (treasury rate, customer-tier rate, scheme rate).
- Fee schedule attachment.
- Address completion (post-CBPR+, structured creditor/debtor required).
- Internal account resolution.

### 4. Authorization
Customer authorisation:
- **Retail**: SCA / 2FA / device-bound credentials / biometrics.
- **Corporate**: multi-signatory, segregation of duties, host-to-host channel-level auth + per-payment hash-signed approval.
- **Mandate-driven**: pre-authorised Direct Debit, UPI AutoPay, e-Mandate, Bacs DD.

Internal authorisation:
- Entitlement service confirms the user can initiate this payment type for this currency / counterparty / amount.

### 5. Funding Check
- Customer balance check (debit side).
- Hold / earmark funds.
- Intraday liquidity check (bank-side, for high-value RTGS payments).
- Credit limit / overdraft check.
- For corporate batch files: pre-funded position or aggregate limit.

### 6. Fraud Screening
ML + rules engine. Inspects:
- Velocity, anomaly, peer comparison.
- Device + behavioural biometrics.
- Counterparty risk + first-party-mule signals.
- For real-time rails: scoring within ~150–300ms budget.

Hits route to a fraud queue; high-confidence hits hold the payment.

### 7. Sanctions Screening
Deterministic name + identifier matching against:
- OFAC SDN + sectoral (US Treasury).
- EU Consolidated List.
- HMT / OFSI (UK).
- UN Security Council.
- SECO (CH).
- Country-specific lists.
- Internal high-risk list.

True hits go to investigators; auto-cleared on next list refresh if list change resolves it. False positives go through whitelisting + audit trail.

### 8. AML Screening / Transaction Monitoring
Post-event (typically) anomaly detection over rolling windows:
- Structuring / smurfing detection.
- Geographic risk concentration.
- Pattern-of-life deviations.
- Networked entity exposure.

Generates alerts → analyst → SAR / STR filing if confirmed.

### 9. Compliance / Regulatory Checks
- **Travel Rule** completeness — FATF Rec 16 / FinCEN Travel Rule / EU Funds Transfer Regulation.
- **PSD2 SCA** confirmation persisted.
- **Jurisdictional rules** — e.g., RBI data localisation, EU GDPR cross-border restrictions.
- **Tax reporting** — FATCA / CRS classification.
- **Disclosure / KID** for relevant products.
- **High-risk corridor policy** internal flagging.

### 10. Routing Decision
Choose the **rail** (FedNow vs RTP vs ACH vs FedWire; FPS vs CHAPS vs Bacs; UPI vs IMPS vs NEFT vs RTGS; SWIFT vs SEPA vs alt rail). Driven by:
- Currency.
- Speed requirement / SLA.
- Cost optimisation.
- Counterparty reachability (BIC directory, scheme membership).
- Customer preference / agreement.
- Regulatory constraint.
- Operational state (rail health, queue depths).

A **rail-aware routing engine** is a core capability of modern payment hubs.

### 11. Format Transformation
Canonical payment record → rail-specific message:
- ISO 20022 `pacs.008` for SEPA, CHAPS, FedNow, RTP, CBPR+ cross-border.
- ISO 20022 `pacs.009` for FI-to-FI.
- SWIFT MT103/MT202 for legacy cross-border (sunsetting Nov 2025).
- NACHA file format for ACH.
- ISO 8583 for card auth.
- Scheme-specific internal protocols (NPCI UPI APIs, FedNow API).

Validation against scheme rule sets (CBPR+, HVPS+, EPC SCT Inst, NACHA, etc.).

### 12. Submission
Through bank's gateway:
- SWIFT Alliance Access / Gateway → SWIFT FIN / FINplus.
- Direct connectivity to FedACH / FedWire / FedNow / TCH RTP / CHIPS.
- Pay.UK FPS / Bacs / CHAPS gateways.
- NPCI UPI Switch / NEFT / RTGS connectivity (RBI-managed).
- Card scheme acquirer connectivity (V.I.P., Banknet, RuPay net, etc.).

### 13. Clearing
Scheme accepts, validates, and routes to the receiving FI. For:
- RTGS rails (FedWire, CHAPS, RTGS-IN, T2): immediate operator-side validation + post.
- Instant rails: sub-10s end-to-end including ACK to sender.
- Deferred rails (ACH, Bacs, NEFT, SEPA CT non-Inst): batched per window.

### 14. Settlement
Inter-bank money movement on operator books. Models:
- **RTGS**: gross, immediate (FedWire, CHAPS, RTGS-IN, FedNow / RTP on prefunded basis).
- **DNS**: deferred net, batched (ACH, NEFT, Bacs DC/DD).
- **Hybrid**: CHIPS, EBA Clearing STEP2.

Bank's **nostro / vostro** (or master account) is the source of truth for settled position.

### 15. Posting
On settlement (or in some models, on commitment), customer accounts and internal GL are updated:
- Debit customer + credit suspense → on settlement, suspense → nostro / interbank GL.
- For instant rails: real-time posting on both sides + interbank net settled later.

Core Banking System (CBS) handles posting and accrual.

### 16. Notification
- Customer: push notification, statement entry, email, SMS.
- Counterparty: ISO 20022 `camt.054` notification.
- Regulator: depending on threshold (e.g., FinCEN CTR, FIU-IND STR).
- Internal MI: live dashboards.

### 17. Reconciliation
Continuous matching across:
- Bank's GL vs. nostro statement (`camt.053`, MT940).
- Bank's transactions vs. scheme net settlement.
- Bank's internal channel records vs. payment hub records.
- Card: issuer / acquirer / scheme three-way.

Reconciliation tools surface breaks; suspense accounts hold un-matched items.

### 18. Reporting
- **Regulatory**: large-value transaction reports, cross-border transfer reports, EMIR-like transaction reporting (for derivatives-adjacent payments), Travel Rule logs, FATF Rec 16 audit.
- **Internal MI**: STP rates, decline rates per rail, fraud loss rates, NPS-equivalent metrics.
- **Audit**: immutable retrieval trail (see [../03-governance/audit-controls.md](../../03-governance/audit-controls.md)).

### 19. Exception Handling
- **Returns** — scheme-formal return messages (`pacs.004`, NACHA returns, Bacs ARUDD, etc.).
- **Repairs** — fixable items (e.g., missing 56A intermediary) re-submitted after correction.
- **Investigations** — `camt.029` / `camt.027` / `camt.087` over SWIFT; bilateral comms for non-SWIFT.
- **Cancellations** — `camt.056` (where supported and within window).
- **Recalls** — bilateral, often via `camt.087` Resolution of Investigation flow.

### 20. Dispute / Chargeback / Refund
- **Cards**: scheme chargeback rights per Visa / Mastercard / etc. dispute rulebooks.
- **UPI**: NPCI DMS dispute flow.
- **APP fraud**: UK PSR reimbursement (50/50 PSP), other jurisdictions emerging.
- **Direct Debit**: Bacs Direct Debit Guarantee — immediate refund.
- **Unauthorized EFT**: Reg E (US) consumer rights.

### 21. Archival
Long-term retention per regulator (typically 5–10 years; some jurisdictions longer for AML). Indexed for retrieval per [../03-governance/audit-controls.md](../../03-governance/audit-controls.md).

---

## SLA Profile by Rail

| Stage | RTGS (FedWire / CHAPS / RTGS-IN) | Instant (FedNow / RTP / UPI / FPS / SCT Inst) | Deferred (ACH / Bacs / NEFT / SEPA CT) | Card auth |
|---|---|---|---|---|
| Pre-validation | < 100ms | < 100ms | < 5s in file pipeline | < 50ms |
| Fraud + sanctions | < 500ms | < 300ms (parallel) | Pre-window batch | < 100ms |
| Submission to clearing | < 1s | < 2s | Window-driven | < 100ms |
| Clearing finality | Seconds | < 10s | Hours to days | Auth response < 200ms; settle T+1 to T+3 |
| Customer notification | < 5s | < 5s | EOD or next day | Real-time |

---

## Common Failure Modes

| Failure | Stage | Customer Impact | Resolution |
|---|---|---|---|
| Sanctions true match | 7 | Payment held | Investigator review; release or reject |
| Fraud high-risk score | 6 | Step-up auth or block | Customer call-back / decline |
| Insufficient funds | 5 | Decline | Customer top-up / return |
| Beneficiary BIC unreachable | 10 | Routing failure | Alternate rail / repair |
| Format reject at scheme | 11 / 13 | Reject from scheme | Repair + resubmit |
| Scheme outage | 12+ | Stuck queue | Failover rail / customer comms |
| Posting failure (CBS down) | 15 | Pending / discrepancy | Suspense + replay on recovery |
| Recon break | 17 | Internal — bank only | Investigations team |
| Cancel after settlement | 19 / 20 | Customer cannot reverse alone | Bilateral recall, scheme dispute, or APP fraud claim |

---

## Open Questions

- [ ] Confirm the bank's **canonical payment record** schema — every chunk in this lifecycle should map to a field there.
- [ ] Confirm intraday liquidity check architecture (real-time vs. periodic position).
- [ ] Confirm fraud + sanctions parallelisation strategy (serial vs. parallel; trade-off latency vs. blocking).
- [ ] Confirm exception-handling ownership matrix per rail / per stage.
