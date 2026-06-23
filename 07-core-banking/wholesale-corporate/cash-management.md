# Wholesale Cash Management — Deep Dive

Companion to [treasury-services.md](treasury-services.md). Where Treasury Services covers payment / receivable / reconciliation products, this file goes deeper on the **liquidity products** — pooling, sweeps, virtual accounts as a system, and intraday liquidity for corporates.

---

## Corporate Treasury's Core Problem

A multi-entity, multi-currency, multi-bank corporation has:
- Hundreds of bank accounts globally.
- Idle balances in some; overdrafts in others.
- FX exposure on multi-currency.
- Cash forecast uncertainty.
- Regulatory + tax friction on inter-entity transfers.

Cash management products **optimise** this:
- Visibility (consolidated reporting).
- Concentration (move cash to where needed).
- Investment (return on surplus).
- FX management (multi-currency).
- Funding (utilise idle balances against overdrafts).

---

## Physical Pooling (Sweeping)

Actual fund movement between accounts.

### Variants Recap
| Type | Description |
|---|---|
| **Zero-balance** | Sub-accounts swept to zero; master holds true balance |
| **Target-balance** | Leave target on sub; sweep rest |
| **Threshold** | Sweep only when exceeds threshold |
| **Single-currency** | Within currency |
| **Multi-currency with FX** | Cross-currency sweeps with FX conversion |
| **Multi-bank (SWIFT-driven)** | Sweep across banks via SWIFT MT (often MT101 + MT940 reporting) |

### Tax + Legal Implications
Physical movement = real fund transfer = potentially:
- Inter-company loan accounting.
- Transfer pricing (between affiliates).
- Withholding tax (cross-border).
- Foreign exchange regulatory reporting (SAFE in China, FEMA in India).

Tier-1 banks structure pools to minimise these — typically via **on-shore notional + cross-border physical hybrid**.

---

## Notional Pooling — Deep Dive

No fund movement. Bank consolidates balances for interest calculation.

### Single-Currency Notional Pool
- Multiple accounts in same currency.
- Bank's CBS or treasury system aggregates balances daily.
- Net long balance earns interest; net short balance pays interest.
- Long balances offset short balances; net interest only.

### Multi-Currency Notional Pool
- Same as above but across currencies.
- Bank typically converts balances to a reference currency for net calculation.
- Often uses bank's internal rates; no real FX movement.

### Regulatory & Accounting
- **US**: structurally difficult; FDIC + GAAP accounting (no right of offset across legally separate accounts of same entity vs. different entities). Less common.
- **EU + UK**: standard product. Available since long.
- **APAC + MEA**: standard.
- **Cross-border notional pooling**: harder; some jurisdictions don't recognise; some banks offer through Singapore / Hong Kong / Netherlands hubs.

### Why Notional vs Physical
| Notional Wins | Physical Wins |
|---|---|
| No inter-company loans | Real cash where needed |
| No transfer pricing | Liquidity actually accessible |
| Tax cleaner | Operational simpler in some cases |
| Multi-entity, multi-jurisdiction | When jurisdictions allow free physical movement |
| Maintains legal segregation | When concentration is also the operating need |

---

## Virtual Accounts — Deep Dive

A **single physical master account**; the bank's virtual-account platform tracks per-customer-of-customer sub-balances, each with its own account number.

### Architecture
```
┌──────────────────────────────────────────────────┐
│   Bank's Physical Master Account                  │
│   Real balance + reserve treatment               │
└─────────────────────┬────────────────────────────┘
                      │
       ┌──────────────┼──────────────┐
       ▼              ▼              ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│ Virtual Acc 1 │ │ Virtual Acc 2 │ │ Virtual Acc N │
│ Account # X1 │ │ Account # X2 │ │ Account # XN │
│ Balance Y1  │ │ Balance Y2  │ │ Balance YN  │
│ Owner: Cust A│ │ Owner: Cust B│ │ Owner: Cust C│
└──────────────┘ └──────────────┘ └──────────────┘
```

### Key Properties
- Each VA has **a unique account number** that resolves on the payment rail (IBAN-aware, sort-code-aware, etc.).
- Inbound payment to a VA credits the master and the VA sub-ledger simultaneously.
- Outbound payment from a VA debits both.
- The **master is the legal account** at the bank; the VA is a bookkeeping construct.

### Use Cases

| Use Case | Why VAs Win |
|---|---|
| **Fintech sponsor banking** | Sponsor bank holds master; fintech tracks per-end-customer balances |
| **Property management** | Per-property segregation; clear audit |
| **Law firm escrow** | Per-matter segregation; trust accounting compliance |
| **Marketplaces** | Per-seller settlement accounts |
| **Group treasury** | Per-business-unit segregation without separate physical accounts |
| **Insurance** | Per-policy escrow / claims |
| **Real estate developers** | Per-project segregation |
| **Government benefit disbursement** | Per-beneficiary tracking |
| **Universities** | Per-student / department |

### Vendor Stacks
- **Tietoevry Virtual Accounts**.
- **FIS Virtual Accounts**.
- **Cashfac VAM** — virtual account specialist.
- **Bank-built** — typical at tier-1.

### Multi-Currency VAs
Some platforms support VAs in multiple currencies under a single multi-currency master — useful for global merchants / marketplaces.

---

## Intraday Liquidity (Corporate-Side)

Corporate treasurer needs intraday visibility on multi-account positions:

| Need | Bank Service |
|---|---|
| Intraday balance | `camt.052` / MT942 real-time reporting |
| Beneficiary-name resolution | CoP / VoP integration |
| Real-time transaction status | gpi UETR-tracked SWIFT cross-border |
| Liquidity headroom | Available limit visibility |
| Forecast | API or file integration to treasury workstation |

### Treasury Workstations Integration
Modern corporate treasurers use **Treasury Workstations** (TWS) to consolidate multi-bank data:
- **Kyriba** — cloud-native, dominant SaaS.
- **ION Treasury (Reval, Wallstreet)** — large-scale.
- **FIS Trax / Quantum** — long-running.
- **SAP Treasury and Risk Management (TRM)** — SAP-integrated.
- **GTreasury** — mid-market.

Bank-to-TWS connectivity:
- SWIFT MT940 / MT942 / camt.053 / camt.052.
- Direct APIs (REST / SWIFT API).
- BAI2 (US legacy).
- SFTP file drops.

---

## Multi-Bank Cash Management

Large corporates work with **5–50+ banks globally**. Bank-side products that work across banks:

| Product | Notes |
|---|---|
| **SWIFT Multi-Bank reporting** | Aggregating reports from multiple banks via SWIFT |
| **TWS integration** | Treasury workstation aggregates |
| **In-House Bank** | Largest MNCs operate internal banks; banks provide infrastructure |
| **Payment-on-Behalf-Of (POBO) / Receipt-on-Behalf-Of (ROBO)** | In-house bank model for the corporate group |
| **Multi-Bank Concentration** | Cross-bank sweeps + concentration |

---

## Cross-Currency + FX Management

Corporates with multi-currency revenue + cost need bank-side FX:

| Service | Notes |
|---|---|
| **Spot FX** | Immediate conversion at market rate |
| **Forward FX** | Lock rate for future delivery |
| **FX Swaps** | Combined spot + forward |
| **NDF (Non-Deliverable Forward)** | For restricted currencies (INR, CNY, KRW) |
| **Multi-Currency Account** | Single account holding multiple currencies |
| **Auto-FX on inbound foreign currency** | Auto-convert on receipt |

Treasury and FX are tightly integrated — the corporate FX desk routes via the cash-management relationship.

---

## Regulatory Considerations

### US
- Reg D (now-relaxed savings transaction limits).
- Reg J for wires.
- FRB intraday liquidity rules for tier-1 banks.

### UK + EU
- DORA op-resilience.
- PSD2-derived SCA for any retail-touching component.

### Cross-Border
- AML on inter-entity flows.
- Transfer pricing documentation.
- Withholding tax.

---

## Open Questions

- [ ] Confirm pooling product set (single-currency / multi-currency notional + physical).
- [ ] Confirm virtual-account platform + use cases.
- [ ] Confirm multi-bank cash management offering.
- [ ] Confirm TWS integration partnerships.
- [ ] Confirm intraday liquidity reporting capability + SLAs.
