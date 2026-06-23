# Trade Finance

Bank-intermediated cross-border + domestic trade. **Letters of Credit, Standby LCs, Documentary Collections, Open Account + Supply Chain Finance, Bank Guarantees.** Multi-billion-USD revenue line at tier-1 universal banks; deeply regulated; ICC rules-governed; high TBML (Trade-Based Money Laundering) exposure.

> Major gap area identified in [../../gap-analysis-tier1-bank.md](../../gap-analysis-tier1-bank.md). Read this if your bank archetype includes trade finance.

---

## Why Trade Finance Exists

International trade introduces:
- **Performance risk** — buyer may not pay; seller may not ship.
- **Country / political risk**.
- **Currency risk**.
- **Information asymmetry** — buyer + seller often don't know each other.

Trade finance instruments **transfer risk to banks** in exchange for fees + financing margin.

---

## Letter of Credit (LC)

A bank's **conditional payment promise** — bank pays the seller on presentation of compliant documents.

### Standard Flow
1. Buyer + Seller agree contract; payment via LC.
2. Buyer (Applicant) approaches its bank (Issuing Bank).
3. Issuing Bank issues LC in favour of Seller (Beneficiary), often through Seller's bank (Advising Bank).
4. Seller ships goods; presents documents (invoice, BL, packing list, certificate of origin, insurance, etc.) to its bank.
5. Documents flow to Issuing Bank.
6. If documents **comply with LC terms**, Issuing Bank pays.

### Key Roles

| Role | Function |
|---|---|
| **Applicant** | Buyer; requests LC |
| **Issuing Bank** | Bank that issues + assumes payment obligation |
| **Beneficiary** | Seller; receives payment |
| **Advising Bank** | Seller's bank; advises LC validity |
| **Confirming Bank** | Adds its own undertaking to pay (typically Seller's bank) |
| **Nominated Bank** | Authorised by Issuing Bank to act (pay, negotiate) |
| **Reimbursing Bank** | Pays Nominated/Confirming Bank under reimbursement instructions |

### LC Variants

| Variant | Description |
|---|---|
| **Sight LC** | Payable at sight on document compliance |
| **Usance / Deferred LC** | Payable at a future date (30/60/90/180 days from sight or BL date) |
| **Transferable LC** | Beneficiary can transfer rights to a 2nd beneficiary |
| **Back-to-Back LC** | Second LC issued backed by first; for intermediaries |
| **Revolving LC** | Auto-renews for ongoing trade |
| **Red Clause LC** | Allows advance to beneficiary before shipment |
| **Green Clause LC** | Like red, but with goods-warehoused condition |
| **Standby LC (SBLC)** | Performance / financial guarantee; payment only on default |

### Governing Rules
- **UCP 600** (Uniform Customs and Practice for Documentary Credits, ICC) — the universal LC rulebook. ICC Publication 600.
- **ISBP** (International Standard Banking Practice, ICC) — document examination standards. Companion to UCP 600.
- **eUCP** — electronic LC version.
- **URR 725** — Uniform Rules for Reimbursement.

---

## Standby Letter of Credit (SBLC)

Functions like a **guarantee** but issued under LC mechanics. Typically not drawn — invoked only on default.

### Variants
- **Financial SBLC** — guarantees financial obligation (e.g., loan repayment).
- **Performance SBLC** — guarantees performance (e.g., construction contract completion).
- **Bid Bond / Tender SBLC** — supports tender bids.
- **Advance Payment SBLC** — guarantees repayment of advance.
- **Direct-Pay SBLC** — designed to be drawn (rare).

### Governing Rules
- **ISP98** (International Standby Practices, ICC Publication 590) — SBLC-specific.
- **UCP 600** — can also govern SBLCs (specified at issuance).
- **URDG 758** — Uniform Rules for Demand Guarantees; sometimes used for SBLCs.

---

## Documentary Collection

Bank-handled exchange of shipping documents against payment (D/P) or acceptance (D/A). **No bank payment undertaking** — bank acts as agent only.

### Variants
| Variant | Description |
|---|---|
| **D/P (Documents against Payment)** | Buyer must pay to receive documents |
| **D/A (Documents against Acceptance)** | Buyer accepts a draft (committing to pay on future date) to receive documents |
| **Clean Collection** | Financial documents only (no commercial docs) |
| **Documentary Collection** | Commercial + financial documents |

### Governing Rule
- **URC 522** (Uniform Rules for Collections, ICC Publication 522).

### Why Use It
- Cheaper than LC (no bank payment undertaking).
- Still gives seller control of goods until conditions met.
- Suitable where trust between parties is moderate.

---

## Open Account + Supply Chain Finance (SCF)

Increasingly the dominant trade model — buyer pays seller after shipment with no bank intermediation in the payment promise. But banks layer financing on top.

### Open Account
- Buyer + Seller transact directly.
- No bank payment instrument.
- Highest TBML risk surface.
- 80%+ of global trade volumes.

### Supply Chain Finance
Bank finances either the buyer's payables or the seller's receivables:

| Variant | Description |
|---|---|
| **Payables Finance / Reverse Factoring** | Bank pays supplier early on buyer's approved invoice; buyer pays bank later at agreed extended terms |
| **Receivables Finance / Factoring** | Bank pays supplier early; supplier sells receivable to bank |
| **Dynamic Discounting** | Buyer offers early-payment discount; bank funds if buyer chooses |
| **Distributor Finance** | Bank finances distributors' purchases from the corporate |

### Vendor Stacks
- **PrimeRevenue**.
- **C2FO**.
- **Taulia** (SAP).
- **Demica**.
- **Bank-built** at tier-1.

---

## Bank Guarantees (BG)

Bank's undertaking to pay if its customer defaults on an obligation.

### Variants
| Variant | Description |
|---|---|
| **Bid Bond / Tender Guarantee** | Backs tender bid |
| **Performance Guarantee** | Backs contract performance |
| **Advance Payment Guarantee** | Backs advance refund if not delivered |
| **Retention Money Guarantee** | Backs retention release |
| **Payment Guarantee** | Backs payment obligation |
| **Customs / Tax Guarantee** | Backs duty / tax payment to government |

### Governing Rules
- **URDG 758** (Uniform Rules for Demand Guarantees, ICC).
- **National civil codes** — many jurisdictions add specific requirements.

### Issuance Mechanics
- Often issued by SWIFT **MT 760 (Issue of Guarantee)** + amendments via MT 767.
- Or paper-based.
- Can be direct (issuing bank to beneficiary) or indirect (via a local bank).

---

## Trade Finance Loans

Specific working-capital products linked to trade cycle:

| Product | Description |
|---|---|
| **Packing Credit (Pre-shipment Finance)** | Funds production before shipment; secured by export order |
| **Post-shipment Finance** | Funds gap between shipment + buyer payment; LC-backed or clean |
| **Buyer's Credit** | Loan to overseas buyer to import from your country |
| **Supplier's Credit** | Extended payment terms from overseas supplier; bank finances |
| **Trust Receipt** | Bank releases goods to importer who sells before paying bank |
| **Avalised Bill** | Bank-guaranteed (by aval) bill of exchange |
| **Negotiation** | Bank advances funds against LC documents pending settlement |
| **Forfaiting** | Non-recourse purchase of trade receivables |
| **Factoring (Export Factor)** | Non-bank receivables financing |

---

## SWIFT MT 7-series Messages

Trade finance is heavily SWIFT MT-based; some migrating to ISO 20022.

| MT | Purpose |
|---|---|
| **MT700** | Issue of Documentary Credit (LC issuance) |
| **MT701** | Issue continuation |
| **MT707** | Amendment to LC |
| **MT710** | Advice of Third Bank's / Non-Bank's LC |
| **MT720** | Transfer of LC |
| **MT730** | Acknowledgement |
| **MT732** | Advice of Discharge |
| **MT734** | Advice of Refusal |
| **MT740** | Authorisation to Reimburse |
| **MT742** | Reimbursement Claim |
| **MT750** | Advice of Discrepancy |
| **MT752** | Authorisation to Pay, Accept or Negotiate |
| **MT754** | Advice of Payment/Acceptance/Negotiation |
| **MT760** | Issue of Guarantee / Standby LC |
| **MT767** | Amendment of Guarantee / SBLC |
| **MT768** | Acknowledgement of Guarantee Message |
| **MT769** | Advice of Reduction or Release |
| **MT770** | Advice of Charges, Interest and Other Adjustments |
| **MT798** | Trade Envelope (corporate-to-bank trade messaging) |

ISO 20022 successor families exist (`tsmt`) but adoption is uneven; most trade finance remains SWIFT MT-driven.

---

## Industry Standards Bodies

| Body | Role |
|---|---|
| **ICC (International Chamber of Commerce)** | Publisher of UCP 600, ISBP, ISP98, URDG 758, URC 522, eUCP, Incoterms |
| **BAFT (Bankers Association for Finance and Trade)** | Industry advocacy + standards |
| **SWIFT** | Network + MT/MX standards |
| **ITFA (International Trade and Forfaiting Association)** | Forfaiting + secondary market |
| **FCI (Factors Chain International)** | Factoring industry |

---

## TBML — Trade-Based Money Laundering

Trade is a major ML / TF channel. Typologies:

| Typology | Mechanism |
|---|---|
| **Over-invoicing** | Over-paying for goods to move value out |
| **Under-invoicing** | Under-paying to move value in |
| **Multiple invoicing** | Same goods invoiced repeatedly |
| **Phantom shipments** | Documents without goods |
| **Misdescribed goods** | Goods don't match description |
| **Multiple borrowing on same goods** | Same goods used for multiple financings |
| **Round-trip transactions** | Goods cycle back to origin |

### Bank Controls
- KYC + KYB on both buyer + seller.
- Documentary scrutiny (UCP 600 ISBP).
- Price benchmarking against market.
- Vessel + shipping verification (IHS Markit, Lloyd's List).
- Sanctions screening on all parties + vessels + goods + ports.
- Dual-use goods controls.
- TBML-specific risk-scoring engines.

### Vendor Tools
- **Surecomp** — trade finance platform with TBML controls.
- **CGI Trade360** — trade finance platform.
- **Finastra Fusion Trade Innovation** — Finastra's trade product.
- **Comarch Trade Finance**.
- **Bank-built** TBML scoring.

---

## Sanctions in Trade

Multi-layered:
- **Parties** — applicant, beneficiary, advising bank, confirming bank, all intermediaries.
- **Goods** — sanctioned goods (military, dual-use, oil from sanctioned origin).
- **Vessels** — sanctioned ships (Russia, Iran-shadow fleet).
- **Ports** — sanctioned ports.
- **Countries of origin / destination / transhipment**.
- **Insurance** — sanctioned insurers (Russian / Iranian).

Sanctions hits in trade can be **complex** — needing OFAC / OFSI / EU specific licences for wind-down or humanitarian goods.

---

## Trade Finance Platforms

| Platform | Vendor | Notes |
|---|---|---|
| **Surecomp** | Surecomp | Long-standing leader |
| **CGI Trade360** | CGI | Multi-tenant SaaS option |
| **Finastra Fusion Trade Innovation** | Finastra | Pairs with Finastra GPP |
| **Comarch Trade Finance** | Comarch | EU + APAC presence |
| **Oracle Banking Trade Finance** | Oracle | Pairs with Flexcube + OBPM |
| **Misys (legacy now Finastra)** | Finastra | Long-running tier-1 |
| **Bank-built** | Internal | Common at tier-1 |

---

## Distributed Ledger Trade Initiatives (Mostly Wound Down or Pivoted)

- **we.trade** — wound down 2022.
- **Marco Polo** — wound down 2023.
- **TradeLens** — wound down 2023.
- **Komgo** — pivoted to commodity.
- **Contour** — pivoted.

Lesson: trade finance digitisation is structurally hard; standards + party-coordination friction is the real blocker, not blockchain.

---

## Open Questions

- [ ] Confirm bank's trade finance product set.
- [ ] Confirm trade finance platform (Surecomp / CGI / Finastra / OBTF / Comarch / built).
- [ ] Confirm SCF arrangements + partners.
- [ ] Confirm TBML controls + scoring engine.
- [ ] Confirm trade-side sanctions playbook.
- [ ] Confirm ISO 20022 migration plan for trade messages.
