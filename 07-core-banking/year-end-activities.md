# Year-End Activities — Core Banking

Year-end is **multiple distinct cycles** colliding in the CBS: **calendar year-end** (Dec 31 — tax + customer reporting), **financial / fiscal year-end** (jurisdiction-specific — accounting close), **tax year** (sometimes a third date), plus **product-specific anniversary cycles**. Each triggers its own batch + reporting + customer-communication chain.

> Companion: [eod-batch-cycle.md](eod-batch-cycle.md) for the daily cycle; this file covers what's **additional** at year-end.
> Status: knowledge scaffolding — must be tailored to the bank's actual year-end calendar.

---

## Three Year-Ends in One Bank

| Year-End | When | Drives |
|---|---|---|
| **Calendar Year-End** | 31 December (global) | Tax certificates, FATCA/CRS, customer statements, escheatment reporting (US) |
| **Financial / Fiscal Year-End** | Jurisdiction-specific (see table below) | Annual GL close, provisioning recompute, regulatory annual reports, capital recompute |
| **Tax Year-End** | Sometimes same as fiscal, sometimes different (e.g., UK personal 5 Apr; HMRC corp varies) | Tax computations, withholding reconciliation, customer tax certs |

### Jurisdictional Fiscal Year-Ends
| Jurisdiction | Fiscal Year-End (Banks Typically) | Notes |
|---|---|---|
| **US** | 31 Dec (most banks; some Sep / Jun) | Calendar = fiscal for most |
| **UK** | 31 Dec or 30 Jun or 31 Mar | Bank choice; HMRC corp tax aligned to bank's |
| **EU** | 31 Dec (most) | Per-country variation |
| **India** | 31 March | Fixed for all banks (RBI mandate) |
| **Japan** | 31 March | Fixed |
| **Singapore** | 31 Dec or 30 Jun (bank choice) | MAS-supervised |
| **Australia** | 30 June | Fixed for banks (APRA) |
| **China** | 31 December | Fixed |
| **Hong Kong** | 31 Dec or 31 Mar | Bank choice |

For an MNC bank with subsidiaries across jurisdictions, multiple fiscal year-ends apply concurrently in the group.

---

## Activity Map (Calendar Year-End — 31 December)

### Customer Tax Reporting

| Output | Jurisdiction | Driven By |
|---|---|---|
| **1099-INT** (Interest Income) | US | IRS; threshold USD 10 (USD 600 for some) |
| **1099-DIV** (Dividend) | US | IRS |
| **1099-B** (Brokerage proceeds) | US | IRS |
| **1099-MISC / 1099-NEC** | US | IRS (relevant for non-deposit fee income) |
| **1098** (Mortgage interest paid) | US | IRS; for tax deduction |
| **1098-T** (Student loan interest) | US | IRS |
| **1098-E** (Education loan interest) | US | IRS |
| **W-2 / W-8 / W-9** related | US | Customer tax-status validation |
| **5498** (IRA contributions) | US | IRS |
| **Form 16A** (TDS on interest) | India | Income Tax Department; quarterly + annual |
| **Form 26AS** support | India | Tax credit visibility |
| **Annual interest certificate** | India | Customer-facing; tax claim |
| **Tax certificate / R185** | UK | HMRC; on request |
| **ISA reporting** | UK | HMRC annual |
| **MMF tax statement** | UK / EU | Per regime |
| **Form 1042-S** | US (for foreign customers) | IRS; withholding on US-source |
| **Annual tax statement** | Per jurisdiction | Per local regime |

### Customer Statements & Disclosures

| Output | Driven By |
|---|---|
| **Annual Account Statement** | Bank policy; some regulators mandate |
| **Annual Privacy Notice (Reg P)** | US — required by GLBA |
| **Annual Fee Disclosure** | Per regulator + contractual |
| **Annual Schedule of Charges** | Per regulator |
| **Annual Interest Rate Notice** | Per regulator |
| **Annual T&C Update** | Bank policy + customer protection rules |

### Cross-Border Tax (Calendar Year-End)

| Filing | Driven By | Timing |
|---|---|---|
| **FATCA** | US IRS — for US persons holding accounts at foreign banks | Annual extract to local tax authority |
| **CRS (Common Reporting Standard)** | OECD — multi-country tax info exchange | Annual extract per signatory |
| **Withholding tax annual reconciliation** | Per jurisdiction | Aligns withheld vs. accrued |

---

## Activity Map (Financial / Fiscal Year-End)

### Annual GL Close

The biggest single CBS activity at FY-end:
1. **Cut-off** for fiscal year postings.
2. **Year-end adjustments** posted (accruals, prepayments, reclassifications).
3. **Closing entries** — close P&L accounts to retained earnings; balance sheet accounts roll forward.
4. **Opening balance creation** for the next fiscal year.
5. **GL → Sub-ledger reconciliation** locked.
6. **Audit-readiness** — locked-down GL for external auditors.

### Provisioning Recompute

| Standard | Activity |
|---|---|
| **IFRS 9 ECL** | Recompute Stage 1 / 2 / 3 provisioning for the loan book; forward-looking model run |
| **CECL (US)** | Annual recompute of life-of-loan expected credit loss |
| **Country-specific (e.g., RBI IRACP)** | Per local provisioning matrix |

### Annual Depreciation / Amortisation
- Fixed asset depreciation closed.
- Intangible amortisation closed.
- IFRS 16 / ASC 842 lease asset roll.

### Loan Book Annual Activities

| Activity | Notes |
|---|---|
| **NPL classification reaffirmation** | All loans re-classified per rules |
| **Annual interest accrual reconciliation** | True-up if any divergence |
| **Annual interest certificate generation** | For customer tax (IN — home loan interest; many jurisdictions) |
| **Covenant testing** | Annual financial covenants tested on year-end financials |
| **Annual facility review** | Each corporate facility reviewed for continued risk-appetite fit |
| **Renewal of revolving facilities** | Annual renewal letters; pricing reset |

### Deposit Book Annual Activities

| Activity | Notes |
|---|---|
| **Annual interest crediting** | Some products credit annually (vs. monthly / quarterly) |
| **Interest reset on floating-rate deposits** | Per-product benchmark roll |
| **ISA / Tax-saver renewal** | UK ISA annual allowance reset (6 Apr); IN tax-saver FD lock-in countdown |
| **Senior citizen status review** | Customer age update may trigger rate uplift |
| **Premature withdrawal penalty review** | Some products waive penalty annually |

### Cards Annual Activities

| Activity | Notes |
|---|---|
| **Annual fee posting** | Per-card; per-product; per-customer-tier waivers |
| **Annual rate notice** | Required disclosures |
| **Reward / point expiry processing** | Annual sweep of unredeemed points |
| **Card renewal cycle** | Cards approaching expiry (typically 2–5 yr lifecycle) re-issued |
| **Tier review** | Reward-tier (Gold/Platinum) reassessed against annual spend / balance |
| **Co-brand reset** | Annual reset of bonus categories |
| **Annual credit limit review** | Risk-based limit reset |

### Cross-Cutting Annual Activities

| Activity | Notes |
|---|---|
| **Annual KYC refresh (high-risk customers)** | EDD-tier customers refreshed annually |
| **Wolfsberg CBDDQ refresh (FIG customers)** | Annual diligence on correspondent / FIG counterparties |
| **PEP screening refresh** | Identifies new PEPs; existing PEP status review |
| **Adverse media scan** | Annual or more frequent for high-risk |
| **Annual entitlement / access recertification** | All system users re-certified |
| **Annual signing rule review (corporate)** | Each corporate's signing matrix confirmed |
| **Annual UBO refresh** | Confirm beneficial owners haven't changed |
| **Annual tax residency confirmation** | FATCA/CRS self-certification refresh as needed |

---

## Regulatory & Compliance Annual Activities

### Capital + Risk

| Activity | Driven By |
|---|---|
| **Pillar 3 / Annual Disclosures** | Basel — public disclosure of risk + capital |
| **ICAAP** | Internal Capital Adequacy Assessment Process |
| **ILAAP** | Internal Liquidity Adequacy Assessment Process |
| **Recovery & Resolution Plan (RRP) update** | "Living wills"; annual refresh |
| **CCAR / DFAST (US)** | Annual stress test submission |
| **EBA stress test inputs** | When called for |
| **BoE stress test inputs (UK)** | When called for |
| **Large Exposures Annual Report** | Per Basel + local regulator |
| **Country / sector concentration reports** | Annual + interim |

### Model Risk

| Activity | Driven By |
|---|---|
| **Annual model validation** | SR 11-7 (US Fed) + equivalent — all material models validated |
| **Model inventory refresh** | Update list of in-use models |
| **Benchmark backtesting** | For credit + market + AML models |

### AML / Sanctions

| Activity | Notes |
|---|---|
| **Annual AML risk assessment** | Bank-wide AML/CFT risk assessment refresh |
| **Annual sanctions risk assessment** | Per OFAC / OFSI / etc. expectation |
| **Annual independent AML testing** | Required for US banks (BSA AML Examination Manual) |
| **Annual SAR/STR pattern analysis** | Retrospective tuning of monitoring |
| **Annual model tuning review (AML monitoring + sanctions screening)** | Tuning records for examiners |

### Operational Resilience

| Activity | Driven By |
|---|---|
| **Annual op-res self-assessment** | FCA/PRA + Fed Interagency op-res policy |
| **Scenario testing** | Annual stress scenarios |
| **Important Business Service (IBS) inventory refresh** | UK FCA/PRA |
| **Critical Third-Party Provider register** | DORA / FCA-PRA + Fed SR letters |
| **Annual TLPT (Threat-Led Penetration Testing)** | For DORA-significant entities (EU) |

### Audit

| Activity | Notes |
|---|---|
| **External audit (FY-end)** | Statutory; UK Big 4 / US PCAOB-registered |
| **SOX 404 testing (US-listed banks)** | Year-round; intensifies at FY-end |
| **Internal audit annual plan delivery** | Coverage report |

---

## Operational Year-End Activities

### Calendar / Holiday Roll

| Activity | Notes |
|---|---|
| **Bank holiday calendar refresh** | Year+1 calendar loaded into CBS (per branch, per country) |
| **Cut-off time updates** | Per-product, per-rail, per-country |
| **Working day calendar** | For accrual basis + settlement |
| **Branch holiday list publication** | Customer-facing |

### Customer Data Hygiene

| Activity | Notes |
|---|---|
| **Address verification batch** | RTS / returned mail processing |
| **Email / mobile validation** | Bounced communications cleanup |
| **Tax residency re-confirmation** | FATCA / CRS self-cert valid? |
| **Marketing consent renewal** | Where required by regulator |

### Dormancy + Escheatment Cycle

| Activity | Notes |
|---|---|
| **Annual dormancy classification batch** | Move accounts to inactive / dormant per threshold |
| **Pre-escheatment customer notification** | Statutory notice before transfer to state |
| **Escheatment file generation** | US states-level filing (per state); IN DEAF Fund transfer; UK Dormant Asset Scheme |
| **Escheated-account closure batch** | Final closure post-handover |

### Standing Instruction Lifecycle

| Activity | Notes |
|---|---|
| **Annual SI review** | Long-standing SIs reviewed for continued validity |
| **SI failure aggregation** | Patterns of failure surfaced |
| **Mandate refresh** | DD mandates that expire annually renewed |

### Account Analysis (Wholesale) Year-End

| Activity | Notes |
|---|---|
| **Annual ECR-rate review** | Per-customer or per-segment |
| **Annual fee schedule reset** | Bilateral renegotiation triggers |
| **Annual relationship profitability review** | RAROC computation per customer |

---

## Indian Fiscal Year-End (31 March) — Specific

India's fiscal year ends 31 March (RBI-mandated). High-volume specific activities:

| Activity | Notes |
|---|---|
| **Income Tax Return data extracts** | For Form 26AS reconciliation |
| **TDS Annual Certificate (Form 16A) generation** | All TDS deductions |
| **Form 15G / 15H validity refresh** | Customer declarations for no-TDS deduction |
| **NPA classification cut-off** | RBI IRACP nuances at year-end |
| **Annual Provisioning recompute** | Per RBI matrix |
| **CRR / SLR balances reconciliation** | Year-end position |
| **NRI account FX revaluation** | Year-end FCNR / NRE valuation |
| **PMLA Compliance Audit submission** | Annual |
| **DEAF Fund transfer** | Dormant accounts > 10 years to RBI |
| **Schedule of Charges annual customer notice** | Per RBI Customer Service guidelines |
| **Annual interest certificate** | Home loan, education loan — for customer's tax claim |

---

## US Calendar Year-End — Specific

| Activity | Notes |
|---|---|
| **1099-series printing + mailing** | January cutoff for IRS deadline |
| **Reg P privacy notice** | If anything has changed |
| **Reg DD savings rate annual notice** | Where applicable |
| **State escheatment reporting** | Per state — different deadlines |
| **CTR aggregation review** | Annual look-back |
| **NACHA Third-Party Sender annual review** | For ACH ODFI obligations |
| **CCAR / DFAST run** | Annual stress submissions |

---

## UK Year-End Specifics

| Date | Activity |
|---|---|
| **31 December** | Calendar year — most banks' fiscal close |
| **5 April** | Personal tax year-end — ISA allowance reset, tax certs |
| **31 March / 30 June** | Corporate fiscal year-end where bank chose |
| **31 July / 31 January** | Self-assessment payment-on-account deadlines |

| Activity | Notes |
|---|---|
| **ISA annual allowance reset (6 Apr)** | New allowance available |
| **Annual tax certificate** | On request |
| **R185 (Trust interest)** | Where applicable |
| **Dormant Asset Scheme** | Annual transfers |
| **FCA Consumer Duty annual board attestation** | Annual sign-off on outcomes |

---

## Failure Modes at Year-End

| Failure | Cause | Impact | Mitigation |
|---|---|---|---|
| **EOD overruns into BOD** | Year-end volume + special jobs | Customer-facing degradation | Schedule + pre-load + dress rehearsal |
| **1099 wrong amount printed** | Sub-ledger / interest accrual error | Customer-facing + IRS correction (1099-C) | Robust pre-validation + spot audit |
| **Annual provisioning model fails** | Data quality issue at FY-end | Audit + regulatory delay | Model + data pipeline pre-checks |
| **FATCA / CRS late filing** | Data gap | Regulatory penalty + customer notification | Mid-year readiness check |
| **Holiday calendar wrong** | Manual update error | Settlement on wrong day | Automated calendar feed + dual-review |
| **GL close incomplete on cut-off** | Open items not cleared | Audit + period-end re-open | Pre-cut-off chase + extended cut-off window |
| **Escheatment list wrong** | Address validation issue | State penalty + customer complaints | Multi-stage verification before sweep |
| **Tax statement currency error** | Multi-currency aggregation issue | Customer mistrust + restatement | Per-currency separate then aggregated |

---

## Operational Cadence (Indicative)

| Month (Calendar) | Activity |
|---|---|
| **Q4** | Year-end planning + dress rehearsals; calendar loaded; communication plans drafted |
| **Mid Dec** | Final pre-checks; customer comms drafted; user-access recert deadline |
| **31 Dec (and following weekend)** | Calendar year-end batch — heaviest |
| **First week of Jan** | 1099 printing + mailing; tax cert distribution; customer-facing close-of-year notices |
| **End Jan** | IRS 1099 deadline (US); state-level deadlines |
| **End Mar (IN)** | Fiscal year-end (IN); equivalent batch in IN entity |
| **Apr** | Annual customer notices; UK ISA reset; tax cert generation |
| **Q2 - Q3** | Stress test submissions; ICAAP / ILAAP / RRP; external audit completion |
| **Q3 - Q4** | Pillar 3 disclosure publication |

---

## Modern CBS vs Legacy at Year-End

| Aspect | Legacy CBS | Modern CBS |
|---|---|---|
| **Cut-off impact** | Long batch window, often degraded customer service | Continuous posting; no blackout |
| **Annual report generation** | Heavy batch; multi-hour | API-driven; on-demand |
| **Multi-jurisdiction year-ends** | Hard — mainframe-era tied to single calendar | Tenant-aware; concurrent |
| **Customer comms** | Print-and-mail dominant | Multi-channel (push, email, in-app) |
| **Data extraction for stress tests** | Manual / bespoke | API + data product |
| **Resilience** | Year-end one-shot risk | Continuous + rehearsed |

---

## Open Questions

- [ ] Confirm bank's fiscal year-end per legal entity.
- [ ] Confirm tax-reporting calendar per jurisdiction.
- [ ] Confirm dormancy + escheatment thresholds + dates per jurisdiction.
- [ ] Confirm annual KYC refresh cadence per risk tier.
- [ ] Confirm year-end dress-rehearsal calendar.
- [ ] Confirm year-end customer-comm content + distribution channels.
- [ ] Confirm GL-close timing + audit-readiness target.
- [ ] Confirm FATCA / CRS extraction pipeline + readiness check.
- [ ] Confirm CCAR / DFAST / equivalent stress test ownership + data pipeline.
- [ ] Confirm cards annual-fee + reward-expiry rules + customer notification path.
