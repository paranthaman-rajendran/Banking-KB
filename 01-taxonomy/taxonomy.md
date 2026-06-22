# Domain Taxonomy

The top-level routing layer for every document, chunk, and retrieval request. This taxonomy is the single source of truth for the `domain` and `sub_domain` metadata fields.

> **Phase 1 deliverable.** Review with capital markets desks and compliance before approval.

---

## Full Tree

```
Banking Knowledge Base
│
├── Retail Banking
│   ├── Deposits (Savings, FD, RD, NRI)
│   ├── Lending & Credit (Home Loan, Personal, Auto, MSME)
│   └── Cards (Credit, Debit, Prepaid)
│
├── Payments
│   ├── Domestic (NEFT, RTGS, IMPS, UPI)
│   ├── Cross-Border (SWIFT, SEPA, ACH, RippleNet)
│   └── Real-Time Rails
│
├── Capital Markets                        ← PRIMARY DOMAIN
│   ├── Equities
│   │   ├── Cash Equities
│   │   ├── Equity Derivatives (Options, Futures, Warrants)
│   │   └── Equity Structured Products
│   │
│   ├── Fixed Income
│   │   ├── Government Bonds (G-Sec, T-Bills, Gilts)
│   │   ├── Corporate Bonds (IG, HY, Perpetual)
│   │   ├── Covered Bonds & ABS
│   │   ├── Securitization (MBS, CDO, CLO)
│   │   └── Fixed Income Derivatives (IRS, CDS, Swaptions)
│   │
│   ├── FX & Rates
│   │   ├── FX Spot, Forwards, Swaps, Options
│   │   ├── Interest Rate Swaps & Basis Swaps
│   │   └── Cross-Currency Basis Swaps
│   │
│   ├── Commodities
│   │   ├── Energy (Oil, Gas, Power)
│   │   ├── Metals & Mining
│   │   └── Agricultural
│   │
│   ├── Structured Products              ← PILOT SUB-DOMAIN
│   │   ├── Principal Protected Notes
│   │   ├── Autocallables & Barrier Products
│   │   ├── CLNs & TRS
│   │   └── Exotic Payoffs
│   │
│   └── Prime Brokerage
│       ├── Margin & Collateral
│       ├── Securities Lending
│       └── Synthetic Products
│
├── Treasury & ALM
│   ├── Liquidity Management
│   ├── Asset-Liability Management
│   └── Capital Planning
│
├── Wealth Management
│   ├── Portfolio Management
│   ├── Advisory & Planning
│   └── Alternative Investments
│
├── Risk Management
│   ├── Market Risk (VaR, PnL Explain, Greeks)
│   ├── Credit Risk (PD, LGD, EAD, IFRS 9)
│   ├── Liquidity Risk (LCR, NSFR)
│   ├── Operational Risk
│   └── Counterparty Credit Risk (CVA, DVA, XVA)
│
├── Compliance & Regulatory
│   ├── KYC / KYB / CDD
│   ├── AML & Sanctions Screening
│   ├── MiFID II / MiFIR (EU)
│   ├── Dodd-Frank / EMIR (OTC Derivatives)
│   ├── Basel III / IV (Capital)
│   ├── SEBI / RBI (India)
│   ├── SEC / FINRA (US)
│   └── IOSCO Standards
│
└── Technology Platform
    ├── Core Banking Systems
    ├── Market Data (Bloomberg, Refinitiv, ICE)
    ├── Order Management (OMS/EMS)
    ├── Risk Engines (Murex, Calypso, Finastra)
    ├── APIs & Integration Layer
    └── Data Warehouse & Lakehouse
```

---

## Canonical Domain Codes (for `domain` metadata)

| Code | Display Name |
|---|---|
| `RetailBanking` | Retail Banking |
| `Payments` | Payments |
| `CapitalMarkets` | Capital Markets |
| `TreasuryALM` | Treasury & ALM |
| `WealthManagement` | Wealth Management |
| `Risk` | Risk Management |
| `Compliance` | Compliance & Regulatory |
| `TechPlatform` | Technology Platform |

## Capital Markets Sub-domain Codes (for `sub_domain`)

| Code | Display Name |
|---|---|
| `Equities` | Equities |
| `FixedIncome` | Fixed Income |
| `FXRates` | FX & Rates |
| `Commodities` | Commodities |
| `StructuredProducts` | Structured Products |
| `PrimeBrokerage` | Prime Brokerage |

---

## Maintenance Rules

1. **Taxonomy is owned by the Domain Council** — adds, renames, and deletions require Council approval.
2. **Codes are immutable** — display names can change, codes cannot. Re-tagging breaks lineage.
3. **Every chunk MUST carry both `domain` and `sub_domain`** — no defaults, no nulls.
4. **`product_class` is a free-tagged third level** — see [metadata-schema.md](metadata-schema.md). New product classes do not require taxonomy changes.
