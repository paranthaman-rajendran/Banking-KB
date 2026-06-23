# Retail Lending

Retail lending products. The lending book is **the bank's primary asset**, generating most of the NIM. Risk-weighted by Basel III; provisioned per IFRS 9 / CECL.

> Companion: [../concepts.md](../concepts.md) for amortisation, NPL classification, ECL provisioning.

---

## Home Loan / Mortgage (`HomeLoan` / `Mortgage`)

The dominant retail lending product by volume.

| Feature | Typical Setting |
|---|---|
| Purpose | Purchase, construction, refinancing |
| Security | First-lien mortgage on the property |
| Tenor | 5–30 years (commonly 20–25) |
| LTV | 75–90% (regulatory caps; LTV varies by jurisdiction + property type) |
| Rate | Fixed / floating / hybrid; floating linked to MCLR / EBLR / SOFR / SONIA |
| Repayment | EMI (Equated Monthly Instalment); pre-EMI for under-construction |
| Prepayment | Allowed; some lenders charge fee on fixed-rate prepayment |
| Disbursement | Lump-sum or stage-wise (construction-linked) |
| Tax benefit | Common (interest deductible; principal under specific provisions) |

### Variants
- **Purchase** — standard new-home purchase loan.
- **Construction** — disbursed in stages against build progress.
- **Plot + Construction** — combined land + build.
- **Top-up** — existing customer borrowing more against rising property value.
- **Balance Transfer** — refinance from another lender at lower rate.
- **Reverse Mortgage** — borrow against home equity; repay at sale / inheritance; senior-citizen product.

### US-Specific
- **Conforming vs Jumbo** — conforming meets Fannie Mae / Freddie Mac limits; jumbo exceeds.
- **FHA / VA Loans** — government-guaranteed.
- **30-year Fixed-Rate** — dominant US product structure.
- **ARM (Adjustable-Rate Mortgage)** — periodic reset against benchmark.

### UK-Specific
- **Help to Buy** (closing / closed schemes) — government-supported.
- **Buy-to-Let** — rental property mortgage.
- **Interest-Only** — pay interest only; repay principal at maturity.
- **Lifetime Mortgage** — equity release.

---

## HELOC (US) (`HELOC`)

Revolving credit line secured by home equity. Customer draws as needed; pays interest only on drawn balance.

| Feature | Typical Setting |
|---|---|
| Tenor | Draw period (5–10 years) + repayment period (10–20 years) |
| Rate | Variable, linked to prime |
| Min draw | Often USD 5,000 or 10,000 |
| Annual fee | Often USD 50–150 |

---

## Personal Loan (`PersonalLoan`)

Unsecured, fixed-tenor lending for general purposes.

| Feature | Typical Setting |
|---|---|
| Purpose | Wedding, medical, debt consolidation, travel |
| Security | Unsecured |
| Tenor | 1–7 years |
| Rate | Higher than secured (typically 10–22% in IN; 6–24% in US) |
| Amount | USD 1k–50k (US); INR 10k–25L (IN); GBP 1k–50k (UK) |
| Repayment | EMI |
| Prepayment | Often allowed without penalty |
| Approval | Increasingly instant via digital channels with AI-driven underwriting |

---

## Auto Loan (`AutoLoan`)

Secured by the vehicle.

| Feature | Typical Setting |
|---|---|
| Purpose | New / used vehicle purchase |
| Security | First-lien on the vehicle |
| Tenor | 3–7 years |
| LTV | 80–95% |
| Rate | Lower than personal loan due to security |
| Repayment | EMI |
| Insurance | Often mandatory comprehensive cover (assigned to bank) |

### Variants
- **New Car** — preferred terms.
- **Used Car** — shorter tenor, higher rate; vehicle age limit.
- **Lease** — leasing alternative.
- **EV-specific** — sometimes preferential rates.

---

## Education Loan / Student Loan (`EducationLoan` / `StudentLoan`)

| Feature | Typical Setting |
|---|---|
| Purpose | Tuition + living expenses + travel |
| Security | Often unsecured up to threshold; collateral above |
| Tenor | 5–15 years incl. moratorium |
| Moratorium | During course + grace period (typically 1 year post-completion) |
| Rate | Government-subsidised in some jurisdictions |
| Disbursement | Per semester / tranche |
| Co-signer | Parent / guardian common |

### US-Specific
- **Federal Student Loans** — government-issued (Stafford, PLUS); separate from private bank loans.
- **Income-Driven Repayment** — federal-loan repayment based on income.
- **Refinance + Consolidation** — private market.

---

## Credit Card (as a credit product) (`CreditCard`)

The card itself is a payment instrument; the **credit line** is the lending product.

| Feature | Typical Setting |
|---|---|
| Credit limit | Set per customer based on income + credit score |
| APR | Typically 18–40%; varies sharply by jurisdiction + risk segment |
| Grace period | 21–55 days from statement to due date (interest-free if paid in full) |
| Minimum payment | Typically 5% of outstanding or fixed minimum |
| Late fee | Capped in some jurisdictions (UK / EU consumer rules) |
| Reward / cashback | Significant value; co-brand drives loyalty |
| Balance transfer | Promotional rates for transfers from other lenders |
| Cash advance | High APR + no grace period |

See [cards.md](cards.md) for the card-payment side.

---

## Overdraft Facility (`OverdraftFacility`)

Pre-authorised borrowing on a current account.

| Feature | Typical Setting |
|---|---|
| Limit | Set per customer |
| Rate | Daily on the utilised amount |
| Authorisation | Pre-arranged (clean) vs unarranged (penalty rate) |
| Auto-renewal | Annual review typical |

### Sub-Variants
- **Salary OD** — limit linked to salary multiple.
- **OD against FD** — secured against own FD; favourable rate.
- **OD against securities** — secured against mutual fund / equity holdings.

---

## Gold Loan (`GoldLoan`) — IN

Secured against gold ornaments. Volume-heavy in India.

| Feature | Typical Setting |
|---|---|
| LTV | 75% cap (RBI rule for banks) |
| Tenor | Short (3–12 months); rollable |
| Rate | Below personal loan; above mortgage |
| Process | In-branch valuation + physical safekeeping |
| Default handling | Auction of gold |

---

## MSME / Small Business Loan (`MSMELoan` / `SmallBusinessLoan`)

Bridges retail to commercial banking.

| Feature | Typical Setting |
|---|---|
| Purpose | Working capital, machinery, business expansion |
| Security | Often partial collateral + personal guarantee |
| Tenor | 1–10 years |
| Rate | Mid-tier (below personal, above mortgage) |
| Underwriting | Bank statement-based + financials + GST returns (IN) |
| Government scheme | Often eligible for govt guarantee (CGTMSE in IN, SBA in US) |

---

## Loan Against Property (`LAP`)

Secured against owned property (not for purchase of property — for general use against existing property collateral).

| Feature | Typical Setting |
|---|---|
| Purpose | Business / personal large-ticket |
| Tenor | 5–15 years |
| LTV | 50–70% |
| Rate | Between home loan and personal loan |

---

## Buy Now Pay Later (`BNPL`)

Short-term, point-of-sale.

| Feature | Typical Setting |
|---|---|
| Tenor | Pay-in-4 (4 instalments over 6 weeks) or 3–12 months |
| Interest | Often 0% for the customer; merchant pays MDR |
| Underwriting | Soft-pull credit decision in seconds |
| Default | Increasingly regulated as credit product (UK FCA, US CFPB Reg Z) |

---

## Loan Lifecycle Stages

1. **Origination** — customer enquiry, eligibility check, document collection, underwriting, sanction.
2. **Disbursement** — funds released; collateral perfected (mortgage registered).
3. **Servicing** — EMI collection, interest accrual, statement generation, customer servicing.
4. **Collections** — overdue follow-up; bucket-1 (0–30 days), bucket-2 (30–60), bucket-3 (60–90), NPA (90+).
5. **Recovery / Restructuring / Settlement** — workout for stressed accounts.
6. **Closure** — final settlement; collateral release.

The CBS supports stages 2–4 + 6. Origination is often a **separate Loan Origination System (LOS)** — Salesforce nCino, Pega, Encompass, FIS Loan Origination, or bank-built. Collections often a **separate collections system** — TCS BaNCS Collections, FIS Recovery, NICE Actimize Collections, FICO TONBELLER.

---

## Risk + Provisioning

| Stage | Trigger | Provisioning |
|---|---|---|
| Standard | Current | Standard rate (~0.25–0.4% in IN per RBI) |
| SMA-0 | 1–30 days overdue | Standard |
| SMA-1 | 31–60 days overdue | Watch list |
| SMA-2 | 61–90 days overdue | Higher provisioning |
| Substandard | > 90 days | 15–20% provisioning |
| Doubtful | Longer duration | Higher provisioning per matrix |
| Loss | Identified | 100% provisioning |

IFRS 9 introduces **Stage 1 / 2 / 3** classification based on **significant increase in credit risk (SICR)** — forward-looking, not just past-due-based.

US CECL is similar in spirit (forward-looking ECL at origination), different mechanics.

---

## Pricing Models

| Model | Description |
|---|---|
| **Risk-based pricing** | Rate depends on credit score, debt-to-income, LTV |
| **Bundled pricing** | Discounted rate if customer holds other products |
| **Promotional pricing** | Limited-period offers (festival, new customer) |
| **Floating benchmark** | Rate = benchmark + spread; benchmark = MCLR / EBLR (IN), SOFR (US), SONIA (UK) |
| **Step-up / step-down** | Schedule-defined changes |

---

## Open Questions

- [ ] Confirm bank's lending product catalogue + risk policies.
- [ ] Confirm LOS architecture (separate vs CBS-integrated).
- [ ] Confirm collections system + bucket framework.
- [ ] Confirm pricing + benchmark + spread framework per product.
- [ ] Confirm IFRS 9 / CECL provisioning model and risk engine.
