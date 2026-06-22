# China Payments — Regulatory Requirements

China's payments regulation is **centrally directed**, with the **People's Bank of China (PBoC)** and **State Administration of Foreign Exchange (SAFE)** as the two primary authorities. The CNY/RMB has **onshore (CNY) and offshore (CNH)** dimensions that drive engine design. China has its own end-to-end payment standards (CNAPS, CIPS) and a uniquely strong data + cybersecurity regime (CSL / DSL / PIPL).

> Foreign banks operating in China typically run a separately licensed CN entity with bespoke localised systems.

---

## Authorities

| Authority | Scope | Engine Impact |
|---|---|---|
| **People's Bank of China (PBoC)** | Central bank; payment system operator (CNAPS, HVPS, CIPS); rule-maker | Direct supervisor; operates the rails |
| **NFRA (National Financial Regulatory Administration)** | Banking + insurance supervision (replaced CBIRC + parts of PBoC in 2023) | Bank supervision incl. payments |
| **SAFE (State Administration of Foreign Exchange)** | FX management + cross-border capital controls | Cross-border flow rules + reporting |
| **CAC (Cyberspace Administration of China)** | Cybersecurity + data | CSL / DSL / PIPL enforcement |
| **MIIT** | Telecoms + IT | Tech infrastructure rules |
| **PBoC Anti-Money Laundering Bureau** | AML / CFT | AML compliance |
| **CSRC** | Securities (adjacent for capital flows) | Limited payments scope |

---

## Core Regulations

### Law of the People's Bank of China + Implementing Regulations
- Foundation for payment system oversight.

### Non-Bank Payment Institutions Regulations (2024)
- Implemented December 2023 (effective May 2024).
- Replaces earlier PBoC Order [2010] No.2 on non-bank PSPs.
- Two activity types: **payment processing** + **stored value account**.
- Higher capital + governance requirements.
- Customer fund custody at PBoC-supervised custodian.

**Engine impact**:
- For non-bank PSPs: stricter customer-fund segregation + reporting.

### Cybersecurity Law (CSL, 2017)
- Critical Information Infrastructure (CII) designation for major financial systems.
- Data localisation for CII operators.
- Cybersecurity multi-level protection scheme (MLPS).

**Engine impact**:
- Payment systems classified as CII — data must reside in China.
- MLPS Level 3 / 4 controls.

### Data Security Law (DSL, 2021)
- Data classification + cross-border transfer controls.
- Data export security assessment (regulated).
- Important data + state-related data categories.

**Engine impact**:
- Customer + transaction data cross-border export requires security assessment.
- Data inventory + classification mandatory.

### Personal Information Protection Law (PIPL, 2021)
- GDPR-equivalent for personal data.
- Consent + purpose limitation.
- Cross-border transfer: security assessment, SCC, or PIP certification.
- Individual rights.

**Engine impact**:
- Customer data handling + consent flows.
- Cross-border transfer compliance (significant for foreign banks).

### Anti-Money Laundering Law of the PRC
- AML obligations for FIs + non-bank PSPs.
- STR submission to PBoC AML Bureau.

### Foreign Exchange Regulations
SAFE-administered cross-border controls:
- Annual individual foreign exchange quota (USD 50,000 per person).
- Corporate cross-border flows: trade vs. capital account.
- **Capital account convertibility is limited** — payments tied to genuine trade / approved capital flow.
- Reporting via SAFE's RCPMIS + International Receipt and Payment Statistical System.

**Engine impact**:
- Cross-border payment validation against:
  - Purpose categories (BoP codes).
  - Per-person FX quota for individuals.
  - Corporate trade documentation requirements.
- SAFE reporting integration.

---

## Payment Schemes & Infrastructure

### CNAPS (China National Advanced Payment System)
PBoC-operated; two-tier:

- **HVPS** — High Value Payment System. RTGS, real-time, final.
- **BEPS** — Bulk Electronic Payment System. Deferred net for retail / small value.

### CIPS (Cross-Border Interbank Payment System)
- Launched 2015; phase 2 in 2018.
- CNY cross-border clearing + settlement.
- Direct + indirect participants globally.
- ISO 20022 native.
- Alternative / complement to SWIFT for CNY cross-border.

### IBPS (Internet Banking Payment System)
- Real-time interbank for retail.

### UnionPay
- Card scheme; dominant in CN.
- ISO 8583-based with UnionPay extensions.

### Alipay + WeChat Pay (Tenpay)
- Dominant retail / merchant payment apps.
- Bank-backed; settled through CNAPS underneath.
- Increasingly integrated with cross-border via partnerships.

### e-CNY (Digital RMB)
- PBoC central bank digital currency (CBDC).
- Live in major cities; expanding.
- Wholesale + retail use cases under pilot.

**Engine impact**:
- e-CNY interface readiness for banks participating in pilot.

---

## Cross-Border CNY: Onshore (CNY) vs. Offshore (CNH)

| Aspect | Onshore CNY | Offshore CNH |
|---|---|---|
| Geography | Mainland China | Hong Kong, Singapore, London, Frankfurt, Taipei, Seoul, NY, etc. |
| Convertibility | Limited (capital account controls) | Freely traded |
| Rate | PBoC-fixed midpoint + 2% daily band | Market-determined |
| Settlement | CNAPS + CIPS | CHATS-CNY (HK), other offshore RTGS, SWIFT |
| Bank participation | PBoC-supervised | Offshore central bank-supervised |
| Engine treatment | Strict purpose + quota validation | Standard cross-border (lighter purpose controls) |

**Engine impact**:
- Routing decision: CNH (where offshore acceptable) vs. CNY (when onshore required).
- Different liquidity pools + nostros per side.
- Clear customer disclosure on which side is used.

---

## Sanctions
- China runs its own sanctions list (limited compared to US/EU/UK).
- **Important**: US OFAC sanctions can reach CN-based entities indirectly via USD chain (secondary sanctions effect).
- Hong Kong has its own UNSC implementation framework.

**Engine impact**:
- Multi-regime screening for CNY-touching + USD-touching payments.

---

## What a China Payment Engine Must Do — Checklist

| Capability | Driver |
|---|---|
| CNAPS HVPS + BEPS adapters | PBoC scheme rules |
| CIPS adapter (ISO 20022 native) for cross-border CNY | CIPS rulebook |
| IBPS for retail interbank | PBoC |
| UnionPay scheme adapter (cards) | UnionPay |
| e-CNY interface (pilot / roadmap) | PBoC CBDC |
| BoP code / purpose validation on cross-border flows | SAFE |
| Per-individual FX quota enforcement | SAFE |
| Corporate cross-border documentation validation | SAFE |
| SAFE reporting (RCPMIS) integration | SAFE |
| AML Law / PBoC AML Bureau STR pipeline | AML Law |
| Multi-regime sanctions screening (CN + UN + US + EU + UK) | Mixed |
| CSL Critical Information Infrastructure controls + MLPS Level 3/4 | CSL |
| DSL data classification + cross-border export controls | DSL |
| PIPL consent + cross-border transfer compliance | PIPL |
| CNH offshore vs. CNY onshore routing decision | CN structural reality |
| Data localisation enforcement (CII data in PRC) | CSL |
| Reporting in Chinese language for regulator-facing outputs | Local practice |

---

## Foreign Bank Practical Implications

- Most global tier-1 banks run a **separately licensed CN subsidiary or branch** with localised tech stack.
- Customer data + transaction data of CN residents stays onshore (CSL + DSL + PIPL).
- Engine deployment frequently uses **local cloud or on-prem datacentres** — major hyperscaler offerings via local partners (Alibaba Cloud, AWS Beijing/Ningxia, Tencent, Azure China).
- Cross-border data exchange between CN entity and global head office requires PIPL / DSL compliance + sometimes individual case-by-case security assessment.

---

## Sources to Ingest

- Law of the People's Bank of China
- Non-Bank Payment Institutions Regulations (2024)
- Cybersecurity Law (2017) + implementing rules + MLPS standards
- Data Security Law (2021)
- Personal Information Protection Law (2021)
- Anti-Money Laundering Law of the PRC + implementing measures
- SAFE foreign exchange regulations + BoP code catalogue
- CIPS Operating Rules + Participation Rules
- CNAPS Operating Procedures (PBoC, primarily Chinese language)
- UnionPay scheme rules
- PBoC e-CNY pilot guidance
- PRC sanctions designations + HK UNSC implementing regs
- Internal: CN entity compliance manual, SAFE reporting pipeline docs, data classification + DSL inventory

---

## Open Questions

- [ ] Confirm CN entity license + scope.
- [ ] Confirm data residency posture (CN-only vs. mixed; PIPL cross-border transfer mechanism).
- [ ] Confirm CNH offshore arrangements + counterparty banks.
- [ ] Confirm CIPS participation tier (direct vs. indirect).
- [ ] Confirm e-CNY pilot participation if applicable.
- [ ] Confirm SAFE BoP reporting integration.
