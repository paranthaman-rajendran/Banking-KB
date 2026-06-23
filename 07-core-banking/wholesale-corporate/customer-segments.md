# Wholesale Customer Segments

Detail on the segments introduced in [README.md](README.md). Segmentation drives product, channel, pricing, KYB depth, and relationship model.

---

## Segmentation Dimensions

Banks typically segment on:
- **Revenue / Turnover** (primary).
- **Industry / Sector**.
- **Geography** (single-country vs MNC).
- **Banking complexity** (single-product to multi-product).
- **Customer-type** (corporate, FIG, sovereign, NBFI).
- **Strategic importance** (relationship-managed vs digital-only).

---

## SME — Small & Medium Enterprise

| Dimension | Typical |
|---|---|
| Revenue threshold | Often < USD 50M (varies by bank + country) |
| Headcount | < 250 (EU SME definition); other definitions vary |
| Banking complexity | Limited products (account, debit, basic loans, payments) |
| Coverage model | Digital-first; relationship-light or pooled |
| Pricing | Standardised; minimal negotiation |
| Onboarding | Streamlined KYB; often eligible for fast-track |
| Cross-sell from retail | Common — many SMEs are managed by retail bank with SME overlay |

### Common SME Products
- Business current account.
- Business debit + credit card.
- Working capital line / overdraft.
- Term loan (smaller-ticket).
- Trade finance (LC, BG smaller-ticket).
- Bulk payments file.
- Salary processing.
- Receivables collection (eNACH mandates, UPI).
- Government-scheme loans (CGTMSE in IN, SBA in US, CBILS-equivalent in UK).

---

## Middle Market / Mid-Corp

| Dimension | Typical |
|---|---|
| Revenue threshold | USD 50M–USD 1B |
| Banking complexity | Multi-product across cash, trade, lending |
| Coverage model | Dedicated Relationship Manager (RM) + product specialists |
| Pricing | Negotiated with template ranges |
| Onboarding | Full KYB; standard implementation |
| FX exposure | Often material; needs FX desk relationship |

### Typical Products
- Full cash-management suite (lockbox, ARP, ZBA, sweeps).
- Working capital + term loan + RCF.
- Trade finance (multi-product).
- Treasury workstation integration.
- FX hedging (forwards, NDF).
- Investment products.
- Capital-markets-light cross-sell (bond issuance for upper end).

---

## Large Corporate / Corporate Banking

| Dimension | Typical |
|---|---|
| Revenue threshold | > USD 1B |
| Banking complexity | All products; bespoke structures |
| Coverage model | Senior RM + multiple product specialists; investment banker as well for capital-markets-active |
| Pricing | Heavily negotiated; bilateral matrices |
| Onboarding | Multi-month for complex |
| Multi-bank | Standard; bank competes for share of wallet |

### Typical Products
- All Treasury Services products.
- Multi-bank cash mgmt with concentration.
- Multi-currency notional pooling.
- Virtual accounts at scale.
- Syndicated loans (lead arranger or participant).
- Project / acquisition / leveraged finance.
- Trade finance multi-product.
- FX + interest-rate derivatives.
- Capital markets (DCM, ECM).
- Custody (if FIG-touching).
- Securities lending.

### KPIs Bank Cares About
- Wallet share (% of customer's banking spend with this bank).
- Cross-sell ratio (products per customer).
- Revenue per customer.
- Customer profitability (RAROC — Risk-Adjusted Return on Capital).

---

## MNC — Multinational Corporation

| Dimension | Typical |
|---|---|
| Operations | Multi-country |
| Treasury structure | Centralised / decentralised / regional models |
| Banking complexity | Highest |
| Pricing | Heavily negotiated; global pricing umbrellas |
| Onboarding | Multi-jurisdiction KYB; long onboarding for new countries |

### MNC Treasury Structures
- **Centralised**: single global treasury runs all flows; in-house bank model.
- **Regional**: regional treasury centres (EMEA, AMER, APAC).
- **Decentralised**: each subsidiary runs its own treasury (rare for very large MNCs).

### Specific MNC Products
- **In-House Bank (IHB)** — single entity provides banking to all subsidiaries; bank provides infrastructure.
- **Payment-on-Behalf-Of (POBO)** — IHB makes payments on behalf of subsidiaries.
- **Receipt-on-Behalf-Of (ROBO)** — IHB receives on behalf of subsidiaries.
- **Inter-company netting** — multilateral netting of inter-co flows; bank executes the net.
- **Multi-currency liquidity** — pooling + investment across currencies.
- **Single-window connectivity** — S4C / SCORE or single TWS for global view.

---

## FIG — Financial Institutions Group

| Dimension | Typical |
|---|---|
| Customer type | Banks, broker-dealers, asset managers, insurance, CCPs, exchanges |
| Products | Correspondent banking, custody, securities services |
| Compliance burden | Highest — bank-as-customer scrutiny |
| Risk profile | Counterparty concentration risk; reputational risk |
| Onboarding | Wolfsberg CBDDQ + EDD |

### Typical FIG Products
- **Correspondent Banking** — USD clearing, multi-currency nostro.
- **Custody + Securities Services** — held-on-behalf-of services.
- **Cash Management** — for the FIG's own operations.
- **FX + Derivatives** — for FIG hedging.
- **Securities Lending** — both as borrower-side intermediary and lender.

### Critical Concerns
- **Nested correspondent** — does this FIG offer correspondent to others, and if so, is that disclosed?
- **MSB sub-segment** — money service businesses; heightened sanctions + AML risk.
- **Crypto VASP** — if FIG touches digital assets, fully different risk + regulatory profile.
- **Wolfsberg CBDDQ annual refresh**.
- **Country-risk overlay** — FIG's home jurisdiction adds risk weighting.

---

## Sovereign / Public Sector

| Dimension | Typical |
|---|---|
| Customer type | National governments, central banks, state / provincial governments, sub-sovereign agencies, multilateral institutions |
| Pricing | Often relationship-driven, low-margin |
| Strategic importance | High (mandate access, reputation) |
| Documentation | Specific to government counterparties |

### Typical Sovereign Products
- Treasury services.
- Government bond underwriting + distribution.
- Custody of reserves.
- Cross-border settlement.
- FX.
- Trade-related guarantees (export credit).

### Specific Compliance
- Sovereign immunity considerations.
- UN-designated countries / regimes.
- Sanctions sensitivity.
- AML overlay specific to PEPs (sovereign customers often have PEP overlap).

---

## NBFI — Non-Bank Financial Institution

| Dimension | Typical |
|---|---|
| Customer type | Fintechs, MSBs, payment processors, fund administrators, FX dealers, crypto firms, hedge funds, family offices |
| Risk profile | Heightened |
| Compliance | Enhanced AML + sanctions diligence |
| Products | Mixed — banking + cash mgmt + sometimes lending |

### Sub-Segments
- **Fintech / Sponsor Bank customers** — fintech relies on the bank for charter access.
- **MSB (Money Service Business)** — money transmitters, currency exchanges; high-risk.
- **Crypto / VASP** — digital asset firms; many banks decline.
- **Hedge Fund + PE Fund** — investment-side relationship.
- **Family Office** — wealth management overlap.
- **Trust Companies** — depend on jurisdiction.

### Specific Concerns
- Nested correspondent issues for MSBs.
- Fintech downstream-customer KYC pass-through.
- Crypto exposure assessment.
- Pre-emptive risk-rating uplift.

---

## Pricing Models by Segment

| Segment | Typical Pricing Approach |
|---|---|
| SME | Standardised tariff |
| Mid-Corp | Negotiated; template ranges |
| Large Corp | Heavily negotiated; bilateral matrix |
| MNC | Global pricing umbrella with regional overrides |
| FIG | Bilateral; usually with mutual reciprocity |
| Sovereign | Often near-cost, relationship-driven |
| NBFI | Risk-premium loaded; bilateral |

---

## Coverage Model by Segment

| Segment | Coverage |
|---|---|
| SME | Digital-led; lightweight RM pool |
| Mid-Corp | Dedicated RM + product specialists on demand |
| Large Corp | Senior RM + product specialists embedded |
| MNC | Global RM + regional RMs + specialists |
| FIG | FIG specialist coverage + dedicated client service |
| Sovereign | Sovereign-specific senior banker |
| NBFI | Industry-specialist coverage |

---

## Open Questions

- [ ] Confirm bank's segmentation thresholds + nomenclature.
- [ ] Confirm coverage model per segment.
- [ ] Confirm pricing-template structure.
- [ ] Confirm onboarding capacity + timelines per segment.
- [ ] Confirm NBFI risk-appetite policy (which sub-segments accepted, which declined).
