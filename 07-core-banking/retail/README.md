# Retail Banking

Retail banking serves **individuals + sole-traders + small businesses** at scale: standardised products, self-service channels, consumer-protection-regulated. The volume is high; per-customer revenue is low; margin comes from scale + cross-sell + NIM on the CASA float.

> Sub-domain: `Retail`
> Default sensitivity: `Internal` (policy, taxonomy) / `Confidential` (customer data, balances, transactions)

---

## Navigation

| File | Purpose |
|---|---|
| [products.md](products.md) | Product catalogue overview — deposits, lending, cards, channels |
| [deposits.md](deposits.md) | Deposit products — CASA, time, NRI, special-purpose |
| [lending.md](lending.md) | Lending products — mortgages, personal, auto, education, cards |
| [cards.md](cards.md) | Cards — debit, credit, prepaid, co-brand; issuing operations |
| [digital-channels.md](digital-channels.md) | Mobile + internet + IVR + conversational banking |
| [operations.md](operations.md) | Branch, ATM, KYC, dormancy, deceased customer, escheatment |

---

## Customer Segments

| Segment | Description | Typical Products |
|---|---|---|
| **Mass Market** | Standard customers | CASA, debit, basic credit, basic loans |
| **Mass Affluent** | Moderate balances + higher value | Premium CASA, multi-card, mortgage, basic investment |
| **HNI / Premier / Priority** | High balance + high engagement | Relationship-managed, multi-product, basic wealth + private |
| **Salaried / Payroll** | Employer-introduced | Salary account + payroll-linked benefits |
| **Pensioner / Senior** | Often regulated tariff | Special-rate savings + simplified channels |
| **Student / Youth** | Lifecycle entry product | Reduced-fee CASA + education loan |
| **NRI (India-specific)** | Non-resident Indian | NRE / NRO / FCNR accounts |
| **Self-employed / Professional** | Often blurs into SME | Mix of retail + small-business products |

Each segment maps to:
- Pricing tier.
- KYC depth.
- Channel preference / SLA.
- Cross-sell scoring.
- Risk rating baseline.

---

## Revenue Model

| Source | Description |
|---|---|
| **NIM (Net Interest Margin)** | Difference between interest earned on lending + investment vs. paid on deposits. Largest source for most retail banks. |
| **Fees** | Account maintenance, ATM, FX margin, payment, statement, locker, replacement. |
| **Interchange (cards)** | Card-issuing interchange income, typically 0.2–0.3% on debit (capped in EU/UK), higher on credit. |
| **Spread (FX)** | Markup on retail FX conversions. |
| **Cross-sell** | Bancassurance, mutual funds, brokerage, gold loans. |

---

## Channel Mix (Typical Modern Retail Bank)

| Channel | % of customer transactions (rough industry avg.) |
|---|---|
| Mobile | 60–80% (and growing) |
| Internet banking | 10–20% |
| ATM | 5–10% |
| Branch | 5–10% (declining) |
| Voice / IVR | 1–3% |
| Branch — but for sales / advice | Higher than transactions |

---

## Operational Concerns

- **Onboarding latency** — minutes to open an account (digital-first); hours or days (traditional).
- **First Time Right (FTR)** — % of transactions completed without rework.
- **Customer effort (CES)** — survey score on ease.
- **NPS** — net promoter score.
- **Dispute resolution time** — hours / days; Reg E / PSRs / similar local rules drive minimums.
- **Fraud loss ratio** — basis points of volume.

---

## Regulatory Lens for Retail

| Regime | Examples |
|---|---|
| US | Reg E, Reg DD, Reg CC, Reg Z, BSA, CFPB Section 1033 |
| UK | PSRs 2017, FCA Consumer Duty, MLRs 2017, FCA BCOBS / CASS |
| EU | PSD2 (→ PSD3 / PSR), Consumer Credit Directive, GDPR |
| India | RBI Master Directions, IT Act, RBI Customer Protection, PMLA, KYC rules |
| Singapore | MAS PS Act, PDPA, Notice 626 |

Consumer protection is the dominant lens in retail — sharply different from wholesale, where prudential and corporate-counterparty rules dominate.

---

## Open Questions

- [ ] Confirm bank's segment definitions and pricing tiers.
- [ ] Confirm channel mix targets and current state.
- [ ] Confirm Wealth / Private Banking boundary (where does HNI hand off to PB).
- [ ] Confirm CBS instance and channels stack.
