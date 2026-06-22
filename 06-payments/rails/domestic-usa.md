# Domestic USA Payment Rails

Authoritative references: **Federal Reserve Operating Circulars (5, 6, 8)**, **NACHA Operating Rules**, **The Clearing House (TCH) RTP & CHIPS Rulebooks**, **Regulation CC / E / J**, **BSA & FinCEN guidance**.

> Sub-domain: `DomesticUS`
> Owner: Payments Product + Operations (US)
> Default sensitivity: `Internal` (operator rulebooks); `Confidential` (transaction data, customer PII)

---

## At-a-Glance Comparison

| Rail                        | Operator                         | Settlement Model                                           | Window                     | Typical Use                             | Limit                                     |
| --------------------------- | -------------------------------- | ---------------------------------------------------------- | -------------------------- | --------------------------------------- | ----------------------------------------- |
| ACH (standard)              | Federal Reserve + TCH (EPN)      | Deferred net, multiple windows                             | Business days              | Payroll, bills, B2B                     | No regulatory cap; ODFI sets              |
| Same-Day ACH                | Same as ACH                      | Deferred net, three same-day windows                       | Business days              | Urgent payroll, B2B                     | USD 1M per txn (raised 2022)              |
| FedWire Funds Service       | Federal Reserve                  | RTGS (final, irrevocable)                                  | 22h/business day (Mon–Fri) | High value, time-critical               | No limit                                  |
| FedNow                      | Federal Reserve                  | RTGS, instant                                              | 24x7x365                   | Retail instant credit transfer          | USD 500,000 default (configurable per FI) |
| RTP (TCH)                   | The Clearing House               | RTGS, instant                                              | 24x7x365                   | Retail instant credit transfer          | USD 10M (raised from 1M, Feb 2025)        |
| CHIPS                       | The Clearing House               | Hybrid: netted with finality optimization                  | ~21h/business day          | High value, wholesale, FX correspondent | No regulatory cap                         |
| Check 21 (image clearing)   | Federal Reserve + private        | Imaged check exchange + ACH-back                           | Business days              | Legacy checks                           | Bank policy                               |
| Zelle                       | Early Warning Services           | Overlay: directory + risk; settled over RTP / FedNow / ACH | 24x7                       | P2P, small biz, B2C disbursements       | Bank-set                                  |
| Card networks (domestic)    | Visa, Mastercard, Discover, Amex | Authorization → clearing → net settlement                  | 24x7 auth                  | POS, e-commerce, ATM                    | Issuer-set                                |
| FedCash / Currency Services | Federal Reserve                  | Physical                                                   | Business days              | Cash supply to banks                    | n/a                                       |

Limits and windows change. Always cite the latest Federal Reserve / NACHA / TCH circular.

---

## ACH — Automated Clearing House

**Operators**: Federal Reserve (FedACH) + The Clearing House (Electronic Payments Network, EPN). Banks choose their operator(s).
**Rule-maker**: NACHA — National Automated Clearing House Association. Annual Operating Rules + Guidelines.
**Model**: Deferred Net Settlement. Files are batched and exchanged in windows.

### Settlement Windows

| Window                | Cut-off (ET) | Settlement               |
| --------------------- | ------------ | ------------------------ |
| Same-Day ACH window 1 | 10:30 AM     | 1:00 PM same day         |
| Same-Day ACH window 2 | 2:45 PM      | 5:00 PM same day         |
| Same-Day ACH window 3 | 4:45 PM      | 6:00 PM same day         |
| Standard ACH          | EOD          | Next business day or T+2 |

### Standard Entry Class (SEC) Codes

Defines how the consumer authorised the transaction. The SEC code drives risk, return windows, and consumer protections.

| Code          | Channel                                      | Common Use                                       |
| ------------- | -------------------------------------------- | ------------------------------------------------ |
| `PPD`         | Written / Prearranged Payment                | Payroll, recurring bills (mandate on file)       |
| `CCD`         | Corporate Credit/Debit                       | B2B vendor payments                              |
| `CTX`         | Corporate Trade Exchange                     | B2B with 820 addenda                             |
| `WEB`         | Internet-initiated                           | Online bill pay, recurring online                |
| `TEL`         | Telephone-initiated                          | One-time phone auth                              |
| `IAT`         | International ACH Transaction                | Cross-border ACH; full Travel Rule data required |
| `POP`         | Point-of-Purchase                            | Check converted at retail                        |
| `ARC` / `BOC` | Accounts Receivable Conversion / Back Office | Mailed check converted to ACH                    |
| `RCK`         | Re-presented Check                           | Bounced check re-presentment                     |
| `XCK`         | Destroyed Check                              | Recovery                                         |
| `MTE`         | Machine Transfer Entry                       | ATM                                              |
| `POS`         | Point-of-Sale                                | POS debit (older usage)                          |

### Return Reason Codes (selected)

| Code  | Reason                                              |
| ----- | --------------------------------------------------- |
| `R01` | Insufficient funds                                  |
| `R02` | Account closed                                      |
| `R03` | No account / unable to locate                       |
| `R04` | Invalid account number                              |
| `R05` | Unauthorized debit to consumer (returned by RDFI)   |
| `R07` | Authorization revoked by customer                   |
| `R10` | Customer advises not authorized                     |
| `R11` | Customer advises entry not in accordance with terms |
| `R29` | Corporate customer advises not authorized           |

Return windows: 2 banking days for most administrative; 60 days for unauthorized consumer (`R05`, `R07`, `R10`).

### File Format

NACHA file format (legacy). Header / Batch Header / Entry Detail / Addenda / Batch Control / File Control. Fixed-width ASCII.

### Same-Day ACH Specifics

- Per-transaction cap raised to **USD 1,000,000** (March 2022).
- All SEC codes eligible except IAT.
- ODFI marks an entry as SDA via the effective date and Same-Day indicator.

### IAT (International ACH)

- Cross-border ACH in/out of the US.
- Carries full Travel Rule fields (originator + beneficiary name, address, identification, etc.) per BSA / FinCEN.
- OFAC screening applies on both sides.

### Key Risk Topics

- **R05 / R07 / R10 returns** — consumer-protection returns; tracked by NACHA; threshold breaches trigger ODFI sanctions.
- **Third-Party Sender obligations** — TPS originating on behalf of multiple end-users have heightened diligence requirements.
- **Account Validation Rule** — for WEB debits, ODFI must use a "commercially reasonable" method to verify account ownership before first use.

---

## FedWire Funds Service

**Operator**: Federal Reserve.
**Model**: RTGS — real-time, gross, final, irrevocable.
**Window**: 21h/business day (currently 21:00 ET previous day — 19:00 ET; verify current schedule).
**Standard**: Migrating to ISO 20022 (pacs.009 baseline). Confirm current migration cutover state.

### Key Points

- Final and irrevocable on Fed books. **No reversal.** Recovery from incorrect destination requires bilateral cooperation.
- Reg J governs FedWire. Originator's bank typically guarantees the wire.
- Used for: high-value corporate, treasury, real-estate closings, securities settlement, inter-bank.

### Common Message Field Concepts

- IMAD / OMAD — Input / Output Message Accountability Data, the FedWire equivalent of a UETR.
- BTR (Business Function Code) — purpose categorisation.
- Originator + Beneficiary structured fields post-ISO 20022 migration.

---

## FedNow Service

**Operator**: Federal Reserve.
**Live**: July 2023.
**Model**: 24x7x365 instant credit transfer, RTGS, final.
**Standard**: ISO 20022 native (`pacs.008`, `pacs.002`, `camt.054`, `camt.056`, etc.).
**Default per-transaction cap**: USD 500,000 (PSPs can configure lower; cap may rise).

### Architecture

```
Sender Customer → Sender FI → FedNow Service (Fed)
                                    → Receiver FI → Receiver Customer
```

Each FI maintains its own connection (direct or via service provider). Settlement is on the Fed's books — final.

### Key Features

- **Liquidity Management Transfer (LMT)** — between FIs' Master accounts even on non-banking days to fund FedNow / RTP positions.
- **Request for Payment (RfP)** — payee can request a push from payer (no pull rail, but RfP simulates it).
- **Negative response on rejection** — `pacs.002` with rejection reason.
- **Tokenization / aliases** — not yet standard at the network level; FIs add their own directories.

### Operating Circular 8

Defines the rules. Read alongside the Service Description and the Fraud Mitigation Toolkit.

---

## RTP — Real-Time Payments (TCH)

**Operator**: The Clearing House.
**Live**: 2017.
**Model**: 24x7x365 instant credit transfer, RTGS-style on TCH-held pre-funded position at the Fed.
**Standard**: ISO 20022 (pacs.008, pacs.002, etc.).
**Per-transaction cap**: USD 10,000,000 (raised from USD 1M in Feb 2025).

### Differences vs. FedNow

| Dimension  | RTP (TCH)                                           | FedNow (Fed)                |
| ---------- | --------------------------------------------------- | --------------------------- |
| Operator   | Private (TCH consortium)                            | Public (Fed)                |
| Settlement | TCH-held prefunded account at Fed                   | Master Account on Fed books |
| Cap        | USD 10M                                             | USD 500k (default)          |
| Coverage   | TCH member FIs (covers ~80% of US deposit accounts) | All Fed-eligible FIs        |
| RfP        | Yes                                                 | Yes                         |
| Live since | 2017                                                | 2023                        |

US banks typically connect to **both**; routing is by directory + reachability.

### Common Message Types

- `pacs.008` — credit transfer
- `pacs.002` — payment status report
- `camt.056` — payment cancellation request
- `pain.013 / pain.014` — Request for Payment + response

### Confirmation of Payee Equivalent

US does not yet have a national CoP. Some FIs and overlays (Zelle directory, ValidiFI) provide name-check at the application layer. Compare with UK's mandatory CoP.

---

## CHIPS — Clearing House Interbank Payments System

**Operator**: The Clearing House.
**Model**: Netted with continuous bilateral / multilateral settlement throughout the day; finality during the operating day, EOD net.
**Window**: ~21h/business day.
**Standard**: ISO 20022 migration completed 2024.
**Typical use**: Large-value, US-dollar correspondent banking, FX settlement, big-ticket commercial.

### Distinctive Features

- **Pre-funded** — members post collateral / pre-fund.
- **Intraday finality optimization** — algorithm releases queued payments as soon as bilateral / multilateral nets allow.
- **Reach** — virtually all USD correspondent banking flows.
- **Cost** — generally cheaper than FedWire for participants on a per-transaction basis at volume.

CHIPS and FedWire are complementary. CHIPS dominates correspondent USD; FedWire dominates immediate finality use cases.

---

## Check 21 — Image Clearing

**Authority**: Check Clearing for the 21st Century Act (2003) + Regulation CC.
**Model**: Substitute checks (image replacement documents, IRDs) given the same legal force as the original paper check.
**Operator**: Federal Reserve Check Services + private exchanges (e.g., SVPCO, ECCHO).

### Why It Matters

Although check volume has fallen, Check 21 still represents a meaningful share of US payments by value (especially B2B). The image is exchanged electronically; the underlying value moves over ACH or correspondent settlement.

### Funds Availability (Reg CC)

- Next-business-day for most deposits.
- Exception holds for large items, repeat-overdraft accounts, etc.
- Post-2020 Reg CC inflation adjustments raised the trigger thresholds.

---

## Zelle

**Operator**: Early Warning Services (EWS) — a joint venture of seven large US banks.
**Model**: Directory + risk + dispute overlay; settlement underneath is RTP or FedNow (real-time) or ACH (deferred), depending on FI.
**Reach**: Most large US bank checking customers.

### Key Operational Points

- Aliases: email or US mobile number.
- Per-transaction and rolling caps set by each FI.
- Disputes — Zelle adopted enhanced reimbursement policies after CFPB pressure on APP fraud (2023). Verify current state.
- Strong consumer awareness but no central instant rail underneath — actual settlement is bank-dependent.

---

## Card Networks (Domestic Context)

US card flows largely operate over the same scheme rails as cross-border (Visa, Mastercard, Discover, Amex). Domestic specifics:

- **Durbin Amendment** — debit interchange capped for FIs with > USD 10B in assets.
- **PIN debit networks** — STAR, NYCE, Pulse, Accel, etc. Competing routing under Reg II.
- **Reg II routing requirements** — merchants must have at least two unaffiliated network choices for debit, even card-not-present (recent CFPB clarification).
- **Push-to-card** — Visa Direct + Mastercard Send used for instant payouts (claims, payroll advances, marketplace).

See [iso-8583.md](../standards/iso-8583.md) for the underlying message format.

---

## Settlement Models Summary

| Rail           | Finality                             | Reversibility                                     | Risk Implication                 |
| -------------- | ------------------------------------ | ------------------------------------------------- | -------------------------------- |
| FedWire        | At message receipt by Fed            | No reversal; recovery only by agreement           | Sender bank bears risk           |
| FedNow         | At credit to receiver Master Account | No reversal; return request only with cooperation | RTGS — operational risk dominant |
| RTP            | At credit to receiver TCH position   | No reversal; return request                       | RTGS-style                       |
| CHIPS          | Intraday + EOD finality              | None after release                                | Pre-funding manages credit risk  |
| ACH            | At settlement (T+0 or T+1)           | Returns within rule windows                       | Counterparty + duplication risk  |
| Same-Day ACH   | Same as ACH, accelerated             | Returns within rule windows                       | Same risk profile                |
| Check 21 / IRD | At Reg CC availability               | Returns within Reg CC                             | Float + image-fraud risk         |
| Zelle          | Per underlying rail                  | Per underlying rail + EWS overlay                 | APP fraud surface                |

---

## Regulators & Authorities (US Payments)

| Body                 | Scope                                                                                            |
| -------------------- | ------------------------------------------------------------------------------------------------ |
| **Federal Reserve**  | Operates FedWire, FedNow, FedACH, Check Services; Reg E, J, CC, II; supervises member banks      |
| **OCC**              | Supervises national banks; operational risk including payments                                   |
| **FDIC**             | Supervises state non-member banks; deposit insurance                                             |
| **CFPB**             | Consumer financial protection — payments fraud, errors, disclosures (Reg E enforcement at scale) |
| **FinCEN**           | BSA / AML enforcement; SAR / CTR filings; Travel Rule                                            |
| **OFAC**             | Sanctions screening; SDN list + sectoral programs                                                |
| **NACHA**            | ACH rulebook                                                                                     |
| **TCH**              | RTP and CHIPS rulebooks                                                                          |
| **State regulators** | Money transmitter licensing (per state); NMLS registration                                       |
| **NCUA**             | Federal credit union supervisor (payments to extent of CU activity)                              |

---

## Key Regulations & Operating Circulars

| Regulation                       | Scope                                                                                          |
| -------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Regulation E** (12 CFR 1005)   | Consumer electronic fund transfer rights; error resolution; unauthorized transaction liability |
| **Regulation J** (12 CFR 210)    | FedWire / FedACH operating terms                                                               |
| **Regulation CC** (12 CFR 229)   | Funds availability + Check 21                                                                  |
| **Regulation II** (12 CFR 235)   | Debit interchange + routing (Durbin)                                                           |
| **Bank Secrecy Act**             | AML foundation; CTR, SAR, Travel Rule                                                          |
| **FinCEN Travel Rule**           | ≥ USD 3,000 originator + beneficiary info                                                      |
| **NACHA Operating Rules**        | ACH primary rulebook (annual updates)                                                          |
| **TCH RTP Operating Rules**      | RTP rulebook                                                                                   |
| **Federal Reserve OC 5, 6, 8**   | Wholesale Wire Transfers; FedACH; FedNow                                                       |
| **State Money Transmitter laws** | License + bonding per state for non-bank PSPs                                                  |

---

## Cross-Border Considerations from US

| Scenario                  | Rail Options                                                                                                 |
| ------------------------- | ------------------------------------------------------------------------------------------------------------ |
| USD wire out              | FedWire (Fed-eligible counterparty), CHIPS (correspondent network), SWIFT MT103/pacs.008 + correspondent leg |
| USD wire in               | Same — depending on routing                                                                                  |
| Foreign currency from USD | SWIFT cross-currency + FX leg                                                                                |
| Cross-border ACH          | IAT SEC code (limited reach); typically replaced by SWIFT or RTP-equivalent overlays                         |
| Card cross-border         | Visa, Mastercard, Discover, Amex — handled by scheme + interchange                                           |

---

## Sources to Ingest

- NACHA Operating Rules + Operating Guidelines (annual + supplements)
- Federal Reserve Operating Circulars 5, 6, 8 + Service Descriptions (FedWire, FedACH, FedNow)
- TCH RTP Operating Rules + CHIPS Rules
- Reg E, J, CC, II (12 CFR Parts 1005, 210, 229, 235)
- FinCEN guidance + BSA examination manual sections relevant to payments
- OFAC SDN + sectoral lists (real-time)
- CFPB enforcement letters and circulars relevant to payments + Zelle / APP fraud
- Internal: bank's ACH origination policies, FedWire / FedNow operations runbooks, RTP / CHIPS connectivity docs, sanctions playbook, NACHA Third-Party Sender register

---

## Open Questions

- [ ] Confirm bank's RTP and FedNow connectivity status (direct vs. service provider).
- [ ] Confirm FedWire ISO 20022 cutover state — relevant to message-translation chunks in the KB.
- [ ] Internal stance on Zelle membership and APP fraud reimbursement obligations.
- [ ] State money transmitter licensing footprint (drives jurisdiction filters in retrieval).
- [ ] Same-Day ACH per-day file cutoff policies internal to the bank.
