# Retail Cards — Issuing Operations

Cards is a distinct business inside retail banking — separate platform, separate scheme membership, separate operations. This file covers the **issuing** side; the **acquiring** side typically sits in wholesale (merchant services).

> Scheme-message standards: [../../06-payments/standards/iso-8583.md](../../06-payments/standards/iso-8583.md). Card-rail context: [../../06-payments/rails/](../../06-payments/rails/).

---

## Product Types

| Product | Description | Funding |
|---|---|---|
| **Debit Card** | Linked to a deposit account; immediate debit | Customer's CASA balance |
| **Credit Card** | Revolving credit instrument | Bank-extended credit line |
| **Prepaid Card** | Pre-funded; gift, travel, payroll | Pre-loaded balance |
| **Co-Brand Credit Card** | Bank + partner (airline, retailer); shared rewards | Credit line |
| **Commercial Card** | Issued to business; corporate liability | Negotiated credit |
| **Virtual Card** | Card number only; one-use or recurring | Linked account / credit line |

### Variant Dimensions
- **Network** — Visa, Mastercard, Amex, Discover, JCB, UnionPay, RuPay (IN), Diners.
- **Form** — physical, virtual, contactless, dual-interface, metal.
- **Tier** — Classic, Gold, Platinum, World, Signature, Infinite, World Elite.
- **Authentication** — chip + PIN, contactless, biometric (Apple Pay / Google Pay / device-bound).
- **Region** — domestic-only vs international.
- **Use case** — general purpose, travel, business, fuel, healthcare (HSA / FSA in US), benefit (Direct Express).

---

## Issuing Lifecycle

### Application
- Channel: web, mobile, branch, partner (co-brand merchant).
- Underwriting: credit score, income, debt-to-income, employment.
- Pre-approved offers using bureau + bank data.
- Compliance: KYC + sanctions + PEP.

### Booking & Personalisation
- Card production: plastic, embossing, hot-stamping, chip personalisation.
- Vendor: Giesecke+Devrient, Thales, IDEMIA, Toppan Gravity, CardLogix.
- Mailing: secure mailing house; activation flow on receipt.

### Activation
- IVR / app / web activation.
- First-use authentication.
- PIN setting (often customer self-set via secure channel).

### In-Use Servicing
- Statement generation.
- Reward / cashback accrual.
- Payment processing (auth → clearing → settlement).
- Customer servicing.

### Loss / Theft / Fraud
- Hot-card flagging (immediate channel block).
- Replacement card issuance.
- Dispute initiation.

### Renewal / Expiry
- Auto-renewal (typically 2–5 year card life).
- Re-issue triggers: expiry, breach, customer request, re-personalisation.

---

## Issuer Operations — Authorisation

The issuer host (CBS-linked or dedicated card platform) responds to an ISO 8583 `0100` auth request in milliseconds.

| Check | Description |
|---|---|
| Card status | Active, not expired, not blocked |
| Available balance / credit limit | Sufficient for the transaction + holds |
| Velocity | Within velocity rules per period |
| Fraud score | Pass / decline / step-up |
| SCA / 3DS | Required for CNP transactions per EU PSD2 / UK PSRs |
| Merchant rules | Allowed MCC, allowed country, allowed time |
| Stand-in processing | Scheme-side fallback if issuer host unavailable |

Response: `0110` with response code (DE 39): 00 (Approved), 01 (Refer), 05 (Do Not Honour), 51 (Insufficient Funds), 54 (Expired), 57 (Not Permitted), 61 (Limit Exceeded), 65 (Velocity), 91 (Issuer Unavailable), etc.

---

## Issuer Processors

Common card issuer-processing platforms:

| Platform | Vendor | Notes |
|---|---|---|
| **TSYS** | Global Payments (acq. 2019) | Long-standing tier-1 issuer processor |
| **FIS** | FIS | US issuer processing; Worldpay merchant side |
| **Fiserv First Data** | Fiserv | Acquirer + issuer processing |
| **ACI BASE24-eps** | ACI | Switch + issuer/acquirer; dominant for several decades |
| **Marqeta** | Marqeta | Modern card-issuing API platform for fintechs |
| **Galileo** | SoFi | Card issuer-processor |
| **i2c** | i2c | Modern issuer platform |
| **Equifax / Pismo / Lithic** | Various | Emerging cloud-native processors |
| **Bank-built** | Internal | Common at largest tier-1 issuers |

---

## Tokenisation

Tokens replace the actual PAN (Primary Account Number) for storage + transmission.

### Network Tokens
- Issued by the **scheme** (Visa Token Service, Mastercard MDES, Amex Token Service).
- One-to-one with PAN; lifecycle managed by scheme.
- Used for e-commerce + device-bound payments.
- Survives PAN re-issue (no need to update merchant-of-record on card replacement).

### Device Tokens
- Apple Pay / Google Pay / Samsung Pay device-bound tokens.
- Tokens are unique per device + per PAN; cryptogram-secured.

### PSP / Acquirer Tokens
- Issued by payment processor / PSP (Adyen, Stripe, Braintree).
- Valid within the PSP / acquirer ecosystem only.

### PCI Implication
Tokenisation reduces PCI scope — merchant + PSP storing tokens (not PANs) have a smaller PCI environment.

---

## 3-D Secure (3DS v2)

For card-not-present (e-commerce) authentication. PSD2 SCA-compliant.

### Flow
1. Merchant initiates 3DS via MPI (Merchant Plug-In).
2. DS (Directory Server) routes to issuer's ACS (Access Control Server).
3. ACS authenticates cardholder (challenge or frictionless).
4. Returns CAVV (Cardholder Authentication Verification Value) + ECI (Electronic Commerce Indicator).
5. Authorisation `0100` carries CAVV + ECI; issuer authorises.

### Frictionless vs Challenge
- **Frictionless** — ACS uses risk-based decisioning (device, behaviour) and approves without prompting.
- **Challenge** — customer prompted (OTP, biometric, app push).

### ECI Codes
- ECI=05 (Visa) / ECI=02 (MC): full 3DS success.
- ECI=06 / 01: attempted; liability typically shifts.
- ECI=07 / 00: non-3DS.

---

## Dispute & Chargeback

### Chargeback Flow
1. Customer disputes a transaction with issuer.
2. Issuer files chargeback with scheme.
3. Scheme debits merchant + credits issuer.
4. Merchant has right to **represent** with evidence.
5. Issuer may **second chargeback** if evidence insufficient.
6. Scheme arbitration if unresolved.

### Common Reason Codes
- **Fraud** (10.1–10.5, Visa; 4837–4849, Mastercard).
- **Authorisation** (11.x, 4808 series).
- **Processing Errors** (12.x).
- **Consumer Disputes** (13.x — quality, services not rendered).

### Tools
- **Visa Resolve Online (VROL)** — Visa dispute management.
- **Mastercom** — Mastercard dispute management.
- **Visa CDRN + Verifi Order Insight** — collaboration.
- **Issuer dispute platforms** — case management.

---

## Rewards & Loyalty

| Type | Description |
|---|---|
| **Cashback** | % of spend returned as cash |
| **Points** | Accrual + redemption against catalogue |
| **Miles** | Airline-linked loyalty currency |
| **Tier benefits** | Lounge access, concierge, travel insurance |

Reward economics:
- Funded from interchange (typically 1.5–2% on credit; less on debit due to caps).
- Co-brand: revenue share with partner.
- Reward currency exchange rates vs cash benchmark a key product KPI.

---

## Key Operational Concerns

| Concern | Metric |
|---|---|
| Application approval rate | % of applications approved |
| Activation rate | % of issued cards activated within 30 days |
| First-90-day spend | New-card engagement |
| Spend per active card | Top revenue metric |
| Net Interchange Income | Per-month revenue from interchange |
| Fraud loss ratio | bps of volume |
| Chargeback rate | % of authorised |
| First Payment Default (FPD) | First EMI / payment missed; sign of fraud |
| Dispute resolution time | Days; regulator minimums |

---

## Regulatory Lens

| Regime | Examples |
|---|---|
| **PCI DSS** | Card data security standard; mandatory for any entity storing / processing / transmitting card data |
| **EMVCo** | Chip + 3DS specifications |
| **Reg E (US)** | Consumer protection on unauthorised transactions |
| **Reg Z (US)** | Truth in Lending — credit card disclosures |
| **CARD Act (US)** | Credit card consumer protections |
| **Durbin Amendment / Reg II (US)** | Debit interchange caps + dual-network routing |
| **EU IFR** | Interchange caps (0.2% debit, 0.3% credit consumer) |
| **UK IFR (onshored)** | UK interchange caps |
| **PSD2 + SCA** | EU 3DS mandate |
| **PSR (UK)** | APP fraud reimbursement (applies to FPS/CHAPS, not cards) |
| **RBI Tokenisation Mandate** | IN — only scheme tokens stored, not PANs (since Oct 2022) |

---

## Open Questions

- [ ] Confirm card-issuing platform (in-house vs vendor).
- [ ] Confirm reward / loyalty economics + funding source.
- [ ] Confirm tokenisation strategy (scheme + device + PSP).
- [ ] Confirm dispute management workflow + tools.
- [ ] Confirm 3DS v2 implementation status + frictionless rate.
- [ ] Confirm PCI scope reduction strategy.
