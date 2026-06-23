# Wholesale / Corporate — Product Catalogue Overview

High-level catalogue of wholesale and corporate banking products. Per-category detail in linked files.

---

## Cash Management & Treasury Services — see [treasury-services.md](treasury-services.md)

| Product | product_class | Description |
|---|---|---|
| Integrated Payables | `IntegratedPayables` | Single file in → multi-rail out (ACH, wire, RTP, FedNow, card, check) |
| Integrated Receivables | `IntegratedReceivables` | Multi-channel in → matched against open invoices |
| Lockbox (physical / image / electronic) | `Lockbox` | Cheque collection at scale; image capture; EFT conversion |
| Account Reconciliation Services (ARP) | `ARP_Reconciliation` | Partial / full ARP; positive pay; reverse positive pay |
| Positive Pay | `PositivePay` | Cheque fraud control; payee-match variant |
| ZBA — Zero Balance Account | `ZBA` | Auto-sweep to / from concentration |
| Sweeps | `Sweeps` | EOD / target-balance / threshold sweeps |
| Notional Pooling | `NotionalPooling` | Net-balance interest calc; no physical movement |
| Virtual Account | `VirtualAccount` | Master account with sub-account ledgers |
| Multi-Bank Cash Management | `MultiBankCashMgmt` | SWIFT-driven multi-bank visibility |
| ECR / Account Analysis | `EarningsCreditRate` / `AccountAnalysis` | Compensation model vs explicit fees |

---

## Corporate Lending — see [corporate-lending.md](corporate-lending.md)

| Product | product_class | Description |
|---|---|---|
| Working Capital Facility | `WorkingCapital` / `CashCredit` (IN) | Short-term liquidity |
| Revolving Credit Facility | `RevolvingCreditFacility` | Multi-draw revolving |
| Term Loan | `TermLoan` (bullet / EMI / balloon) | Long-term debt |
| Bridge Loan | `BridgeLoan` | Interim financing |
| Syndicated Loan | `SyndicatedLoan` | Multi-lender |
| Bilateral Loan | `BilateralLoan` | Single-lender |
| Asset-Based Lending | `AssetBasedLending` / `ABL` | Collateralised by inventory / receivables |
| Equipment Finance | `EquipmentFinance` | Equipment-secured |
| Leasing (Operating / Finance) | `Leasing` | Operating + finance lease |
| Project Finance | `ProjectFinance` | Long-tenor, asset-specific cashflow |
| Mezzanine Debt | `MezzanineDebt` | Subordinated junior debt |
| Commercial Real Estate | `CommercialRealEstate` / `CRE` | CRE-secured |
| Leveraged Loan | `LeveragedLoan` | LBO-financing |
| Acquisition / LBO Loan | `LBOLoan` | Acquisition-specific |
| Trade Finance Loans | (under Trade Finance) | Post-shipment / pre-shipment, packing credit |

---

## Trade Finance — see [trade-finance.md](trade-finance.md)

| Product | product_class | Description |
|---|---|---|
| Letter of Credit | `LetterOfCredit` (sight / usance / transferable / back-to-back / revolving) | Documentary credit |
| Standby LC | `StandbyLC` (financial / performance) | Guarantee-like LC |
| Documentary Collection | `DocumentaryCollection` (D/P / D/A) | Bank-handled document exchange |
| Open Account | `OpenAccount` | No documentary bank involvement |
| Supply Chain Finance | `SupplyChainFinance` (payables / receivables) | Buyer / supplier finance |
| Forfaiting | `Forfaiting` | Non-recourse receivables sale |
| Factoring | `Factoring` (recourse / non-recourse) | Receivables sale |
| Bank Guarantee | `BankGuarantee` (bid / performance / advance payment / retention) | Performance / payment assurance |
| Avalised Bill | `AvalisedBill` | Bank-guaranteed bill |
| Trade Receivables Securitisation | `TradeReceivablesSecuritisation` | Off-balance-sheet financing |
| Post-shipment / Pre-shipment Finance | (sub-class of working capital) | Trade-cycle working capital |
| Packing Credit (IN) | (sub-class) | Pre-shipment working capital |

---

## Channels — see [corporate-channels.md](corporate-channels.md)

| Channel | product_class | Description |
|---|---|---|
| Bank Portal (ACCESS / CashPro / CEO / etc.) | per-portal | Web-based corporate banking |
| Host-to-Host (H2H) | `HostToHost` | SFTP / AS2 / MFT file exchange |
| SWIFT for Corporates (S4C) | `SWIFTForCorporates` | Multi-bank SWIFT connectivity |
| Corporate API | `CorporateAPI` | Programmatic integration |
| ERP Connector | `ERPConnector` | SAP, Oracle, NetSuite native plugins |

---

## Customer Segments — see [customer-segments.md](customer-segments.md)

| Segment | Tier | Typical Products |
|---|---|---|
| SME | Sub-tier of WholesaleCorporate | Account, lending, trade-light, digital channels |
| Mid-Corp | Standard tier | Full cash management, lending, trade finance |
| Large Corp | Tier-1 | Bespoke pricing, multi-product, multi-currency |
| MNC | Cross-border tier | Group-wide treasury, multi-jurisdiction |
| FIG | Specialist | Correspondent + custody |
| Sovereign | Specialist | Public-sector specifics |
| NBFI | Specialist | MSB-class diligence |

---

## Cross-Product Concerns

### Pricing
Per-customer matrix:
- Per-transaction fees (often tiered by volume).
- Per-month subscription fees (lockbox, ARP).
- ECR linked to balance maintenance.
- Negotiated rates on lending + trade.
- Volume-based discounts.

### Bundling
Corporate clients often hold 5–15+ products. Bundling discounts:
- Cross-product fee waivers.
- Free transactions above a balance threshold.
- ECR offsets against transaction-fee bills.

### Documentation
Each product has its own:
- Customer agreement / MSA.
- Operating procedure (callback rules, signing rules).
- Pricing schedule.
- Risk disclosure.

### Reporting
Corporate clients consume:
- Real-time intraday (camt.052, MT942).
- End-of-day (camt.053, MT940, BAI2).
- Periodic AA statements (typically monthly).
- Per-product reporting (LC status, lockbox detail, ARP file).

---

## Open Questions

- [ ] Confirm bank's full wholesale product catalogue.
- [ ] Confirm segment-product eligibility matrix.
- [ ] Confirm bundling + pricing framework.
- [ ] Confirm reporting standard per product.
