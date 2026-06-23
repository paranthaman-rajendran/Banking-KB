# Retail Banking — Operations

Branch, ATM, customer servicing, onboarding, lifecycle events. The plumbing under the digital channels.

---

## Branch Operations

Despite digital migration, branches remain central for:
- Cash transactions (deposit, withdrawal, large value).
- Cheque + draft issuance.
- Sales (advice-driven complex products).
- KYC + onboarding (especially for non-digital-native customers).
- Customer servicing for complex / regulated issues.
- Locker / safe deposit access.

### Branch Roles
| Role | Function |
|---|---|
| Teller / Cashier | Cash, cheque, basic transactions |
| Customer Service Representative | Account servicing, complaint intake |
| Personal Banker | Cross-sell, advisory, premier customer relationship |
| Branch Manager | Operations, sales, risk, P&L |
| Operations / Back Office | Cheque clearing, locker, vault, reconciliation |

### Branch Systems
- Branch teller application (CBS-integrated front end).
- Cash management + ATM driver.
- Cheque + draft issuance.
- Locker management.
- KYC document capture.

---

## ATM Operations

| Function | Notes |
|---|---|
| Cash withdrawal | Issuer-acquirer routing (LINK in UK; STAR/NYCE/Pulse in US; NPCI NFS in IN) |
| Balance enquiry | Real-time |
| Mini statement | Last N transactions |
| Cash deposit | Cash Deposit Machine (CDM); image-capture; provisional vs final credit |
| Cheque deposit | Image capture + Reg CC / equivalent availability |
| Cardless withdrawal | Increasingly via OTP, QR, biometric |
| PIN change | Customer-driven |
| Card upgrade / pickup | Less common |

### ATM Driver & Switch
- **ATM Driver software** — NCR Aptra, Diebold Nixdorf Vynamic.
- **Switch** — ISO 8583-based; routes to internal CBS for on-us, to scheme for off-us.

### Cash Management
- Cash forecasting per ATM.
- Replenishment scheduling (CIT — Cash in Transit).
- Recycling ATMs (deposits fund withdrawals; lower cost).

---

## KYC & Onboarding

### Pre-Account-Opening
- Identification: government ID (Driver's Licence, Passport, Aadhaar, National ID).
- Address verification: utility bill, official document, or system-driven verification.
- Income / occupation: declaration, employer letter, payslip.
- Tax residency: FATCA / CRS self-certification.

### Verification Methods
| Method | Notes |
|---|---|
| In-person | Branch-driven; standard for higher-risk segments |
| Video KYC (V-CIP) | IN-allowed under RBI guidelines; live agent verification |
| eKYC | Aadhaar-based (IN), eIDAS (EU); database-driven |
| Photo + Liveness | AI-driven; document + selfie match |
| Bureau verification | Credit bureau-driven identity check |

### Risk Rating
Per-customer rating: low / medium / high (some banks use 5-tier).
Factors: occupation, geography, source of funds, expected transaction volume, products held.

Drives:
- Periodic KYC refresh cycle (low: 5-yearly, high: yearly or sooner).
- Transaction monitoring threshold.
- Product eligibility.

### EDD Triggers
- PEP designation.
- High-risk geography.
- Cash-intensive business.
- Politically connected.
- Adverse media match.
- Volume / pattern anomaly.

---

## Statement of Account

| Feature | Typical State |
|---|---|
| Frequency | Monthly default; configurable |
| Format | PDF (push, email, in-app); paper on request |
| Content | Per-product per regulator |
| Retention | Customer can download 1–7 years online; longer in archive |
| Tax statements | Annual 1099-INT (US), Form 16A (IN), tax certificate (UK) |

---

## Customer Service & Complaints

### Channels
- Branch (in-person).
- Voice (call centre).
- Chat (web, app).
- Email.
- Social media.

### Complaint Categories
- Transactional (failed / disputed payment).
- Service (slow, unhelpful, error).
- Product (mis-sold, unclear terms).
- Charges (unexpected fee, dispute).
- Fraud (unauthorised activity).

### SLAs (per regulator)
- **UK FCA**: 8 weeks for final response; FOS escalation thereafter.
- **US CFPB**: complaints visible to CFPB; 60-day response standard.
- **IN RBI**: 30-day response; Banking Ombudsman escalation.
- **EU**: per-country; FOS-equivalents.

### Vendor Tools
- **Pega Customer Service**.
- **Salesforce Financial Services Cloud**.
- **Bank-built case management**.

---

## Dispute Resolution

### Transaction Disputes
Reg E (US) defines:
- 10 business days for investigation (extendable to 45 with provisional credit).
- Customer liability tiered: USD 50 / 500 / unlimited.

UK PSRs:
- 1-business-day refund for unauthorised; investigation thereafter.

EU PSD2:
- D+1 refund standard for unauthorised; investigation thereafter.

### Card Chargeback
See [cards.md](cards.md) — scheme-driven; standardised reason codes.

### Fraud Investigation
Coordination across:
- Internal fraud team.
- AML / SAR investigators.
- Law enforcement.
- Customer.
- Counterparty bank.

---

## Dormancy & Inactive Account Lifecycle

### Stage Progression
- **Active** — recent customer-initiated activity.
- **Inactive** — no activity for first threshold (often 6–12 months).
- **Dormant** — no activity for longer (1–3 years per jurisdiction).
- **Unclaimed** — no activity + no contact for very long (5–10 years).
- **Escheated** — transferred to regulator's unclaimed property regime.

### Operations
- Dormancy classification batch (often EOD weekly).
- Customer notification at each stage.
- Reactivation requires customer ID + presence.
- Auto-block of non-customer-initiated debits in some stages.

---

## Deceased Customer Processing

### Notification
- Family / executor notifies bank.
- Bank verifies via death certificate.

### Immediate Actions
- Block customer-initiated debits.
- Continue auto-credits (salary, dividend).
- Cancel cards.
- Freeze online channels.

### Account Disposition
- **Joint Account (Either-or-Survivor mandate)** — straightforward survivor takes ownership.
- **Joint Account (All Sign mandate)** — proves more complex; new mandate or closure.
- **Single-holder** — estate processing, probate (jurisdiction-dependent).
- **Nominee** — claims via nomination (where available).
- **No nominee** — legal heir; documentation required.

### Documentation
- Death certificate.
- Probate / letter of administration.
- Nomination form (where applicable).
- Indemnity (above threshold).
- Joint-holder ID + signature.

---

## Reg E Hot Card / Fraud Block

US-specific (Reg E-grounded):
- Customer reports lost / stolen / fraud → bank must:
  - Investigate within 10 business days.
  - Provide provisional credit if not complete by then.
  - Cap customer liability per timing of notification.

Engineered through:
- Hot-card flag on the card master.
- Real-time block on auth + clearing.
- Replacement card issuance pipeline.

---

## Customer Communications

### Channels
- Email — most communications.
- SMS — transaction alerts + OTP.
- Push — in-app real-time.
- Letter — regulatory + high-value disclosures.
- Voice — outbound from collections + relationship.

### Categories
- Transactional (debit / credit / failure).
- Servicing (statement, fee).
- Relationship (offer, news).
- Regulatory (KYC refresh, tax-related, T&C change).

### Consent + Preferences
- Customer-set preference centre.
- Opt-out for marketing.
- Mandatory categories cannot be opted out.

---

## Compliance + AML Touchpoints in Retail Operations

| Touchpoint | Operation |
|---|---|
| Onboarding | KYC + sanctions + PEP screen |
| Cash deposits | CTR (>USD 10k cash in US); STR thresholds |
| Large outbound | Travel Rule on wires; pattern monitoring |
| Dormancy reactivation | Re-screen + re-verify |
| KYC periodic refresh | Per risk tier |
| Adverse media | Periodic + event-triggered |

---

## Open Questions

- [ ] Confirm branch / ATM operations stack.
- [ ] Confirm V-CIP / eKYC adoption + jurisdictional approval state.
- [ ] Confirm complaint case management platform.
- [ ] Confirm dormancy + escheatment thresholds per jurisdiction.
- [ ] Confirm deceased customer processing workflow + average resolution time.
- [ ] Confirm Reg E / PSRs / equivalent dispute SLA performance.
