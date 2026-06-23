# Retail Deposits

Deposit products are the **funding base** of a retail bank — low-cost (often zero-interest) demand deposits + higher-cost time deposits. The CASA ratio is a top management metric.

> Companion: [../concepts.md](../concepts.md) for CASA, demand vs time, dormancy concepts.

---

## Savings Account (`SavingsAccount`)

The workhorse retail deposit. Interest-bearing, on-demand, transactional but typically with limited free transactions per month.

| Feature | Typical Setting |
|---|---|
| Interest rate | Tiered by balance; market-driven; often 0.5–4% in normal-rate environments |
| Minimum balance | Often a threshold below which fees apply; zero-balance variants for inclusion (BSBDA in IN) |
| Free transactions | Typically 25–50 free credit / debit per month |
| Statement | Monthly e-statement standard; paper on request (sometimes chargeable) |
| Online + mobile | Universal |
| Debit card link | Universal |
| Cheque book | Often optional / on-request |
| Sweep-in / Sweep-out | Often configurable — sweeps surplus to FD |
| Joint / Minor | Per mandate framework |
| Nomination | Standard in most jurisdictions; mandatory in some (IN) |

### Variants
- **Premium / Priority Savings** — higher minimum balance, premium rate, dedicated relationship manager.
- **Salary Account** — minimum-balance waiver for payroll customers.
- **Senior Citizen Savings** — uplift on rate; simplified channels.
- **Minor / Youth Account** — restricted operations; parent / guardian co-signed.
- **Basic Savings (BSBDA, IN)** — zero-balance, restricted transactions; financial inclusion.

---

## Current Account / Checking Account (`CurrentAccount` / `CheckingAccount`)

Transactional account, non-interest-bearing (in most jurisdictions; some EU pay token interest). Heavy on cheque + transfer activity.

| Feature | Typical Setting |
|---|---|
| Interest | Usually zero (banks may pay marginal rate or "earnings credit" in commercial variants) |
| Minimum balance | Typically higher than savings; fees if below |
| Free transactions | Higher allowance than savings, sometimes unlimited above threshold |
| Cheque book | Standard |
| Overdraft | Often available (linked OD line) |
| Direct debit | Standard for utility / mandate-based |
| Standing instruction | Standard |
| Statement | Often monthly or on-demand |

### Variants
- **Personal Checking (US)** — most common consumer checking.
- **Premium Checking** — fee waivers + reward features.
- **NRI Current** (IN) — NRE/NRO/FCNR variants.
- **Salary Current** — for sole traders, gig workers.

---

## Fixed Deposit / Certificate of Deposit (`FixedDeposit` / `CD`)

Time deposit at fixed rate for fixed tenor.

| Feature | Typical Setting |
|---|---|
| Tenor | 7 days to 10 years |
| Rate | Fixed at booking; tiered by tenor + amount + customer segment |
| Interest payout | Quarterly / half-yearly / yearly / cumulative (paid at maturity) |
| Premature withdrawal | Penalty rate, typically -0.5% to -1% on actual tenor |
| Auto-renewal | Common — renew at then-prevailing rate or specified instruction |
| Loan against FD | Common — facility against the deposit collateral |
| Senior citizen uplift | +0.25 to +0.5% typically |
| Tax treatment | TDS on interest above threshold (IN); 1099-INT (US); ISA shelters in UK |

### Variants
- **Tax-Saver FD (IN)** — 5-year lock; tax deduction under section 80C.
- **Cumulative vs Non-cumulative** — interest paid out periodically vs reinvested.
- **Floating-rate CD** — rate linked to a benchmark.
- **Step-up CD** — rate increases at defined points.
- **No-penalty CD** — premature withdrawal without penalty (rate trade-off).
- **Brokered CD (US)** — sold through brokerages; secondary market exists.

---

## Recurring Deposit (`RecurringDeposit`)

IN / MEA / parts of APAC. Monthly contribution into a time deposit.

| Feature | Typical Setting |
|---|---|
| Tenor | 6 months to 10 years |
| Rate | Same as FD of equivalent tenor |
| Monthly contribution | Fixed amount; SI from CASA |
| Missed instalment | Penalty; sometimes auto-debit from linked account |
| Premature closure | Penalty on rate |

---

## Money Market Deposit Account (MMDA, US) (`MMDA`)

US-specific high-yield deposit with limited transaction count.

| Feature | Typical Setting |
|---|---|
| Interest | Higher than standard savings, market-linked |
| Min balance | Typically higher than savings |
| Transactions | Limited per month (pre-2020 Reg D rule abolished; many banks retain) |

---

## ISA (Individual Savings Account, UK) (`ISA`)

UK tax-advantaged wrapper. Variants: Cash ISA, Stocks & Shares ISA, Lifetime ISA, Junior ISA.

| Feature | Typical Setting |
|---|---|
| Annual allowance | Set by HMT (currently GBP 20,000 total across ISA types; verify current) |
| Tax | Interest + capital gains tax-free within the wrapper |
| Withdrawal | Free for Cash ISA; restrictions on Lifetime ISA |
| Tracking | Bank reports balances to HMRC |

---

## NRI Variants (India) — NRE / NRO / FCNR

| Variant | Currency | Repatriability | Interest Taxable? |
|---|---|---|---|
| NRE | INR | Freely repatriable | No (tax-free in IN) |
| NRO | INR | Restricted (USD 1M annual cap) | Yes |
| FCNR | Foreign currency (USD/GBP/EUR/etc.) | Freely repatriable | No (in IN) |

Critical for NRI customers; FEMA regulations govern. Wrong product mapping has tax + repatriation implications.

---

## Account Operations

### Account Opening
- Identification + verification.
- KYC + sanctions + PEP screening.
- Risk rating assignment.
- Welcome kit (cheque book, debit card, mobile activation).

### Activation
First customer-initiated transaction. Customer-activation rate within 30/60/90 days is a top KPI.

### Maintenance
- Statement generation.
- Interest accrual + crediting.
- Fee accrual + posting.
- Nominee + beneficiary updates.
- Address + contact updates.
- Mandate changes.
- Account holder additions / removals.

### Dormancy & Inactive Account
- **Dormant** — no customer-initiated transaction for defined period (e.g., 2 years in IN; varies elsewhere).
- **Inactive** — first-stage marker, often shorter window.
- Reactivation requires customer presence + ID verification.

### Closure
- Customer-initiated (with outstanding-balance settlement).
- Bank-initiated (AML, fraud, non-compliance, dormancy + escheatment threshold reached).
- Anti-tipping if AML-driven (cannot tell customer the AML reason).

### Escheatment / Unclaimed Property
- Long-dormant balances handed over to regulator's unclaimed-property regime.
- **IN**: DEAF Fund (Depositor Education and Awareness Fund) at RBI.
- **US**: State-level unclaimed property programmes; reporting per state law.
- **UK**: Reclaim Fund / Dormant Asset Scheme.

---

## CBS Implementation Notes

The CBS manages:
- Product master per deposit type.
- Per-account interest accrual model.
- Daily accrual + periodic (monthly / quarterly) crediting.
- Cut-off + EOD posting.
- Fee schedule application.
- Dormancy state machine.
- Statement generation queue.

Common batch jobs:
- Daily: interest accrual, fee accrual, balance reporting.
- Monthly: interest credit, fee crediting, statement generation.
- Quarterly: regulatory reporting.
- Annual: 1099-INT / tax-form generation (US); FATCA / CRS extracts.

---

## Open Questions

- [ ] Confirm full deposit product catalogue.
- [ ] Confirm dormancy + escheatment thresholds per jurisdiction.
- [ ] Confirm interest accrual basis per product.
- [ ] Confirm cross-jurisdictional tax-reporting integration.
