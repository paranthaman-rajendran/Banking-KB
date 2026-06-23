# Treasury Services / Cash Management

Treasury Services — JPMC TS, BofA GTS, Wells WCB, Citi TTS — is the bank's **cash-management revenue engine** for corporate clients. Multi-billion-USD revenue lines at tier-1 banks; sticky, counter-cyclical, deeply integrated into corporate operations.

> One of the major gap areas identified in [../../gap-analysis-tier1-bank.md](../../gap-analysis-tier1-bank.md). Universal-bank readers should treat this as priority content.

---

## Integrated Payables

A single corporate **payment file** in → multi-rail out (ACH, wire, RTP, FedNow, card, check). The bank decides per payment which rail is optimal.

### How It Works
1. Corporate submits a single payment file (NACHA, ISO 20022, CSV, EDI 820, etc.) via H2H or portal.
2. Bank's IP platform classifies each payment by:
   - Amount + timing (small + non-urgent → ACH; large + urgent → wire; instant → FedNow / RTP; small recurring vendor → check still common).
   - Beneficiary capability (does the payee have RTP-eligible account?).
   - Customer's rate preferences.
3. Each payment is routed to the chosen rail.
4. Status returned to corporate (success / fail / pending) per scheme.

### Common Vendor Stacks
- **Bottomline Technologies** — Cyber Fend, PT-X, Universal Aggregator.
- **Fiserv** — ImageCenter, Payment Manager.
- **FIS** — PayDirect, Open Payment Framework integrations.
- **Bank-built** — common at tier-1.

### Value Proposition
- Corporate sends one file instead of multiple per-rail files.
- Bank does optimisation (cost, speed, reach).
- Single reconciliation file back to corporate.
- Reduces corporate ERP integration burden.

---

## Integrated Receivables (IR)

Multi-channel in (lockbox, ACH, wire, card, RTP, FedNow) → **matched against open invoice file**. Closes receivable + cash positioning in real time.

### How It Works
1. Corporate provides open-invoice file (ERP extract).
2. Bank's IR platform matches incoming payments to invoices using:
   - Invoice number in payment remittance.
   - Amount match.
   - Customer-of-customer name fuzzy match.
   - AI-driven matching for the unmatched.
3. Matched payments auto-apply; unmatched go to exception queue.
4. Output: post-matched file back to corporate ERP.

### Modern AI Layer
- ML models for fuzzy-matching unstructured remittance text.
- LLM-augmented matching gaining ground (2024+).
- Match rate: 85–95% auto-match is achievable target.

### Vendor Stacks
- **Fiserv ImageCenter Connect**.
- **HighRadius** — AR-specialist with bank-partnership model.
- **Billtrust** — receivables automation.
- **FIS GETPAID**.
- **Bank-built** — common at tier-1.

---

## Lockbox

Cheque + remittance collection at scale. Despite cheque-decline narrative, lockbox volumes at large US banks remain significant (B2B insurance, healthcare, real-estate, government).

### Variants

| Variant | Description |
|---|---|
| **Wholesale Lockbox** | Large-dollar B2B; complex remittance; longer processing |
| **Retail Lockbox** | Consumer payments (utility bills); high volume + low value |
| **Image Lockbox** | All-electronic — cheques imaged + data captured; physical destroyed |
| **Wholetail / Wholesale Image** | Hybrid |
| **Electronic Lockbox** | ACH credits routed to a virtual lockbox account; no paper |

### Operations
- Cheque receipt at bank-operated processing centre.
- High-speed cheque scanner + OCR / ICR for amount + payor.
- Remittance document scanned alongside.
- Image archived (Check 21 IRD for the substitute).
- Data extracted (account, amount, invoice number).
- Match + post + report to corporate.

### Vendor Stacks
- **Fiserv ImageCenter**.
- **FIS Lockbox** (formerly SunGard).
- **Bottomline Lockbox**.
- **Deluxe / Wausau Financial Systems**.
- **Bank-built** — common.

---

## Account Reconciliation Services (ARP)

Bank-provided reconciliation of the corporate's account activity against the corporate's records.

### Types
- **Full Reconciliation** — bank reconciles all items; outputs matched + unmatched.
- **Partial Reconciliation** — bank reconciles select items (typically cheques).
- **Positive Pay** — corporate provides issued-cheque list; bank declines any not matching.
- **Reverse Positive Pay** — bank presents all paid cheques to corporate for daily approval.
- **Payee-Match Positive Pay** — positive pay + payee name validation; reduces alteration fraud.

### Operations
- Daily output file to corporate (matched + exceptions).
- Corporate disposition on exceptions (approve / decline).
- Multi-day cycle for non-bank-decision items.

### Value Proposition
- Cheque fraud reduction (positive pay).
- Corporate accounting team efficiency.
- Audit-trail compliance.

---

## ZBA — Zero Balance Account

Multiple accounts auto-sweep balances to / from a single concentration account at EOD (or intraday). The sub-accounts always end the day at zero.

### How It Works
- Corporate sets up:
  - **Master / Concentration Account** — true balance lives here.
  - **Sub-accounts** — operating accounts that auto-zero.
- During the day, sub-accounts transact normally.
- At end-of-day (or intraday cycle), sweep moves all positive sub-account balances to master; covers any negative sub-account balances from master.

### Use Cases
- Multi-entity / multi-location operations.
- Different account purposes (operating, payroll, tax).
- Investment of consolidated balance in money market.

### CBS Implementation
- Sweep rules configured per pair / hierarchy.
- Sweep batch runs at defined times.
- Postings auto-generate at each sweep.

---

## Sweeps (Broader)

| Type | Description |
|---|---|
| **End-of-day sweep** | Standard EOD movement |
| **Target-balance sweep** | Leave target balance; sweep rest |
| **Threshold sweep** | Sweep only when balance exceeds threshold |
| **Multi-bank sweep** | Across banks via SWIFT messages |
| **Investment sweep** | Auto-invest in MMA / treasury sweep |
| **Loan-coverage sweep** | Auto-pay down loan / line of credit |

---

## Notional Pooling

Multiple accounts kept legally separate; **interest calculated on consolidated net balance**. No physical funds movement.

### How It Works
- Several accounts (often multi-currency or multi-entity).
- Bank consolidates balances daily for interest computation.
- Long balances + short balances offset.
- Interest applied to the net.

### Use Cases
- Tax-efficient (no physical inter-company movement).
- Treasury efficiency without commingling.
- Multi-currency pooling (with FX overlay).

### Limitations
- **US**: structurally difficult due to FDIC + GAAP treatment; less common.
- **EU + UK + APAC**: standard product.
- **Cross-border**: regulatory friction; often jurisdiction-by-jurisdiction.

---

## Virtual Accounts

A **single physical master account** at the bank holds the funds. The bank's CBS / virtual account platform tracks **per-virtual-account sub-balances**, each with its own account number.

### Use Cases
- **Fintech sponsor banking** — sponsor bank holds the master; fintech maps virtual accounts to its end-customers.
- **Property management / law firm escrow** — segregated client funds.
- **Marketplaces** — virtual account per seller for clean reconciliation.
- **Group treasury** — segregation across business units without separate physical accounts.

### Operations
- Customer-of-customer (Cosmo) accounting on the bank's books.
- Per-VA reconciliation files.
- Multi-currency VA where the platform supports.

### Vendor Stacks
- **Tietoevry** virtual accounts.
- **FIS** virtual accounts.
- **Bank-built** — typical at tier-1.

---

## ECR + Account Analysis (AA)

Compensation model unique to wholesale banking: corporate maintains operating balances; bank gives them "earnings credit" against fees.

### Earnings Credit Rate (ECR)
- Daily rate applied to **investable balance** (collected balance less reserve requirements).
- Bank-set; tracks short-term market rates.
- Customer-specific tier may apply.

### Investable Balance Computation
```
Ledger Balance              (sub-ledger balance per the bank's books)
- Float                    (cheques deposited but not collected)
= Collected Balance
- Reserve Requirement      (Fed-imposed reserves on demand deposits)
= Investable Balance
```

### AA Statement (Monthly)
- Detailed list of services consumed (per-product, per-volume).
- Service fees per service line.
- Average ledger / collected / investable balances.
- ECR-earned credits.
- Net fee position (positive = customer pays; negative = excess credit, often expires).

### Why It Matters
- Corporate Treasury can choose: pay fees explicitly or maintain balances.
- Most corporates blend — maintain partial balance, pay rest as fees.
- ECR competition between banks; corporate treasurers benchmark.

---

## Information Reporting (Real-Time + EOD)

### Real-Time / Intraday
- **camt.052** (ISO 20022 BankToCustomerAccountReport — intraday).
- **MT942** (SWIFT legacy).
- Delivered: streamed via API or periodic file.

### End-of-Day
- **camt.053** (ISO 20022 BankToCustomerStatement — EOD).
- **MT940** (SWIFT legacy).
- **BAI2** (legacy US format; still widely used).

### Per-Product Reports
- Lockbox detail (per cheque + image link).
- ARP daily output.
- Trade Finance status.

### Notification Services
- Wire received.
- Large debit / credit.
- Account hold / freeze.
- Fee charged.

---

## SWIFT for Corporates (S4C)

Multi-bank corporate SWIFT connectivity. Replaces or supplements proprietary bank portals.

### Models
- **MA-CUG** (Member-Administered Closed User Group) — bank-by-bank arrangements.
- **SCORE** (Standardised Corporate Environment) — SWIFT-administered; corporates apply to SWIFT; multi-bank.
- **SWIFT Bureau** — bank or 3rd-party provides connectivity to corporate.

### Benefit
- Single connectivity to many banks.
- Standardised message formats.
- Bank-agnostic.

### Limitations
- High setup cost.
- Maintenance overhead.
- Less rich than bank-native portal for some functions.

---

## ERP Integration

Modern treasury services connect directly to corporate's ERP:

| ERP | Integration Approach |
|---|---|
| **SAP S/4HANA + SAP TRM** | Native banking adapter |
| **Oracle ERP Cloud / EBS** | Oracle Banking Cloud Services or REST integration |
| **NetSuite** | Native banking + treasury workstations |
| **Microsoft D365** | Connector-based |
| **Treasury Workstations (Kyriba, ION, FIS Trax)** | Multi-bank, multi-ERP |

---

## Operational SLAs

| Operation | Typical SLA |
|---|---|
| Lockbox same-day credit | T+0 (early cut-off) to T+1 |
| ARP exception cycle | T+1 |
| ZBA / sweep | EOD same-day |
| Virtual account reconciliation | T+0 / T+1 |
| Information reporting (camt.053) | EOD + 1 hour |
| Wire investigation initial response | 24 hours |

---

## Open Questions

- [ ] Confirm bank's wholesale cash-management platform.
- [ ] Confirm Integrated Payables / Integrated Receivables product offering + vendor.
- [ ] Confirm lockbox network + processing capability.
- [ ] Confirm virtual-account platform.
- [ ] Confirm S4C / SCORE participation.
- [ ] Confirm ERP-integration partnerships.
- [ ] Confirm AA / ECR pricing framework + benchmarking process.
