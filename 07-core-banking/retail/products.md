# Retail Banking — Product Catalogue Overview

High-level catalogue of retail products with per-category links to detail files. Each product has a `product_class` code per [../taxonomy-detail.md](../taxonomy-detail.md).

---

## Deposits — see [deposits.md](deposits.md)

| Product | product_class | Description | Typical Geographies |
|---|---|---|---|
| Savings Account | `SavingsAccount` | Interest-bearing, on-demand | Global |
| Current / Checking | `CurrentAccount` (UK/IN) / `CheckingAccount` (US) | Transactional, low or no interest | Global |
| Fixed Deposit / CD | `FixedDeposit` / `CD` | Time-locked, fixed rate | Global; FD nomenclature in IN, CD in US |
| Recurring Deposit | `RecurringDeposit` | Monthly contributions to a TD | IN, MEA |
| Money Market Deposit | `MMDA` | Higher-yield, restricted withdrawals | US |
| ISA (Individual Savings Account) | `ISA` | Tax-advantaged savings | UK |
| Sparbuch / Tagesgeld | `SavingsAccount` variant | DE / AT consumer savings | DE, AT, CH |
| NRE / NRO / FCNR | `NRE`, `NRO`, `FCNR` | Non-Resident Indian deposit variants | IN |
| BSBDA | `BasicSavingsBankDepositAccount` | Financial inclusion zero-balance | IN |
| Joint / Minor / Trust | sub-class flags | Mandate-driven | Global |
| Escrow | `EscrowAccount` | Third-party-controlled holding | Global |

---

## Lending — see [lending.md](lending.md)

| Product | product_class | Description | Tenor |
|---|---|---|---|
| Home Loan / Mortgage | `HomeLoan` / `Mortgage` | Secured against residential property | 5–30 years |
| HELOC | `HELOC` | Revolving home-equity line of credit | Open-ended |
| Personal Loan | `PersonalLoan` | Unsecured | 1–7 years |
| Auto / Vehicle Loan | `AutoLoan` | Secured by vehicle | 3–7 years |
| Education / Student Loan | `EducationLoan` / `StudentLoan` | Tenor with deferral | 5–15 years |
| Credit Card (as credit product) | `CreditCard` | Revolving | Open-ended |
| Overdraft Facility | `OverdraftFacility` | Linked to current account | Renewable |
| Gold Loan | `GoldLoan` | Secured against gold | Short tenor; IN-specific |
| MSME / Small Business | `MSMELoan` / `SmallBusinessLoan` | Bridges retail to SME | Variable |
| Loan Against Property | `LAP` | Secured against property | Long tenor |
| BNPL | `BNPL` | Short-term, point-of-sale | < 12 months |

---

## Cards — see [cards.md](cards.md)

| Product | product_class | Description |
|---|---|---|
| Debit Card | `DebitCard` | Linked to deposit account |
| Credit Card | `CreditCard` | Revolving credit instrument |
| Prepaid Card | `PrepaidCard` | Pre-funded; gift / payroll / travel |
| Co-Brand Credit Card | `CoBrandCard` | Bank + brand partner |
| Commercial / Business Card | `BusinessCard` / `CommercialCard` | Issued to small business |
| Virtual Card | `VirtualCard` | Card number only; no plastic |
| Contactless | sub-flag | All card types, NFC-enabled |
| EMV chip + 3DS-enabled | mandatory | All modern cards |

---

## Digital Channels — see [digital-channels.md](digital-channels.md)

| Channel | Notes |
|---|---|
| Mobile Banking | Dominant channel; iOS + Android native + responsive web |
| Internet Banking | Browser-based; transitioning to mobile-first |
| IVR | Interactive Voice Response; supports basic enquiries + payments |
| Chatbot / Conversational AI | Increasingly LLM-augmented |
| WhatsApp Banking | IN, EM-strong |
| SMS Banking | Legacy; still present for lowest-tier connectivity |
| USSD | Feature-phone payments (IN: *99#, MEA equivalents) |

---

## Operations — see [operations.md](operations.md)

| Operation | Notes |
|---|---|
| Onboarding (eKYC, biometric, video KYC) | Aadhaar (IN), Driver's Licence (US), Photo ID (UK) |
| Branch / Teller | Cash, cheque, large value |
| ATM | Cash withdrawal, deposit (CDM), passbook update |
| Dispute Resolution | Reg E (US), PSRs (UK), MAS / RBI / PDPA equivalents |
| Dormant Account Management | Per-jurisdiction thresholds + escheatment |
| Deceased Customer Processing | Estate handling + survivor flow |
| Standing Instructions | Customer-side automation |
| Beneficiary Management | Pre-registered payees for faster + safer transfers |
| Locker / Safe Deposit Box | Physical product, declining usage |

---

## Cross-Product Concerns

### Pricing & Fee Schedules
Modern banks operate per-segment pricing matrices: same product, different fees per customer tier. The CBS / product master holds the matrix; channels surface the right tariff per customer.

### Cross-Sell & Bundling
Retail banking economics depend on cross-sell. A salary-account customer is targeted for: credit card, personal loan, insurance, mutual fund SIP, home loan. The CBS feeds eligibility data to a cross-sell engine.

### Customer Lifecycle Triggers
Life events (marriage, child, job change, retirement) drive product upgrade. Behavioural triggers (declined transaction, salary credit, large inbound transfer) drive contextual offers.

### Statement & Communications
Periodic statements (monthly, quarterly, annual), notifications (transaction, balance, due-date), customer-care correspondence. Statement formats: PDF, paper, push-notification, email. Regulatory disclosure requirements per jurisdiction.

---

## Open Questions

- [ ] Confirm full product catalogue for the bank.
- [ ] Confirm pricing matrix structure.
- [ ] Confirm cross-sell engine architecture.
- [ ] Confirm statement-of-account standards (paper retention, e-statement opt-in).
