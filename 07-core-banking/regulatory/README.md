# Core Banking — Regulatory & Compliance Activities

Per-jurisdiction deep-dives focused on **what the Core Banking System (CBS) must do** to satisfy regulators. Distinct from the [payments regulatory deep-dives](../../06-payments/regulatory/) — payments rules govern the **money movement**; these rules govern the **customer + account + product + book** layer.

> Scope: USA, UK, Singapore, China (the user-requested set). Other jurisdictions (India, EU, Japan) can be added on the same template.

---

## Navigation

| File | Coverage |
|---|---|
| [usa.md](usa.md) | Fed / OCC / FDIC / CFPB / FinCEN / NYDFS — CIP, Reg E/Z/DD/CC, FDIC, BSA, Call Reports, CCAR, NYDFS Part 500, Section 1033, state banking |
| [uk.md](uk.md) | PRA / FCA / PSR / BoE / FCA Consumer Duty / FSCS — CASS, BCOBS, MLRs, FCA Handbook, op resilience, SS letters |
| [singapore.md](singapore.md) | MAS — Banking Act, Notice 626 AML/CFT, TRM Guidelines, BCM, PDPA, SDIC deposit insurance, FAA, outsourcing Notice 658 |
| [china.md](china.md) | PBoC / NFRA / SAFE / CAC — Bank Account Mgmt, AML Law, CSL/DSL/PIPL, FX administration, deposit insurance, e-CNY |
| [cbs-compliance-matrix.md](cbs-compliance-matrix.md) | Cross-jurisdiction requirement → CBS-feature map |

---

## Why a Separate CBS Regulatory View

Payments regulations focus on the *transaction* (Travel Rule, scheme rules, sanctions screening on the wire). CBS regulations focus on the *relationship + product + book*:

| Domain | Examples |
|---|---|
| **Customer relationship** | KYC, CIP, KYB, UBO, PEP, tax residency |
| **Account** | Account opening rules, disclosures, dormancy, escheatment |
| **Product** | Truth-in-Savings (US Reg DD), Truth-in-Lending (US Reg Z), Consumer Credit (UK CCA / EU CCD) |
| **Deposit insurance** | FDIC (US), FSCS (UK), SDIC (SG), Deposit Insurance Fund (CN) |
| **Customer protection** | Reg E / Reg Z / CFPB / FCA Consumer Duty / MAS FAA |
| **Capital + reporting** | Basel III, Call Reports / FFIEC 031, COREP / FINREP, MAS-prescribed returns |
| **Privacy + cyber** | GLBA + NYDFS Part 500 (US), UK GDPR + DORA-equivalent, PDPA + MAS TRM (SG), CSL / DSL / PIPL (CN) |
| **Tax reporting** | 1099 / 1098 / FATCA / CRS / Form 16A etc. |
| **AML at account-relationship layer** | CIP, EDD, SAR/STR, beneficial ownership registry |
| **Open finance / data rights** | CFPB §1033 (US), Open Banking (UK), SGFinDex (SG), still developing (CN) |

These are **distinct from the payments regulatory burden** — they sit on the CBS, not the payment hub.

---

## CBS Compliance Layers (Universal Pattern)

```
                   Regulator
                       │
                       ▼
    ┌──────────────────────────────────────┐
    │  Compliance Framework (bank-wide)     │
    │  Policies + procedures + 2LoD        │
    └──────────────────────────────────────┘
                       │
                       ▼
    ┌──────────────────────────────────────┐
    │  CBS-Embedded Controls                │
    │  • Customer master (CIF) — KYC/UBO   │
    │  • Account master — disclosures      │
    │  • Product master — interest, fees   │
    │  • GL / sub-ledger — accounting truth│
    │  • Reporting extract — for filings   │
    │  • Audit log — immutable trail       │
    │  • Dormancy / escheatment state mc.  │
    └──────────────────────────────────────┘
                       │
                       ▼
    ┌──────────────────────────────────────┐
    │  Adjacent Systems                     │
    │  AML / Sanctions / Fraud / KYC /     │
    │  Tax-reporting / Regulatory-report /  │
    │  Customer comms / Audit               │
    └──────────────────────────────────────┘
```

The CBS doesn't do compliance alone — but **it owns the source of truth** that compliance systems consume. Wrong customer-tier metadata, missing UBO field, stale tax classification — every one of these is a CBS data-quality problem with regulatory consequence.

---

## Cross-References

- Payments per-jurisdiction regulatory: [../../06-payments/regulatory/](../../06-payments/regulatory/)
- Year-end activities (calendar/fiscal/tax): [../year-end-activities.md](../year-end-activities.md)
- Data classification + audit controls (cross-cutting): [../../03-governance/](../../03-governance/)

---

## Open Questions

- [ ] Confirm in-scope jurisdictions per bank's footprint (this folder starts with US / UK / SG / CN).
- [ ] Confirm CBS instance per jurisdiction + whether group-level CIF is in use.
- [ ] Confirm second-line compliance team's mapping to CBS data domains.
- [ ] Confirm regulatory-reporting pipeline (Axiom / OneSumX / equivalent).
