# Wholesale / Corporate Banking

Wholesale / corporate banking serves **corporations, institutional clients, governments, and other banks**. This is the revenue engine of large universal banks — JPMC Treasury Services, BofA Global Transaction Services, Wells Wholesale Commercial Banking, Citi TTS, HSBC Global Banking & Markets transaction-banking arm — all multi-billion-USD revenue lines.

> Sub-domain: `WholesaleCorporate` (or split as `TreasuryServices` + `CorporateLending` + `TradeFinance` for tier-1 banks)
> Default sensitivity: `Confidential` (customer data, transaction data, pricing); `Restricted` for select deal-sensitive flows

---

## Navigation

| File | Purpose |
|---|---|
| [products.md](products.md) | Wholesale product catalogue overview |
| [treasury-services.md](treasury-services.md) | Cash management — Integrated Payables/Receivables, Lockbox, ARP, Positive Pay, ZBA, sweeps, virtual accounts, ECR/AA |
| [corporate-lending.md](corporate-lending.md) | Working capital, term loans, syndicated loans, ABL, project finance |
| [trade-finance.md](trade-finance.md) | LC, SBLC, Documentary Collections, Open Account, SCF, BG, UCP 600, MT 7-series |
| [cash-management.md](cash-management.md) | Liquidity products — pooling, sweeps, virtual accounts at depth |
| [corporate-channels.md](corporate-channels.md) | Channels — ACCESS/CashPro/CEO/CitiDirect/HSBCnet, H2H, S4C, APIs, ERP integration |
| [customer-segments.md](customer-segments.md) | SME, Mid-cap, Large Corp, FIG, MNC, Sovereign / Public Sector, NBFI |

---

## Why Wholesale Differs Sharply From Retail

| Dimension | Retail | Wholesale |
|---|---|---|
| Customer count | Millions | Thousands–hundreds of thousands |
| Onboarding | Self-service in minutes | Relationship-managed, weeks |
| Pricing | Standard tariff | Negotiated, per-customer matrices |
| KYC depth | Personal ID | KYB — entity structure, UBOs, financials, regulatory licences |
| Channels | Mobile, internet, branch | ACCESS / CashPro / CEO / CitiDirect portals, H2H file, S4C, API, ERP |
| Products | Standardised, configurable | Bespoke, structured, often multi-product packages |
| Decision-maker | Individual | Treasurer / CFO / multi-stakeholder |
| Sales | Mass-market + cross-sell | Relationship Manager + product specialists |
| SLA | Customer-self-help | Dedicated client service, response SLAs |
| Disputes | Reg E / PSRs / consumer rules | Per-contract; bilateral |
| Risk profile | Credit risk (lending) + operational | Counterparty credit + concentration + reputation |

---

## Revenue Model

| Source | Description |
|---|---|
| **NIM on lending book** | Term loans, working capital, trade finance, project finance |
| **Fee income — Transaction Banking** | Per-payment, per-LC, per-collection, per-statement |
| **Fee income — Cash Management** | Lockbox, ARP, virtual account, positive pay, pooling |
| **Fee income — Custody / Securities Services** | Where bank also runs custody (JPMC, BNY, State Street) |
| **FX margin on corporate flows** | Spread on multi-currency conversion |
| **Earnings Credit Rate (ECR)** | Customer maintains balances; bank funds itself + offsets explicit fees |
| **Trade margin** | LC commission, confirmation fee, advising fee, negotiation fee |
| **Wealth + Investment Banking cross-sell** | Capital markets revenue from corporate clients |

Transaction-banking revenue at JPMC TS / BofA GTS / Citi TTS is **~10–15% of group revenue** at each of those banks — material, sticky, and counter-cyclical.

---

## Customer Segmentation

Segmentation drives product, channel, pricing, and relationship model:

### SME (Small & Medium Enterprise)
- Revenue often < USD 50M (varies sharply by bank).
- Standardised products + simplified pricing.
- Digital channels dominant; relationship-light.
- Cross-sell from retail platform common.

### Middle Market / Mid-Corp
- Revenue USD 50M–USD 1B.
- Mix of standardised + bespoke products.
- Dedicated Relationship Manager.
- Multi-product cross-sell.

### Large Corporate / Corporate Banking
- Revenue > USD 1B.
- Bespoke products + multi-product packages.
- Senior Relationship Manager + product specialists.
- Multi-banking relationships standard.

### Multinational Corporate (MNC)
- Multi-country operations.
- Group-wide cash management.
- Multi-currency liquidity products.
- Cross-border + multi-jurisdiction compliance.
- Centralised / decentralised treasury models.

### FIG — Financial Institutions Group
- Other banks, insurance, asset managers, central counterparties.
- Correspondent banking + custody + securities services.
- Wolfsberg CBDDQ + enhanced diligence.

### Sovereign / Public Sector
- Governments, central banks, multilateral institutions.
- High-trust, low-margin, strategically important.
- Specific compliance overlays.

### NBFI — Non-Bank Financial Institution
- Fintechs, MSBs (Money Service Businesses), broker-dealers, fund administrators, payment processors.
- Heightened risk profile (especially MSB sub-segment).
- Enhanced AML + sanctions diligence.

---

## Sales + Coverage Model

- **Relationship Manager (RM)** — owns the customer relationship.
- **Product Specialists** — Cash Mgmt, Trade Finance, Lending, Capital Markets.
- **Coverage Banker** — for capital-markets-heavy clients.
- **Treasury Sales** — for cash-management-heavy clients.
- **Operations / Customer Service** — implementation + ongoing servicing.

The RM is the customer's primary contact; product specialists join for deep product conversations. Implementation teams onboard, operations service.

---

## Onboarding (KYB)

Far more complex than retail KYC:
- Entity legal structure (parent, subsidiaries, branches).
- UBO identification (often multiple levels of ownership).
- Regulatory licences (if FIG / payment institution).
- Financial statements (typically 2–3 years).
- Tax residency + treaty status.
- Sanctions + adverse media on each entity + UBO.
- PEP screen on UBOs + key principals.
- Industry / sector risk.
- Country risk.
- Wolfsberg CBDDQ (for FIG clients).
- Periodic refresh (annual for high-risk; 3–5 yearly for standard).

Onboarding can take **weeks to months** for a complex MNC client.

---

## Operational SLAs

| Service | Typical SLA |
|---|---|
| Wire investigation response | 24 hours (gpi-tracker) to 5 business days |
| Trade Finance LC issuance | 1–3 business days post-document |
| Lockbox same-day credit | T+0 to T+1 |
| New account setup | 5–15 business days |
| Customer service response | 4–24 business hours |

---

## Regulatory Lens for Wholesale

| Regime | Examples |
|---|---|
| US | BSA, FinCEN, OFAC, Reg J (FedWire), NACHA (ACH), FATCA, state MTL (for non-bank PSP clients) |
| UK | PSRs 2017, MLRs, FCA / PRA conduct + prudential, Consumer Duty (where small business intersects retail) |
| EU | PSD2 → PSD3 / PSR, IPR, EU AML Package, DORA, MiCA |
| India | RBI Master Directions, FEMA (for cross-border), GST integration |
| Cross-border | FATF, BIS, Wolfsberg correspondent banking, sanctions multi-regime |

Prudential dominates over consumer protection — Basel III risk-weighting on the lending book, large-exposures rules, leverage ratio.

---

## Open Questions

- [ ] Confirm segmentation thresholds for the bank.
- [ ] Confirm channel mix per segment.
- [ ] Confirm CBS instance(s) supporting wholesale vs retail.
- [ ] Confirm trade finance + cash management product set in scope.
- [ ] Confirm whether the bank treats Treasury Services + Trade Finance as separate sub-domains organisationally.
