# Core Banking — Taxonomy Detail

Deeper breakdown of the `CoreBanking` domain. Used to drive `sub_domain` and `product_class` metadata values during ingestion.

> Parent: [../01-taxonomy/taxonomy.md](../01-taxonomy/taxonomy.md)

---

## Sub-Domain Codes

| Code | Display Name | Default Sensitivity |
|---|---|---|
| `Retail` | Retail Banking | `Internal` (policy) / `Confidential` (customer data) |
| `WholesaleCorporate` | Wholesale / Corporate Banking | `Internal` (policy) / `Confidential` (customer data) |
| `Platform` | Core Banking Systems & Platform | `Internal` |
| `TreasuryServices` | Treasury Services (wholesale, optional split) | `Confidential` |
| `CorporateLending` | Corporate Lending (optional split) | `Confidential` |
| `TradeFinance` | Trade Finance (optional split) | `Confidential` |

Many large universal banks split `WholesaleCorporate` into the three optional codes above. Choose at sign-off based on the bank's organisational shape.

---

## Product Classes — Retail

### Deposits (`product_class` examples)
- `SavingsAccount` — general purpose interest-bearing
- `CurrentAccount` (UK / IN) / `CheckingAccount` (US) — non-interest, transactional
- `FixedDeposit` (IN) / `CertificateOfDeposit` / `CD` (US) / `BondedDeposit`
- `RecurringDeposit` (IN)
- `MoneyMarketDeposit` / `MMDA` (US)
- `ISA` (UK) — tax-advantaged savings
- `Sparbuch` (DE) — passbook
- `NRE`, `NRO`, `FCNR` (IN, NRI variants)
- `MinorAccount`, `JointAccount`, `BasicSavingsBankDepositAccount` (BSBDA — IN)
- `EscrowAccount`

### Lending (`product_class` examples)
- `HomeLoan` / `Mortgage`
- `MortgageRefinance` / `HELOC` (US — Home Equity Line of Credit)
- `PersonalLoan` / `UnsecuredPersonalLoan`
- `AutoLoan` / `VehicleLoan`
- `EducationLoan` / `StudentLoan`
- `GoldLoan` (IN)
- `CreditCard` (lending product perspective)
- `OverdraftFacility`
- `MSMELoan` / `SmallBusinessLoan`
- `LoanAgainstProperty` (LAP)
- `BuyNowPayLater` / `BNPL`

### Cards (`product_class` examples)
- `DebitCard`
- `CreditCard`
- `PrepaidCard`
- `CoBrandCard` (e.g., airline / retailer)
- `BusinessCard` / `CommercialCard`
- `VirtualCard`

### Channels & Operations
- `MobileBanking`
- `InternetBanking`
- `BranchTeller`
- `ATM`
- `IVRBanking`
- `KYCOnboarding`
- `DormantAccountManagement`
- `DeceasedCustomerProcessing`

---

## Product Classes — Wholesale / Corporate

### Cash Management & Treasury Services
- `IntegratedPayables`
- `IntegratedReceivables`
- `Lockbox` (physical, image, electronic)
- `ARP_Reconciliation`
- `PositivePay` / `PayeeMatchPositivePay`
- `ZBA` — Zero Balance Account
- `Sweeps` (Operating → MMA, end-of-day, target balance)
- `NotionalPooling` (single-currency, multi-currency)
- `VirtualAccount` (master-account-with-segregated-customer-of-customer ledgers)
- `EarningsCreditRate` / `AccountAnalysis`
- `ConcentrationAccount`
- `MultiBankCashMgmt`

### Lending (`product_class` examples)
- `WorkingCapital` / `CashCredit` (IN) / `RevolvingCreditFacility`
- `TermLoan` (bullet, EMI, balloon)
- `BridgeLoan`
- `SyndicatedLoan`
- `BilateralLoan`
- `AssetBasedLending` / `ABL`
- `EquipmentFinance`
- `Leasing` (operating, finance)
- `ProjectFinance`
- `MezzanineDebt`
- `CommercialRealEstate` / `CRE`
- `LeveragedLoan`
- `Acquisition` / `LBOLoan`

### Trade Finance
- `LetterOfCredit` (sight, usance, transferable, back-to-back, revolving)
- `StandbyLC` (financial, performance)
- `DocumentaryCollection` (D/P, D/A)
- `OpenAccount`
- `SupplyChainFinance` (payables, receivables)
- `Forfaiting`
- `Factoring` (recourse, non-recourse)
- `BankGuarantee` (BG — bid bond, performance, advance payment, retention)
- `AvalisedBill`
- `TradeReceivablesSecuritisation`

### Corporate Channels
- `ACCESS` (JPMC)
- `CashPro` (BofA)
- `CEO` (Wells Fargo)
- `CitiDirect` (Citi)
- `BarclaysNet`, `HSBCnet`, `DBSIDEAL`, etc.
- `HostToHost` (SFTP / AS2 / MFT)
- `SWIFTForCorporates` / `S4C`
- `CorporateAPI`
- `ERPConnector` (SAP, Oracle ERP)

### Segments
- `SME` — Small & Medium Enterprise
- `MidCorp` — Middle Market
- `LargeCorp` — Large Corporate
- `MNC` — Multinational Corporation
- `FIG` — Financial Institutions Group
- `Sovereign` — Sovereign / Public Sector
- `NBFI` — Non-Bank Financial Institution

---

## Product Classes — Platform

- `EODBatchCycle` / `BODProcessing` — daily batch cycle (see [eod-batch-cycle.md](eod-batch-cycle.md))
- `FinacleCBS` (Infosys)
- `FlexcubeCBS` (Oracle)
- `T24Transact` (Temenos)
- `BaNCS_CBS` (TCS)
- `FIS_Profile` / `FIS_Systematics` / `FIS_Horizon`
- `Fiserv_DNA` / `Fiserv_Premier` / `Fiserv_Signature`
- `JackHenry_SilverLake`
- `Mambu`
- `ThoughtMachine_Vault`
- `10x_Banking`
- `SAP_BankingServices`

---

## Cross-Sub-Domain Linkage (Examples)

| Sub-Domain | Linked Field | Linked Sub-Domain | Use Case |
|---|---|---|---|
| `Retail / SavingsAccount` | `accountNumber` | `Payments / DomesticIN-NEFT` | NEFT debit postings to the savings account |
| `WholesaleCorporate / ZBA` | `accountHierarchy` | `Payments / Sweeps` | End-of-day sweep automation |
| `WholesaleCorporate / LetterOfCredit` | `LCNumber` | `Payments / SWIFT-MT700` | LC issuance over SWIFT |
| `Retail / CreditCard` | `cardId` | `Payments / Cards-ISO8583` | Auth + clearing flows |
| `Platform / FlexcubeCBS` | `accountSchema` | `Retail / *` and `WholesaleCorporate / *` | Posting + balance maintenance |

---

## Open Questions

- [ ] Confirm whether bank treats Cards as part of Retail (typical) or as a separate sub-domain (when issuing is a stand-alone P&L).
- [ ] Confirm whether Wealth Management private-bank account products belong here or in Wealth sub-domain.
- [ ] Confirm whether `Platform` belongs as a sub-domain of `CoreBanking` or as `TechPlatform` top-level (currently both).
- [ ] Confirm sensitivity-tier defaults (some Wholesale customer data may need `Restricted` rather than `Confidential`).
