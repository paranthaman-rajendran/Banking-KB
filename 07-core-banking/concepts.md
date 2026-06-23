# Foundational Concepts — Core Banking

Paragraph-style explainers for the generic terms that recur across retail + wholesale CBS designs. Companion to [../06-payments/concepts.md](../06-payments/concepts.md). For one-liners see a future glossary; for framing read this.

---

## Customer & Account Master

### Customer Master / CIF (Customer Information File)
A single identity record per **legal entity or natural person** the bank serves. The CIF holds identifying information (name, address, ID documents, contact info), demographic and segmentation data, KYC status, risk rating, relationship overview (linked accounts + products), and tax classification (FATCA / CRS). Every product (account, loan, card) links to a CIF. The CIF is the **golden source** for "who is this customer?" — every payment posting, every regulatory report, every credit decision references it.

Universal banks typically have **separate CIFs per legal-entity hierarchy** — retail customers in one CIF, corporate customers in another, with relationship-mapping where they overlap (e.g., the same person is the controlling shareholder of a corporate customer).

### Account Master
Per-account record holding product code, currency, opening date, status (active / dormant / closed / frozen), interest rate model, GL classification, regulatory categorisation, and the linked CIF. The account is the **booking unit** — every debit and credit lands on an account.

### Product Master
Per-product configuration — interest rates, fees, eligibility rules, regulatory categorisation, default GL mapping, accounting treatment. Centralising the product configuration on the CBS is what allows the bank to launch a new product without code changes.

### Account Number Structure
Account numbers carry meaning. A common pattern: branch code + product code + sequence number + check digit. India uses IFSC + account number; UK uses sort code (6 digits) + account number (8 digits); US uses ABA routing (9 digits) + account number; EU + UK use IBAN (country + check + bank + account). The CBS resolves the routing identifiers to the internal account ID.

---

## Posting & Accounting

### Double-Entry Bookkeeping
Every transaction posts **at least one debit and one credit** of equal value. A USD 1,000 wire from a customer's account debits the customer (their balance reduces) and credits the bank's nostro (the bank's funded position). The two postings together preserve the accounting identity (Assets = Liabilities + Equity).

### Debit vs Credit
From the **bank's perspective**:
- A customer's **deposit account balance** is a *liability* (the bank owes the customer). Crediting the account *increases* the bank's liability to that customer.
- A customer's **loan balance** is an *asset* (the customer owes the bank). Debiting the loan *increases* the bank's asset.

This is why customer-facing language inverts the accounting language: when you "credit" a customer's savings account, the customer's perspective is "money coming in" — but the bank's accounting entry is *increasing a liability*. Modern CBS UIs sometimes translate; legacy ones don't.

### General Ledger (GL) vs Sub-Ledger
- **GL** is the bank's accounting truth — aggregated balances per accounting category (Cash, Loans, Customer Deposits, Interest Income, etc.).
- **Sub-Ledger** is the per-customer / per-account detailed record. Sub-ledger balances aggregate up to GL balances.

Reconciling sub-ledger to GL is a daily discipline. Breaks land in suspense accounts pending investigation.

### Posting
The act of writing the debit + credit pair to the account master + GL. Posting can be:
- **Online / real-time** — the entry is written immediately on transaction commit (most modern instant-rail-aware CBS).
- **Batch** — entries accumulate during the day, posted at EOD (legacy / specific product types).

A modern CBS supports both for different product types.

### Value Date vs Book Date / Posting Date
- **Book Date** (or **Posting Date**) — when the transaction was posted to the books.
- **Value Date** — the date on which interest accrual treats the transaction as effective.

These differ when a deposit is booked on day T but valued on day T-1 (back-valued) or T+1 (forward-valued). Critical for interest computation, regulatory reporting, and cross-currency FX.

### Accrual Basis
Interest is computed on the running balance, accrued daily (or per the product's accrual frequency), and credited to the customer at a defined frequency (monthly, quarterly, yearly). The accrual basis (Actual/360, Actual/365, 30/360) is per-product.

### Reversal vs Correction
- **Reversal** — undoes an erroneous transaction by booking the opposite-sign entry, leaving both entries visible in audit.
- **Correction** — modifies the original entry (limited to specific entry types and within an authorisation framework).

Reversal is the safe operation; correction is restricted.

---

## Daily Cycle — BOD, EOD, and the Day's Posting Window

### Beginning-of-Day (BOD)
Pre-day-start processing: roll calendar, apply scheduled standing instructions, accrue overnight interest, post forward-dated payments, refresh exchange rates. BOD typically runs in the early-morning hours.

### Online Day
The bank is open for transactions. Real-time postings flow through.

### Cut-off (Daily Cut)
The boundary between Day T and Day T+1 for accounting purposes. Cut-off times vary by product (a payment received after cut-off books with T+1 value date). The **system cut-off** can differ from the **branch cut-off** and the **payment-rail cut-off**.

### End-of-Day (EOD)
Post-cut-off processing: close balances, compute average balances for AA / ECR, compute interest accrual, generate statements, run regulatory reports. EOD historically took hours on mainframes; modern in-memory CBS can complete in minutes or run continuously. Full job sequence, retail vs. wholesale differences, and EOD-specific failure modes: [eod-batch-cycle.md](eod-batch-cycle.md).

### 24x7 vs Batch-Bound CBS
Legacy CBS (older Finacle / Flexcube / T24 variants) cannot post during EOD — there's a "blackout window" of 30–120 minutes when retail rails are degraded. Modern CBS (Vault, 10x, Mambu, recent Finacle releases) run **24x7** with continuous posting — required for FedNow / UPI / FPS / SCT Inst real-time rails.

The CBS upgrade from batch-bound to 24x7 is a major architectural shift, often a multi-year programme.

---

## Deposits

### CASA — Current Account, Savings Account
Industry shorthand for **non-time** deposit accounts. Low-cost funding for the bank; high transactional volume. The CASA ratio (CASA / total deposits) is a closely-watched profitability metric.

### Time Deposit / Term Deposit
Deposit committed for a fixed term (3 months, 1 year, 5 years) at a fixed rate. Examples: Certificate of Deposit (US), Fixed Deposit (IN), Bonded Deposit, term savings. Higher rate to the customer; longer-tenor funding for the bank. Premature withdrawal typically incurs penalty.

### Demand Deposit vs Time Deposit
- **Demand** — payable on demand, no notice (CASA).
- **Time** — locked for a tenor.

This distinction shapes regulatory capital requirements (LCR HQLA treatment), interest economics, and customer-protection rules.

### NRI Variants (India)
- **NRE** — Non-Resident External; in INR; freely repatriable.
- **NRO** — Non-Resident Ordinary; in INR; restricted repatriation.
- **FCNR** — Foreign Currency Non-Resident; in foreign currency.

Each has distinct tax and FEMA treatment.

### Joint Accounts & Mandate Structures
Joint accounts can be **either or survivor**, **anyone or survivor**, **all parties signing**, **former or survivor**, etc. The mandate determines who can operate. Critical at customer death (estate processing); the CBS holds the mandate code and enforces it at posting time.

### Dormancy
An account untouched (no customer-initiated debit) for a defined window (e.g., 2 years in IN, varies by jurisdiction) is marked **dormant**. Dormancy reduces fraud exposure but adds friction to legitimate customer use. Long-term dormancy can trigger **escheatment** — funds transferred to the state's unclaimed-property regime.

### Escheatment
The legal handover of unclaimed deposits to a regulatory body after a long period (often 7–10 years). Treatment varies sharply by jurisdiction. In the US, state-level escheatment laws differ widely. In India, RBI's DEAF Fund holds these.

---

## Lending

### Principal, Interest, and Charges
A loan has:
- **Principal** — the amount lent, repayable over time.
- **Interest** — the cost of borrowing, computed on the outstanding principal at the contractual rate.
- **Charges / Fees** — origination, late payment, prepayment, NSF, etc.

Each is tracked separately on the loan account.

### Amortisation
The schedule by which principal is repaid:
- **Bullet** — entire principal at maturity; interest paid periodically.
- **EMI / Equated** — fixed monthly payment covering interest + principal; common for home / auto / personal loans.
- **Balloon** — small periodic payments + large final principal.
- **Custom schedule** — bespoke for project finance, commercial lending.

### Interest Rate Models
- **Fixed** — same rate throughout the tenor.
- **Floating** — rate resets periodically against a benchmark (SOFR, EURIBOR, MIBOR, internal MCLR).
- **Mixed** — fixed for an initial period, then floating.
- **Step-up / step-down** — schedule-defined rate changes.

### NPL / NPA Classification
Non-Performing Loans / Non-Performing Assets. Industry thresholds:
- **Performing** — current on payments.
- **SMA** (Special Mention Account, IN) — early signs of stress.
- **Substandard** — overdue 90 days.
- **Doubtful** — overdue longer.
- **Loss** — written off.

The CBS computes these classifications nightly based on overdue days; results feed risk reporting + provisioning calculations.

### IFRS 9 / CECL Provisioning
Modern accounting standards require **expected credit loss** provisioning at origination — not at default. IFRS 9 (international) and CECL (US) use different mechanics. The CBS feeds raw loan data; a dedicated risk engine computes ECL.

### Asset-Liability Management (ALM)
The bank manages the **interest-rate-sensitivity gap** between deposits (typically short-tenor) and loans (typically longer-tenor). The CBS supplies the cashflow buckets; ALM systems compute repricing gaps and Value-at-Risk.

---

## Customer Lifecycle

### Onboarding
- Identification + verification (KYC documents, biometrics, eKYC).
- Risk rating.
- Sanctions + PEP screening.
- Product offer + signing.
- Account opening + initial funding.
- Customer education.

### Activation
First customer-initiated transaction. Banks watch the lag between onboarding and activation as an engagement KPI.

### Servicing
Ongoing operations: statements, transactions, complaints, address changes, mandate changes, beneficiary updates.

### Closure
Customer-initiated or bank-initiated closure. Anti-tipping rules apply if AML-driven. Distinguish from dormancy (the account stays open but inactive).

### Deceased Customer Processing
On notification of death, the account is frozen pending estate documentation. Successor account flow under the mandate (e.g., E or S — Either or Survivor) drives release. Multiple-jurisdiction complications for cross-border customers.

---

## Wholesale-Specific Concepts

### Relationship Hierarchy
Wholesale customers have **legal-entity hierarchies**: parent → subsidiary → branch. The CBS must model the hierarchy because:
- Account limits roll up.
- Pricing tiers apply at parent level.
- Regulatory exposure (large-exposure rules) consolidates.

### Earnings Credit Rate (ECR)
The interest-equivalent credit a corporate customer earns on their **operating balances**, applied against fees rather than paid out. Allows the corporate to maintain balances as compensation in lieu of explicit fees. Calculated daily, surfaced on the monthly Account Analysis statement.

### Account Analysis (AA) Statement
Monthly corporate-banking statement summarising:
- Service fees + counts.
- Average ledger / collected / investable balance.
- Earnings credit at ECR.
- Net fee position.

Negotiated bilaterally; varies per customer.

### Sweeping
Automated movement of balances between accounts to a target. Common types:
- **Zero-balance sweep** — sweep all excess to a concentration account at EOD.
- **Target-balance sweep** — leave a target amount; sweep the rest.
- **Threshold sweep** — sweep only when balance exceeds a threshold.

### Notional Pooling
Multiple accounts are kept legally separate but **interest is calculated on the net consolidated balance**. No physical movement of funds. Used for tax + treasury efficiency where physical pooling has cross-border friction. Less common in US (regulatory friction); common in EU + UK + APAC.

### Virtual Account
A bookkeeping construct: one **physical master account** at the bank holds the funds, but the bank's CBS tracks per-virtual-account sub-balances. The customer perceives separate accounts (different account numbers, different reconciliation files). Common for fintech (sponsor-bank cosmos), law-firm escrow, property managers, marketplaces.

### Mandate (Corporate Signing)
Corporate authorisation rules:
- Single signer up to USD X.
- Dual signers up to USD Y.
- Board resolution required above USD Z.

The CBS or a separate signing-rules engine enforces.

---

## Operational Concepts

### Maker-Checker
Two-person rule for high-risk operations: maker enters, checker authorises. Standard in branch teller, wire initiation, loan disbursement. Configurable per limit, per channel, per customer segment.

### Limit Framework
Customer-level + product-level + channel-level limits (daily, per-transaction, cumulative). Modified by KYC tier, customer risk rating, and bilateral negotiation.

### Standing Instruction (SI)
Customer-pre-authorised recurring payment (e.g., monthly utility bill). Differs from a mandate (which is for direct debit by a third party) — SI is bank-side automation.

### Stop Payment
Customer instruction to refuse a specific pending payment (often a cheque). The CBS holds a flag; the payment engine checks the flag at posting time.

### Hold (Lien)
A constraint on the balance — funds in the account but not available. Sources:
- Cheque deposit hold (Reg CC in US).
- Court order / garnishment.
- AML investigation.
- Loan collateral (when the deposit secures a loan).

### Suspense Account
A holding account for items not yet posted to their final destination — failed payments, returned funds awaiting investigation, intra-bank breaks. Suspense balances are a top operational risk metric.

---

## Cross-References

- Settlement vs posting + finality concepts: [../06-payments/concepts.md](../06-payments/concepts.md)
- Specific CBS vendor positioning: [core-banking-systems.md](core-banking-systems.md)
- Retail product detail: [retail/](retail/)
- Wholesale product detail: [wholesale-corporate/](wholesale-corporate/)

---

## Open Questions

- [ ] Confirm bank's CIF model — single CIF for retail + corporate or separated.
- [ ] Confirm posting model — true online / real-time vs deferred batch per product type.
- [ ] Confirm dormancy + escheatment rules per jurisdiction.
- [ ] Confirm AA / ECR pricing framework per corporate customer segment.
- [ ] Confirm virtual-account product set if any (drives system requirements).
