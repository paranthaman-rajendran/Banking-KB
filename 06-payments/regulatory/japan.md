# Japan Payments — Regulatory Requirements

Japan's payments regulation is anchored by the **FSA (Financial Services Agency)** and the **Bank of Japan (BoJ)**, with industry coordination through the **Japanese Bankers Association (JBA)** which operates **Zengin** (the domestic credit transfer rail) and **JBA Net**. The main law is the **Payment Services Act (Funds Settlement Act)** for non-bank PSPs.

> Cross-border SWIFT-heavy and yen-dominated; growing instant-rail focus; CBDC research advanced.

---

## Authorities

| Authority | Scope | Engine Impact |
|---|---|---|
| **FSA (Financial Services Agency)** | Banking + payments supervision | Direct supervisor; licensing under FSA |
| **Bank of Japan (BoJ)** | Central bank; operator of BOJ-NET (RTGS); CBDC research | RTGS adapter; BoJ-supervised |
| **Japanese Bankers Association (JBA)** | Industry body — operates Zengin via Zengin-Net | Scheme rules + connectivity |
| **JFSA-related supervisory units** | Onsite + offsite supervision | Reporting + examinations |
| **JFIU (Japan Financial Intelligence Center)** | FIU; STR submissions | STR pipeline |
| **METI (Ministry of Economy, Trade and Industry)** | Cybersecurity policy; trade-related | Cyber baseline |
| **PPC (Personal Information Protection Commission)** | APPI enforcement | Data privacy |

---

## Core Regulations

### Payment Services Act / Funds Settlement Act (FSA, original 2010 + amendments)
- License regime for **Funds Transfer Service Providers (FTSPs)** — non-bank.
- Three-tier system based on transaction size:
  - **Type I** — up to JPY 1M / txn (no cap).
  - **Type II** — up to JPY 1M / txn (cap on float).
  - **Type III** — small value only (JPY 50,000 cap).
- Customer asset preservation (segregation).
- Reporting + capital requirements.

### Banking Act
- Banking license requirements.
- Sound business operations + risk management.

### Act on Prevention of Transfer of Criminal Proceeds (APTCP)
- AML / CFT for banks + non-bank FTSPs + crypto exchanges.
- CDD, EDD, STR.
- Beneficial ownership.

### Act on the Protection of Personal Information (APPI)
- Japan's GDPR-equivalent.
- 2022 amendments tightened breach reporting + cross-border transfer.
- PPC supervisory authority.

**Engine impact**:
- Customer data handling + breach reporting.
- Cross-border data transfer compliance.

### Sanctions
- Implemented via **Foreign Exchange and Foreign Trade Act (FEFTA)**.
- METI + MOF (Ministry of Finance) administered.
- UN-sourced + autonomous designations.

**Engine impact**:
- JP sanctions list integration + screening.

### Foreign Exchange and Foreign Trade Act (FEFTA)
- Cross-border payment reporting + restrictions.
- Capital flow controls (limited).
- Sanctions implementation.

**Engine impact**:
- Cross-border payment categorisation for FEFTA reporting.

---

## Payment Schemes & Infrastructure

### Zengin System / Zengin-Net
JBA-operated; the workhorse for domestic JPY credit transfers.

- 24x7x365 since Oct 2018 (Zengin More).
- ISO 20022 migration on programme (Zengin System migration target).
- Per-FI connectivity.
- Inter-bank net settlement via BOJ-NET.

### BOJ-NET (BoJ Financial Network)
- RTGS for JPY.
- ISO 20022 migration on programme.
- JGB settlement leg (DvP).

### JNCH (Japan Net Clearing House) + Multi-Bank Clearing
- Cheque / batch + DD.

### Pay-easy
- Bill payment scheme.

### J-Debit
- Bank-issued debit card scheme.

### Major card schemes
- Visa, Mastercard, JCB, Amex, Diners, UnionPay.
- JCB is Japan-origin and dominant in JP-issued cards.

### Mobile / QR
- LINE Pay, PayPay, Rakuten Pay, Merpay — bank-backed + non-bank PSPs.
- J-Coin Pay (consortium).
- QR-code interoperability through industry initiatives.

### CBDC — Digital Yen
- BoJ in advanced "proof-of-concept" + experimental phase (verify current).
- Likely retail + wholesale roadmap.

---

## Operational Risk + Cyber

### FSA Cybersecurity Guidelines for Financial Institutions
- Defines expectations on governance, prevention, detection, response.
- Critical infrastructure obligations.

### Operational Resilience expectations
- FSA-aligned operational resilience guidance evolving (broadly tracking BCBS + UK / EU).

**Engine impact**:
- Documented cybersecurity programme.
- Incident reporting.

---

## What a Japan Payment Engine Must Do — Checklist

| Capability | Driver |
|---|---|
| Zengin / Zengin-Net adapter (ISO 20022-ready) | JBA scheme |
| BOJ-NET RTGS adapter (ISO 20022 migration) | BoJ |
| JNCH + DD + cheque imaging | Domestic scheme |
| Pay-easy bill payment integration | Scheme |
| J-Debit + JCB + other card schemes | Card schemes |
| Mobile / QR PSP integration where relevant | Market structure |
| FSA license-aware activity routing | Funds Settlement Act |
| FTSP customer asset segregation | Funds Settlement Act |
| APTCP-aligned AML / CDD / EDD + STR pipeline to JFIU | APTCP |
| FEFTA cross-border categorisation + reporting | FEFTA |
| Multi-regime sanctions screening (JP + UN + US + EU + UK) | FEFTA + global |
| APPI data handling + cross-border transfer compliance | APPI |
| Cybersecurity programme aligned to FSA guidelines | FSA Cyber |
| Operational resilience + incident reporting | FSA op-res |
| CBDC interface readiness (roadmap) | BoJ pilots |
| Japanese-language disclosures + regulator-facing reports | Local practice |

---

## Sources to Ingest

- Payment Services Act / Funds Settlement Act + amendments
- Banking Act
- Act on Prevention of Transfer of Criminal Proceeds (APTCP)
- Foreign Exchange and Foreign Trade Act (FEFTA)
- Act on the Protection of Personal Information (APPI) + PPC guidelines
- FSA Cybersecurity Guidelines for Financial Institutions
- JBA Zengin System operating rules + Zengin-Net documentation
- BOJ-NET operating rules + ISO 20022 migration plan
- JNCH operating rules
- BoJ CBDC publications + pilot reports
- Internal: JP entity compliance manual, FEFTA reporting pipeline, JFIU STR submission templates

---

## Open Questions

- [ ] Confirm JP entity license + scope (bank vs. FTSP tier).
- [ ] Confirm Zengin + BOJ-NET ISO 20022 migration state and bank's readiness.
- [ ] Confirm APPI cross-border transfer mechanism (consent / adequate-country / SCC-equivalent).
- [ ] Confirm CBDC pilot participation.
- [ ] Confirm major card scheme membership (incl. JCB issuance).
