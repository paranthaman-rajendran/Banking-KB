# Corporate Lending

The asset side of wholesale banking. Term loans, working capital, syndicated facilities, asset-based lending, project finance. Generates NIM + structuring fees + ongoing facility fees.

> Companion: [trade-finance.md](trade-finance.md) for trade-related lending; [../concepts.md](../concepts.md) for NPL classification, IFRS 9 / CECL.

---

## Working Capital Facilities

Short-term financing for day-to-day operations. Renewable annually.

### Variants

| Variant | Description |
|---|---|
| **Overdraft (OD)** | Pre-authorised borrowing on operating account |
| **Cash Credit (IN)** | Working capital limit secured by inventory + receivables |
| **Revolving Credit Facility (RCF)** | Multi-draw revolving limit |
| **Packing Credit (Pre-shipment Finance)** | Pre-shipment working capital for exporters |
| **Post-Shipment Finance** | Bridge between shipment + payment from buyer |
| **Bill Discounting / Negotiation** | Receivables conversion to cash |
| **Letter of Credit-backed Financing** | Financing against LC proceeds |
| **Demand Loan** | Repayable on demand; secured |

### Pricing
- Floating rate (MCLR / EBLR / SOFR / SONIA + spread).
- Per-draw vs per-day interest computation.
- Commitment fee on unused portion of RCF.
- Renewal fee annually.

---

## Term Loans

Fixed-tenor debt for capital expenditure, acquisition, or refinancing.

### Variants

| Variant | Description |
|---|---|
| **Bullet** | Full principal at maturity |
| **EMI / Equated** | Equal periodic principal + interest |
| **Balloon** | Small periodic + large maturity |
| **Custom Amortisation** | Structured per cashflow |
| **Bridge Loan** | Short-term interim |
| **Mezzanine** | Subordinated junior debt; often with equity warrant |

### Pricing
- Fixed or floating.
- Spread over benchmark.
- Step-up / step-down per schedule.
- Pricing flex per market conditions during syndication.

---

## Syndicated Loans

Multi-lender facility. Lead arranger / agent bank syndicates to participants.

### Roles

| Role | Description |
|---|---|
| **Mandated Lead Arranger (MLA)** | Originates + structures |
| **Bookrunner** | Manages syndication process |
| **Agent Bank** | Administers throughout life |
| **Security Trustee** | Holds collateral on behalf of lenders |
| **Participants** | Take portions of the facility |

### Process
1. Mandate from borrower.
2. Information memorandum (IM) prepared.
3. Syndication launched to potential lenders.
4. Allocations finalised.
5. Documentation closed.
6. Drawdown.
7. Ongoing administration (interest, principal, info-reporting, waivers).

### Why It Matters
- Spreads risk across lenders.
- Allows very large facilities (USD 1B+).
- Generates structuring + arrangement fees.

### Vendor Platforms
- **Loan IQ** (Finastra) — commercial loan servicing dominant in syndicated.
- **ACBS** (FIS) — alternative.
- **Bank-built** at largest tier-1.

---

## Asset-Based Lending (ABL)

Lending secured by **specific asset pools**, typically receivables + inventory. Borrowing base calculated periodically.

### How It Works
- Borrowing base = % of eligible receivables + % of eligible inventory.
- Periodic (often monthly) reporting from borrower; bank revalues.
- Revolver structure — borrower draws against base.
- Eligibility criteria (age, concentration, dispute-status of receivables).

### Use Cases
- Manufacturers + distributors with working-capital needs.
- Cyclical businesses (seasonal swings).
- Sub-investment-grade borrowers where unsecured lending is unavailable.

---

## Equipment Finance & Leasing

| Type | Description |
|---|---|
| **Equipment Loan** | Secured by equipment; ownership with borrower |
| **Finance Lease** | Lessee bears risk + reward; substance is purchase |
| **Operating Lease** | Lessor bears risk + reward; substance is rental |
| **Hire Purchase** | Hybrid; ownership transfers at end |
| **Sale-and-Leaseback** | Owner sells then leases back; releases capital |

Accounting: IFRS 16 + ASC 842 converged most leases onto the balance sheet from 2019.

---

## Project Finance

Long-tenor (10–30 year) lending where repayment comes from **project cashflows**, not corporate balance sheet.

### Structure
- Special Purpose Vehicle (SPV) borrows.
- Construction phase: bank or syndicate funds the build.
- Operations phase: cashflow services debt.
- Non-recourse to sponsors (or limited recourse).

### Sectors
- Infrastructure (toll roads, ports, airports).
- Energy (oil + gas, renewables, power plants).
- Mining + resources.
- Telecom.

### Documentation
Extensive: facility agreement, common terms agreement, security package (assignment of project agreements, share pledge, account pledge), inter-creditor agreement, sponsor support.

---

## Commercial Real Estate (CRE)

Loans secured by commercial property.

### Variants
- **Office, retail, industrial, multi-family, hospitality**.
- **Construction loan** — funds the build.
- **Permanent loan** — refinances construction.
- **Bridge loan** — interim.
- **Mezzanine** — subordinated.

### Risk Concerns
- LTV + DSCR (Debt Service Coverage Ratio).
- Sector concentration.
- Geographic concentration.
- Tenant quality + rollover risk.

---

## Leveraged & Acquisition Finance

| Type | Description |
|---|---|
| **Leveraged Loan** | High-leverage loan to non-IG borrower |
| **LBO Loan** | Funds the leveraged buyout |
| **Acquisition Finance** | Funds corporate acquisition |
| **Unitranche** | Single facility blending senior + mezzanine |

Often sold down to institutional investors post-close.

---

## Loan Lifecycle

### 1. Origination
- Mandate from client.
- Credit analysis (financials, projections, industry, management).
- Internal credit committee approval.
- Term sheet.
- Documentation drafting.
- Closing.

### 2. Disbursement
- Conditions precedent satisfied.
- Drawdown notice from borrower.
- Funds released.
- Security perfected.

### 3. Servicing
- Periodic interest + principal.
- Covenant monitoring (financial + non-financial).
- Drawdowns / repayments on revolvers.
- Waivers + amendments.
- Information reporting.

### 4. Monitoring
- Quarterly / annual financial review.
- Covenant compliance reports.
- Watchlist monitoring for stressed credits.
- Industry / macro updates.

### 5. Workout / Recovery
- Distressed credits restructured or wound down.
- Special Assets Group involvement.
- Legal enforcement if needed.

---

## Loan Origination & Servicing Systems

| System | Vendor | Use |
|---|---|---|
| **nCino** | nCino (Salesforce-based) | Modern origination, increasingly tier-1 |
| **FIS ACBS** | FIS | Loan servicing, commercial |
| **Finastra Loan IQ** | Finastra | Syndicated loans dominant |
| **Oracle Banking Corporate Lending** | Oracle | OBS-suite member |
| **Temenos T24 Lending** | Temenos | T24-integrated |
| **Pega Loan Origination** | Pega | Customer-built on Pega platform |
| **TCS BaNCS Corporate Lending** | TCS | BaNCS suite |
| **Bank-built** | Internal | Common at very large banks |

---

## Risk Lens

### Credit Risk
- **PD (Probability of Default)** — per borrower rating.
- **LGD (Loss Given Default)** — recovery expected.
- **EAD (Exposure at Default)** — drawn + undrawn.
- **Expected Loss** = PD × LGD × EAD.

### Provisioning
- **IFRS 9 Stage 1 / 2 / 3** based on SICR.
- **CECL** (US) — life-of-loan expected loss.
- Bank's risk engine computes; CBS provides loan data.

### Concentration Risk
- **Large Exposures** — regulatory limit per single counterparty (~25% of Tier 1 capital).
- **Sector concentration** — internal monitoring + limits.
- **Geographic concentration** — internal monitoring + limits.

### Counterparty Risk
- Internal rating model.
- External ratings (S&P, Moody's, Fitch, CRISIL, etc.).
- Watch + stress override.

---

## Documentation

| Document | Purpose |
|---|---|
| **Term Sheet** | Outline terms; binding intent |
| **Facility Agreement / Loan Agreement** | Master legal document |
| **Common Terms Agreement** | Multi-facility shared terms |
| **Security Documents** | Mortgage, charge, assignment, share pledge |
| **Guarantee** | Third-party guarantee |
| **Inter-Creditor Agreement** | When multiple lender classes |
| **Sponsor Support** | Project finance contributions |
| **Disclosure Letter** | Updates to representations |
| **Conditions Precedent** | Conditions for first drawdown |

Standards bodies:
- **LMA (Loan Market Association)** — EU standard.
- **LSTA (Loan Syndications and Trading Association)** — US standard.
- **APLMA** — Asia-Pacific.

---

## Open Questions

- [ ] Confirm bank's lending product catalogue + risk policy.
- [ ] Confirm LOS architecture (per product type).
- [ ] Confirm syndicated loan platform (Loan IQ most common).
- [ ] Confirm Watchlist + workout process.
- [ ] Confirm IFRS 9 / CECL provisioning model and risk engine.
