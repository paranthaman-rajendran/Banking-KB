# Gap Analysis — KB vs. Tier-1 US MNC Bank

Honest review of the Payments KB content against what a tier-1 US universal bank (JPMC, Bank of America, Wells Fargo, Citi) actually runs in production. Identifies the structural gaps and proposes a prioritised fill-in plan.

> Compiled: 2026-06-22.
> Audience: KB owners + Payments architecture / product leads.

---

## Executive Summary

**What's strong**: rails, scheme rules, message standards, regulatory mapping by jurisdiction, hub architecture, two vendor deep-dives, foundational concepts.

**What's missing for tier-1 US MNC banks**: the **wholesale / treasury services business stack** (the revenue engine at JPMC TS, BofA GTS, Wells WCB), **trade finance**, **card issuing + acquiring as a business** (not just standards), **foreign branch + group operations**, **stress testing & operational risk capital**, **US-specific Open Banking & Section 1033 reality**, **disbursements & push-to-card**, and **sponsor-bank / BaaS** dynamics that the largest US banks are exposed to indirectly.

Roughly: today's KB covers the **retail + scheme + hub layer** well; it under-covers the **wholesale + corporate banking + group-level governance** layer that is most of these banks' payments revenue and risk.

---

## What's Well Covered

| Area | Files |
|---|---|
| Rails (US, UK, India, Europe instant, cross-border) | [rails/](rails/) |
| Message standards (ISO 20022, SWIFT MT/MX, ISO 8583) | [standards/](standards/) |
| Payment lifecycle stages | [architecture/lifecycle.md](architecture/lifecycle.md) |
| Systems landscape + categories | [architecture/systems-landscape.md](architecture/systems-landscape.md) |
| Payment engine vendor inventory | [architecture/payment-engines.md](architecture/payment-engines.md) |
| Two vendor deep-dives | [architecture/vendors/finastra-gpp.md](architecture/vendors/finastra-gpp.md), [architecture/vendors/oracle-obpm.md](architecture/vendors/oracle-obpm.md) |
| Per-jurisdiction regulatory | [regulatory/](regulatory/) (8 files) |
| Engine compliance matrix | [regulatory/engine-compliance-matrix.md](regulatory/engine-compliance-matrix.md) |
| Generic concepts (sanctions, AML, settlement, etc.) | [concepts.md](concepts.md) |
| Glossary + golden eval questions | [glossary.md](glossary.md), [golden-questions.md](golden-questions.md) |

This is a credible foundation for an India/UK/EU retail-rails-focused programme.

---

## Major Gaps — Tier-1 US MNC Lens

### Gap 1: Treasury Services / Wholesale Payments Product Stack

The biggest missing chunk. JPMC Treasury Services, BofA Global Transaction Services, Wells Wholesale Commercial Banking, Citi TTS — each is a multi-billion-USD revenue line whose product set the KB barely touches.

Missing:
- **Integrated Payables** — single corporate file in → multi-rail out (ACH, wire, check, RTP, FedNow, card disbursement). Vendor stack often includes Bottomline Cyber Fend, Fiserv ImageCenter, FIS PayDirect.
- **Integrated Receivables (IR)** — lockbox + ACH receivables + wire receipts + virtual accounts → matched against open-invoice file. Often AI-assisted matching today.
- **Lockbox services** (physical, image, electronic) — paper-cheque collection at scale, image capture, EFT-conversion (ARC/BOC SEC codes).
- **Account Reconciliation Services (ARP)** — partial / full ARP, positive pay, reverse positive pay.
- **Earnings Credit Rate (ECR) + Account Analysis (AA)** — pricing model where corporate maintains balances in lieu of fees; AA statements are a core product.
- **Zero Balance Accounts (ZBA), Concentration / Sweeps, Notional Pooling** — corporate liquidity products.
- **Virtual Accounts** — segregated bookkeeping under one master account; common for fintech / property management / law-firm escrow / marketplace use cases.
- **Cross-currency pooling** — global treasury liquidity.
- **Positive Pay / Payee-Match Positive Pay** — cheque fraud control.
- **Same-Day ACH origination at corporate scale** — beyond the basic rail file.
- **SWIFT for Corporates (S4C) / SCORE / MA-CUG** — multi-bank corporate connectivity model.
- **Healthcare payments** — EDI 835 (Remit) / 837 (Claim) over ACH CCD+ / CTX with 820 addenda.
- **Government payments / TT&L** — Treasury Tax and Loan, Direct Express, IRS integrations.
- **Treasury workstation integration** — Kyriba, FIS Trax, ION Reval, SAP Treasury and Risk Mgmt (TRM), Coupa Treasury, BlackLine.

### Gap 2: Trade Finance

Tier-1 MNC banks have multi-billion-USD trade finance books. Not in the KB.

Missing:
- **Letters of Credit (LC)** — issuing, advising, confirming, negotiating; sight vs usance.
- **Standby LCs (SBLC)** — financial vs performance.
- **Documentary Collections** — D/P (Documents against Payment), D/A (Documents against Acceptance).
- **Open Account** — increasingly the dominant model with TBML risk.
- **Supply Chain Finance** (SCF) — payables finance, receivables finance, dynamic discounting.
- **Forfaiting / Factoring** — receivables sale.
- **Trade Receivables Securitization**.
- **UCP 600** — Uniform Customs and Practice for Documentary Credits.
- **ISBP** — International Standard Banking Practice for examination of documents.
- **URDG 758** — Uniform Rules for Demand Guarantees.
- **URC 522** — Uniform Rules for Collections.
- **MT 7-series SWIFT messages** (MT700, 707, 710, 720, 740, 750, 760, 768, 769, 770, 798) — relevant to LC + guarantees.
- **ICC Banking Commission** rules + opinions.
- **BAFT** — Bankers Association for Finance and Trade industry standards.
- **Trade-Based Money Laundering (TBML)** typologies + controls.
- **Sanctions in trade** — dual-use goods, end-use / end-user controls.

### Gap 3: Card Issuing + Acquiring as a Business

The KB has [iso-8583.md](standards/iso-8583.md) for the message standard, but not the **commercial structure** that tier-1 issuers + acquirers actually run.

Missing on issuing:
- **Issuer-side processing** — Chase Card Services, BofA Cards, Wells Card. BIN management, embossing / personalisation, dispute representment, chargebacks at scale.
- **Co-brand cards** — Chase Sapphire / United / Amazon / Disney / Marriott; BofA Customized Cash; Wells Active Cash. Revenue-share economics.
- **Reward / loyalty programmes**.
- **Push-to-card outbound** — Visa Direct + Mastercard Send for disbursement (insurance claims, gig economy, marketplace payouts).
- **Tokenisation at scale** — network tokens, device tokens (Apple Pay, Google Pay), e-commerce token vault.
- **Card-not-present fraud + 3DS at scale**.
- **EMV personalisation + key management**.
- **Card issuing platforms** — FIS Card Issuance, Fiserv, TSYS (Global Payments), ACI BASE24-eps, Marqeta (fintech-issuer), Galileo, i2c.

Missing on acquiring:
- **Chase Merchant Services / BofA Merchant Services / Wells Merchant Services** — multi-billion-USD merchant businesses.
- **ISO / MSP (Independent Sales Organisation / Member Service Provider)** distribution model.
- **Interchange economics + interchange-plus pricing**.
- **MCC (Merchant Category Codes)** + risk-based MCC pricing.
- **Chargeback / dispute representment workflow** — Visa CDRN, Verifi Order Insight, Mastercom.
- **MOTO + e-commerce risk classification**.
- **3DS v2 + EMV 3DS frictionless flow**.
- **Network tokens for e-commerce + push-payment**.
- **Cross-border interchange + scheme fees**.
- **High-risk merchant management** (gambling, adult, MLM).

### Gap 4: Foreign Branch + Group Operations

Tier-1 MNC banks operate across 30–100 countries. Each branch / subsidiary has its own host-country regulatory regime, plus group-level controls.

Missing:
- **Branch vs Subsidiary vs Representative Office** licensing models per host country.
- **Group-wide AML / sanctions governance** — single global watchlist + jurisdiction-specific overlays.
- **Foreign Bank Organization (FBO) Enhanced Prudential Standards** in the US — IHC (Intermediate Holding Company) structure for non-US banks operating in the US.
- **Group-wide customer KYC** — single CIF or federated; data sharing constraints (CN PIPL, EU GDPR, etc.).
- **Inter-affiliate / book transfer flows** — intercompany payments, transfer pricing, regulatory capital allocation.
- **CRS / FATCA at scale** — multi-jurisdictional tax reporting.
- **Group sanctions governance** — internal "highest common denominator" policy.

### Gap 5: Securities Cash Settlement + Custody-Adjacent Payments

JPMC, BofA, BNY Mellon, State Street are custody / securities-services giants. Cash side of securities settlement is core.

Missing:
- **DTC (Depository Trust Company)** — equity / corporate bond / muni cash settlement in the US.
- **FICC / NSCC** — Fixed Income / Equity scheme clearing.
- **DvP (Delivery vs Payment)** mechanics.
- **T+1 settlement transition (May 2024 in US)** — impact on cash funding cycles.
- **Margin calls + variation margin** payment flows.
- **Corporate Actions cash** — dividends, coupons, redemptions.
- **Foreign tax reclaim** flows.
- **Securities lending cash collateral** flows.
- **CLS (Continuous Linked Settlement)** — only briefly touched in [concepts.md](concepts.md); these banks are CLS settlement members; CLS Now intraday liquidity.
- **CHIPS deep-dive** — JPMC, Citi, BofA, BNY Mellon are top CHIPS participants.

### Gap 6: Operational Risk Capital + Stress Testing

US tier-1 banks operate under enhanced prudential standards.

Missing:
- **Basel III Operational Risk** — SMA (Standardised Measurement Approach) replacing AMA.
- **CCAR (Comprehensive Capital Analysis and Review)** — Fed annual stress test.
- **DFAST** — Dodd-Frank Act Stress Test.
- **Recovery and Resolution Planning (RRP)** — "living wills".
- **LCR / NSFR** at HQLA + USD funding constraints — affects intraday liquidity for payments.
- **TLAC** — Total Loss Absorbing Capacity.
- **Reg HH / Reg YY** — operational + prudential.
- **SR Letters** — FRB supervisory guidance (SR 11-7 model risk, SR 13-19 third-party risk, SR 23-4 ICT risk).
- **OCC Heightened Standards** — for large national banks.
- **Operational Resilience programmes** — FRB / OCC / FDIC interagency policy (Oct 2023).
- **Critical operations classification** — payments is universally critical.

### Gap 7: US Open Banking — Section 1033 + FDX + Aggregators

The EU [europe.md](regulatory/europe.md) and UK [uk.md](regulatory/uk.md) docs cover PSD2-driven Open Banking, but US Open Banking has a very different shape and is not deeply covered.

Missing:
- **CFPB Section 1033** — Personal Financial Data Rights, finalised Oct 2024; phased compliance.
- **FDX (Financial Data Exchange)** — industry standards body and API spec, evolving as the de facto US OB standard.
- **Aggregator ecosystem** — Plaid, MX, Yodlee, Finicity (now Mastercard), Akoya (FMR-backed).
- **Screen-scraping → tokenised API transition**.
- **Data Recipient (DR) authorisation model**.
- **Provider obligations** — covered banks must offer free secure data access.
- **Data security + permissioning** under FDX.

### Gap 8: Disbursement Products + Instant Payouts

A fast-growing revenue line for tier-1 US banks.

Missing:
- **Push-to-card disbursements** — Visa Direct + Mastercard Send.
- **Instant payouts to debit cards / accounts** — gig economy (Uber Instant Pay), insurance claims, marketplace.
- **Prepaid card disbursements** — government benefits, payroll cards, Direct Express, state unemployment.
- **B2C instant via RTP / FedNow** — emerging revenue line.
- **Mass-payment / payout APIs** — competing with Adyen, Stripe Connect, Modern Treasury.

### Gap 9: Sponsor Bank / BaaS Dynamics

US fintech ecosystem is built on sponsor-bank arrangements. Even the largest banks are touched indirectly (correspondent flows, customer overlap).

Missing:
- **Sponsor Bank model** — bank holds the regulated charter; fintech is a programme manager.
- **BSA / AML allocation** between sponsor and fintech.
- **Reg E + Reg DD compliance** in pass-through arrangements.
- **Customer-of-customer (Cosmo) accounting** — virtual accounts under master.
- **Recent enforcement environment** — OCC / FDIC consent orders on sponsor banks (Cross River, Blue Ridge, etc., 2023–2024).
- **OCC "third-party risk management" interagency guidance (June 2023)**.
- **State MTL coverage via sponsor-bank shield** — and where that shield doesn't apply.

### Gap 10: CBDC + Stablecoin + Tokenised Deposits

Strategic future state for tier-1 banks.

Missing:
- **JPM Coin** — JPMC's deposit-token wholesale payment system (Onyx / JPMorgan Onyx Digital Assets).
- **Project Cedar** (NY Fed) — wholesale cross-border CBDC research.
- **Project Agora** (BIS) — multi-CBDC / tokenised-deposit cross-border PoC.
- **Regulated stablecoin landscape** — proposed US Stablecoin legislation; PayPal PYUSD; Circle USDC.
- **Custody for digital assets** — limited at major banks under current rules; SAB 121 implications.
- **Tokenised deposits vs stablecoins** — bank-issued deposit tokens as future settlement asset.

### Gap 11: Recent CFPB Actions Reshaping US Payments

Significant for product / engine design.

Missing:
- **Junk fees** — overdraft fee caps, NSF fee restrictions (rules + enforcement evolving).
- **Overdraft rules** — final rule + litigation status.
- **BNPL regulation** — CFPB treatment as Reg Z credit cards (for certain products).
- **Section 1033** (also in Gap 7).
- **Larger Participants Rule** for non-bank digital wallet apps.

### Gap 12: Treasury Services Customer Channel + Connectivity

Wholesale corporates connect to tier-1 banks via specific protocols + portals.

Missing:
- **JPMC ACCESS / BofA CashPro / Wells CEO / Citi CitiDirect** — these flagship corporate banking portals are major engineering artefacts.
- **Corporate API estates** — JPMC API Developer Portal, BofA APIs, Wells Wells Developer.
- **Host-to-Host (H2H)** — secure file transfer (SFTP, AS2, MFT) for corporate file submission.
- **MT940 / camt.053 customer statement delivery**.
- **BAI2 file format** (legacy US corporate statement).
- **ACH addenda standards** — EDI 820, 835, NACHA addenda.
- **Real-time treasury** — intraday MT942 / camt.052 reporting.

### Gap 13: ATM + Branch Operations

Volumes are falling but tier-1 banks operate enormous ATM + branch networks.

Missing:
- **ATM driver software** — NCR Aptra, Diebold Nixdorf Vynamic.
- **ATM cash management** — replenishment, dispense pattern AI.
- **LINK-equivalent in US** (no national network — issuer-acquirer bilateral / regional + STAR, NYCE, Pulse, Accel, Allpoint).
- **Branch teller payment functions** — cash, cheque cashing, cashier's cheque, wire initiation.
- **Reg E hot-card processing** for lost / stolen cards.

### Gap 14: Healthcare + Government + Specific Verticals

Specific verticals with their own payment standards.

Missing:
- **EDI 835 / 837 / 820** over ACH CTX — healthcare claim / remit / premium.
- **EFT / ERA pairing** for healthcare provider reconciliation.
- **HSA / FSA cards** — IRS-defined.
- **TT&L (Treasury Tax and Loan)** — Federal government deposits.
- **Direct Express** — federal benefit prepaid card.
- **IRS / state tax payment integrations**.
- **EBT (Electronic Benefits Transfer)** — SNAP, TANF, state benefit.
- **Real estate / title industry payments** — pre-FedNow, wires dominate; APP fraud high.

### Gap 15: Internal Audit + SOX for Payment Controls

US-listed banks are public companies under SOX.

Missing:
- **SOX 404 controls** for payment processing.
- **PCAOB inspection requirements**.
- **Internal Audit lines of defence** — 1LoD operations, 2LoD risk/compliance, 3LoD audit.
- **Control attestation processes**.

### Gap 16: Customer Channels — Real-Time Bank Comms

Modern payments need omnichannel customer experience.

Missing:
- **Real-time notifications architecture** — push, SMS, email at scale.
- **Customer comms during dispute / investigation**.
- **Self-service in-app dispute initiation**.
- **Voice channel + IVR** for payment status.
- **Bot / agent assist for ops** — increasingly LLM-augmented.

---

## Lower-Priority Gaps

- Stablecoin and crypto custody (regulatory + product) — but evolving.
- ESG / Carbon-tracked payments — emerging, not yet operational at most banks.
- Quantum-resistant cryptography migration — long-horizon programme.
- DePIN / Decentralised payments — research-only.

---

## Recommended Fill-In Plan (Prioritised)

### Tier 1 — Add Soon (revenue-critical or high-risk)

1. **Wholesale Treasury Services product stack** — new folder `07-wholesale-payments/` or add a `treasury-services/` sub-folder under `06-payments/`.
2. **Trade Finance** — new folder `08-trade-finance/` or sub-folder.
3. **Card Issuing + Acquiring as a business** — extend `cards/` content beyond ISO 8583 standards.
4. **US Open Banking (Section 1033, FDX, aggregators)** — extend [regulatory/usa.md](regulatory/usa.md).
5. **Operational Risk Capital + Stress Testing** — extend [regulatory/usa.md](regulatory/usa.md); add a `governance/` cross-link.
6. **Sponsor Bank / BaaS dynamics** — extend [regulatory/usa.md](regulatory/usa.md).

### Tier 2 — Add Next (operationally important)

7. **Foreign Branch + Group Operations** — new file `multi-jurisdictional-group-operations.md`.
8. **Securities cash settlement (DTC, FICC, NSCC, CLS)** — extend [architecture/lifecycle.md](architecture/lifecycle.md) or new file.
9. **Disbursement products / push-to-card / instant payouts** — new file.
10. **CBDC + stablecoin + tokenised deposits (US slant)** — new file or extension.
11. **Treasury Services customer channels (ACCESS / CashPro / CEO)** — extend [architecture/systems-landscape.md](architecture/systems-landscape.md).

### Tier 3 — Add When Relevant

12. ATM + branch deep dive.
13. Healthcare + government verticals.
14. SOX + Internal Audit for payments.
15. Real-time customer comms architecture.
16. Specific tier-1 US vendor deep-dives (FIS, Fiserv, ACI BASE24, Bottomline, Marqeta, etc.).

---

## Reframe of Pilot Selection

The original Phase-2 pilot recommendation in this KB was a **UPI Ops copilot**. For a tier-1 US MNC bank specifically, the highest-ROI Payments pilot is more likely one of:

- **Wire investigation copilot** — high-volume, well-bounded, strong ROI, low data-classification risk.
- **Sanctions hit explainability copilot** — solves a real ops pain at scale.
- **Wholesale treasury onboarding KYC + product matching** — revenue-relevant + complex enough to demonstrate value.
- **Trade finance LC discrepancy detection** — narrow scope, deep regulatory text fit.

This re-prioritisation should land in the pilot scope discussion if the KB is being built for a US MNC archetype rather than a UK retail / India hybrid.

---

## What This Means for the KB Structure

Current taxonomy in [01-taxonomy/taxonomy.md](../01-taxonomy/taxonomy.md):

```
Payments
├── Domestic
├── Cross-Border
└── Real-Time Rails
```

Recommended extension for tier-1 universal-bank coverage:

```
Payments
├── Domestic
├── Cross-Border
├── Real-Time Rails
├── Wholesale / Treasury Services        ← Gap 1
├── Cards (Issuing + Acquiring as business)  ← Gap 3
└── Trade Finance                        ← Gap 2  (or split to a sibling sub-domain)
```

Trade Finance might warrant its own top-level sub-domain since it intersects payments + lending + compliance heavily. The decision affects taxonomy + access-control namespacing.

---

## Open Questions

- [ ] Confirm bank archetype the KB is being built for — pure retail/UK/India bias was the implicit assumption; if the target is a tier-1 US MNC, the priority order changes.
- [ ] Confirm whether Trade Finance is in scope for this KB or a separate KB.
- [ ] Confirm Cards as a sub-domain (Issuing + Acquiring + Switches) — likely yes for a tier-1 universal bank.
- [ ] Confirm wholesale-vs-retail content split — same namespace or separate sub-domains?
- [ ] Confirm if any tier-1 US-specific vendor deep-dives are needed next (FIS, Fiserv, ACI, Marqeta).
- [ ] Confirm pilot reframe — does the org want the original UPI Ops copilot or a tier-1 US-aligned pilot?
