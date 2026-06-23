# Core Banking Sub-Domain

Knowledge base content for **core banking** — the customer + account + product platform layer that sits beneath Payments and feeds the General Ledger. Covers both **Retail** and **Wholesale / Corporate** sides of a universal bank.

> Domain code: `CoreBanking`
> Sub-domain codes: `Retail`, `WholesaleCorporate`, `Platform` (for the CBS systems themselves)
> Status: knowledge scaffolding — content to be populated per bank's actual product catalogue.

---

## Navigation

| File / Folder | Purpose |
|---|---|
| [concepts.md](concepts.md) | Foundational concepts — CASA, deposit, loan, accrual, GL/sub-ledger, EOD/BOD, posting, value date, customer master/CIF — **start here** |
| [taxonomy-detail.md](taxonomy-detail.md) | Sub-domain codes + product class catalogue |
| [core-banking-systems.md](core-banking-systems.md) | CBS landscape — Finacle, Flexcube, T24/Transact, BaNCS, Vault, Mambu, 10x, FIS, Fiserv |
| [eod-batch-cycle.md](eod-batch-cycle.md) | EOD/BOD batch cycle — job sequence, retail vs. wholesale differences, 24x7 impact, failure modes |
| [year-end-activities.md](year-end-activities.md) | Year-end activities — calendar / fiscal / tax year-end; GL close, tax certs, FATCA/CRS, provisioning recompute, escheatment, KYC refresh, regulatory cycles, jurisdiction nuances |
| [retail/](retail/) | Retail banking — products, deposits, lending, cards, channels, ops |
| [wholesale-corporate/](wholesale-corporate/) | Wholesale / corporate banking — treasury services, lending, trade finance, cash management, channels, segments |

---

## Why a Distinct Sub-Domain

Core banking is **separate from Payments**:
- Payments **moves money**; core banking **books money** (debit/credit on customer accounts + GL).
- Core banking owns the **customer master (CIF)**, **product master**, and **account master**.
- Payments is rail-oriented (FedWire, FPS, UPI, SEPA, SWIFT); core banking is **product-oriented** (savings, current, term loan, LC).
- Settlement on a payment is the trigger; core banking is what consumes the trigger and posts the books.

Both sub-domains are typically delivered by **separate vendor products** (a CBS + a Payment Hub) integrated by the bank — or, in legacy stacks, bundled by the same vendor (Finacle / Flexcube / T24 all bundle a payments module with the CBS).

---

## Retail vs. Wholesale / Corporate

These two sides of core banking diverge sharply, and many large banks run **distinct CBS platforms per side**:

| Dimension | Retail | Wholesale / Corporate |
|---|---|---|
| Customer count | Millions–tens of millions | Hundreds–tens of thousands |
| Average ticket | Small (USD 10s–10000s) | Large (USD 100k–billions) |
| Product complexity | Standardised, configurable | Bespoke, negotiated |
| Channels | Mobile, internet, branch, ATM | Portal (ACCESS / CashPro / CEO), H2H, S4C, API |
| Pricing | Standard tariff | Negotiated, ECR + AA |
| Onboarding | Self-service, eKYC | Relationship-managed, document-heavy KYB |
| Revenue model | NIM + fee + interchange | NIM + fee + earnings credit + transaction-volume |
| Regulatory weight | Consumer protection (Reg E, FCA Consumer Duty) | Prudential (Basel, large-exposures) |
| Disputes | Reg E / Bacs DD Guarantee | Bilateral / per-product contract |

The KB treats them as **parallel folders** with shared concepts but distinct product / process / channel content.

---

## Relationship to Other KB Sub-Domains

| Sub-Domain | Interaction |
|---|---|
| [Payments](../06-payments/) | Payments move money; core banking posts the books. Tight integration via account number, scheme reference, settlement |
| Compliance & Regulatory | Customer KYC, AML, sanctions live in core banking customer master; payments + lending consume |
| Risk Management | Credit risk on the lending book lives on the CBS; market risk lives in capital-markets systems |
| Treasury & ALM | Bank's own liquidity + funding sits at the CBS-treasury boundary |
| Wealth Management | Often runs on a separate platform; customer master shared with retail CBS |

---

## Cross-References

- Master taxonomy: [../01-taxonomy/taxonomy.md](../01-taxonomy/taxonomy.md)
- Metadata schema (mandatory fields): [../01-taxonomy/metadata-schema.md](../01-taxonomy/metadata-schema.md)
- Data classification tiers: [../03-governance/data-classification.md](../03-governance/data-classification.md)
- Payments sub-domain (sister, tightly integrated): [../06-payments/](../06-payments/)

---

## Open Questions for Sub-Domain Sign-off

- [ ] Confirm CBS product(s) in scope for the bank — single CBS vs. separate retail / corporate stacks.
- [ ] Confirm whether `WholesaleCorporate` should split further into `TreasuryServices` + `CorporateLending` + `TradeFinance` (the tier-1 universal-bank view).
- [ ] Confirm sub-domain owner (typically per-CBS team).
- [ ] Confirm scope split between this sub-domain and Wealth Management.
