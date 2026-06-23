# Retail Digital Channels

The customer-facing layer over the CBS. Mobile dominates; everything else is supplementary.

---

## Mobile Banking

The primary channel for most retail customers globally.

| Aspect | Typical State |
|---|---|
| Platforms | iOS native + Android native + responsive web fallback |
| Architecture | Mobile app → API gateway → CBS + payments + cards |
| Authentication | Biometric (FaceID, fingerprint), passcode, device binding |
| Step-up | OTP / push approval for high-risk operations |
| Offline support | Limited; typically requires network |
| Push notifications | Real-time transaction alerts |
| Open Banking | PISP / AISP integration in EU + UK |

### Common Features
- Account balance + statement.
- Funds transfer (intra-bank, NEFT / IMPS / UPI / FPS / Zelle / etc.).
- Bill payment.
- Card management (block, replace, set limits).
- Cheque deposit (image capture).
- Loan / FD / RD opening.
- Customer service chat.
- KYC re-verification.
- Standing instructions.
- Beneficiary management.
- Investment + insurance products (cross-sell).

### Modern Stack Components
- **Front-end**: SwiftUI / Jetpack Compose / React Native / Flutter.
- **API gateway**: bank's API platform (Mulesoft, Apigee, Kong, Tyk, custom).
- **Backend-for-Frontend**: BFF layer aggregating CBS + payment + cards.
- **Security**: device attestation, SSL pinning, root / jailbreak detection.
- **Observability**: AppDynamics, Datadog, New Relic, custom.

### Common Vendors / Platforms
- **Backbase** — digital engagement layer over CBS.
- **Temenos Infinity** — Temenos's digital layer.
- **Finacle Digital Engagement Suite** — Infosys's.
- **Bank-built** — common at tier-1.

---

## Internet Banking

Browser-based desktop / web banking. Declining mobile share but still important.

| Aspect | Typical State |
|---|---|
| Auth | Username + password + 2FA |
| Channel preference | Bulk file uploads, large-value transfers, corporate-ish use |
| Migration | Many banks reducing investment in IB in favour of mobile + responsive |

---

## IVR (Interactive Voice Response)

Voice-channel access for basic enquiries + simple transactions.

| Use Case | Typical Operation |
|---|---|
| Balance enquiry | Pre-authenticated via card + ATM PIN or phone-banking PIN |
| Mini statement | Last N transactions read out |
| Card block | Hot-card flagging |
| Transfer | Pre-registered beneficiary + small value |
| Customer service routing | Branch / agent / specialist routing |

---

## Chatbot / Conversational AI

Increasingly LLM-augmented at the customer-service tier.

| Capability | Notes |
|---|---|
| FAQ-style queries | Account features, fees, hours |
| Simple ops | Balance, statement, branch locator |
| Transactional | Limited; OTP-style authentication needed |
| Complaint intake | Increasingly |
| Hand-off to human | Critical for unhandled cases |

### Notable Bank Bots
- **BofA Erica** — established voice-led assistant.
- **Capital One Eno** — text + voice.
- **Chase chatbot + Cortana-style flows**.
- **HSBC Olivia / Amy**.
- **Citi Citibot**.
- **ICICI iPal / HDFC Eva**.

---

## WhatsApp Banking

Significant in IN, EM markets, where WhatsApp penetration drives adoption.

| Aspect | Typical State |
|---|---|
| Operations | Balance, mini-statement, payment, card mgmt |
| Auth | Phone-binding + OTP step-up |
| Volume | Significant in IN; growing in EM |
| Tech | Vendor (WhatsApp Business API) + bank-built or platform (Jio Haptik, Yellow.ai, Haptik) |

---

## SMS Banking

Legacy but still present.

| Use Case | Notes |
|---|---|
| Balance | Send SMS code, receive response |
| Mini statement | Last N transactions |
| Transaction alerts | Automatic on debit / credit |
| Reduced in modern markets | Replaced by push notifications |

---

## USSD / Feature-Phone Banking

Critical for financial inclusion in EM markets.

| Use Case | Notes |
|---|---|
| `*99#` (India) | UPI on feature phone |
| Mobile money (M-PESA equivalents) | KE, TZ, RW, NG, etc. |
| Adoption | Declining as smartphone penetration grows |

---

## Open Banking Channels (PSD2 + UK + EU + AU Open Banking + US Section 1033)

Third-party-initiated banking.

| Channel | Use Case |
|---|---|
| **PISP** | Third party initiates payment on customer's behalf |
| **AISP** | Third party reads account data |
| **CBPII** | Card-based payment instrument issuer |
| **VRP** | UK Variable Recurring Payments |

The CBS exposes APIs to authorised TPPs via the bank's Open Banking platform (often a dedicated layer, not direct CBS exposure).

---

## Cross-Channel Concerns

### Identity + Authentication
A customer typically authenticates **once** per session and has consistent identity across channels. Session bridging (e.g., start on mobile, complete on web) is increasingly common.

### Channel Routing
The CBS / orchestration layer doesn't usually care which channel; the channel layer enforces channel-specific UX, security, and limits.

### Channel Limits
Typical structure:
- Per-transaction limit (lower on mobile vs branch).
- Daily cumulative limit (varies by KYC tier + customer segment).
- Channel-specific overrides (some products allowed only via specific channels).

### Customer-Driven Channel Preferences
Notifications, statement delivery, OTP destination — customer-configurable.

---

## Key Operational Concerns

| Concern | Metric |
|---|---|
| App availability | 99.9%+ target |
| Login success rate | High; failures track to auth issues |
| Time-to-complete | Per-task (transfer, payment) timing |
| Drop-off rate | At each step in critical journeys |
| Customer Effort Score (CES) | Survey |
| App store rating | 4.5+ ideal; below 4.0 often signals quality issues |
| Channel adoption mix | Per-segment usage by channel |

---

## Open Questions

- [ ] Confirm digital channel platform (vendor / in-house).
- [ ] Confirm cross-channel session bridging.
- [ ] Confirm Open Banking exposure architecture.
- [ ] Confirm conversational AI strategy.
- [ ] Confirm USSD / SMS roadmap for financial inclusion markets.
