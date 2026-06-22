# Top Global Payment Processing Engines

The "payment engine" / "payment hub" sits at the centre of [systems-landscape.md](systems-landscape.md). It holds the canonical payment record, orchestrates pre-processing, decides routing, transforms format, and tracks status. This document inventories the vendor products most commonly seen in tier-1 banks.

> Disclaimer: vendor product positioning shifts. Treat below as a directional reference; confirm with the vendor before quoting versions or capabilities.

---

## Selection Lens

When a tier-1 bank evaluates a hub, the recurring criteria are:

1. **ISO 20022 nativeness** (not adapter-bolted) — increasingly table-stakes.
2. **Rail breadth** — does it cover the bank's geographies + retail / wholesale / cards?
3. **Real-time throughput** — sub-second budgets at peak TPS.
4. **Catalogue of pre-integrated controls** — fraud, sanctions, AML.
5. **Cloud-native posture** — multi-region active-active, container-native.
6. **Operational tooling** — investigation UX, repairs, replay.
7. **TCO** — license + ops + run-rate cost.
8. **Implementation track record** at similar-size banks.

---

## Tier-1 Hubs / Engines

### Finastra Global PAYplus (GPP) / Fusion Payments
- Origin: D+H + Misys merger → Finastra (2017).
- Stack: ISO 20022 native (multi-decade); rail-aware routing; integrated control orchestration; large global rail library.
- Strong in: cross-border SWIFT, EU SEPA, US Fed + RTP, MEA, APAC.
- Variants: GPP SmartOps (operations), GPP RTP-specific deployment, Fusion Payments-as-a-Service.
- Typical deployment: large banks; multi-year programmes.
- **Deep dive**: [vendors/finastra-gpp.md](vendors/finastra-gpp.md)

### Volante Technologies — VolPay + Volante Payments-as-a-Service
- Origin: NJ-based; founded 2001 around financial messages.
- Stack: ISO 20022 native; very flexible message-transformation core; growing cloud-native PaaS footprint.
- Strong in: payments modernisation, FedNow / RTP adoption, low-code message work.
- Notable: chosen by several US banks for FedNow launches; UK + EU presence growing.

### ACI Worldwide — ACI Universal Payments (UP) / Money Transfer System (MTS) / BASE24
- Origin: long history in payments (BASE24 cards since the 1980s).
- Stack:
  - **ACI Money Transfer System (MTS)** — workhorse for wholesale wires and ACH.
  - **ACI UP Real-Time Payments** — RTP / FedNow / SCT Inst / others.
  - **ACI UP Immediate Payments** — instant rail core.
  - **BASE24-eps** — issuer / acquirer card switch.
  - **ACI Enterprise Banker** — corporate channels.
  - **ACI Fraud Management** — built-in fraud.
- Strong in: cards, wholesale wires, instant rails.
- Notable: extremely broad payments stack from a single vendor.

### FIS — Open Payment Framework (OPF) + Payments One Hub
- Origin: FIS has grown by acquisition (eFunds, Metavante, SunGard, Worldpay).
- Stack: OPF as the modern hub; integrates with FIS's CBS (Profile, Systematics, Horizon).
- Strong in: US banks (regional + large), UK FPS connectivity, EU.
- Notable: also offers payment-processing-as-a-service for community + regional FIs.

### Fiserv — Payments Hub (PEP+) and Frontier
- Origin: Fiserv (pre-FIS-merger competitor; serves many US banks).
- Stack: PEP+ for ACH and wholesale; Frontier for reconciliation; Now Network / NOW Mobile for real-time.
- Strong in: US ACH + wires, regional banks, credit unions.

### IBM — Financial Transaction Manager (FTM)
- Stack: configurable transaction-orchestration platform — payment hub + ISO 20022 transformation + clearing connectivity.
- Strong in: highly customised tier-1 bank deployments; on-prem + IBM Cloud.
- Notable: often paired with IBM Sterling for file workflows + WebSphere MQ for messaging.

### Temenos — Payments Hub (T24 Payments / Transact Payments)
- Stack: integrated with Temenos T24 / Transact CBS; cloud-native variant on Temenos Banking Cloud.
- Strong in: Temenos-CBS banks; EU + APAC mid-tier + tier-1 modernisation.

### Oracle — Banking Payments (OBPM, within Oracle Banking Suite)
- Stack: ISO 20022 native; integrated with Oracle Flexcube CBS + Oracle FCCM (Sanctions/AML); deployable standalone.
- Strong in: Flexcube banks; MEA, India, APAC; growing in EU + Americas.
- Tech: Oracle DB + WebLogic + Java EE; OCI-native cloud direction.
- **Deep dive**: [vendors/oracle-obpm.md](vendors/oracle-obpm.md)

### TCS BaNCS — Payments
- Stack: part of TCS BaNCS suite, deeply integrated with BaNCS CBS.
- Strong in: tier-1 Indian banks, large global deployments (e.g., State Bank of India), APAC.

### Infosys Finacle — Payments
- Stack: integrated with Finacle CBS, ISO 20022-native modules; Connect24 + Finacle Payments.
- Strong in: India + MEA + APAC; growing globally.

### Bottomline Technologies — Universal Aggregator + PT-X + Cyber Fraud and Risk Management
- Stack: corporate-channel + SWIFT service-bureau heritage; modern payments-as-a-service offerings.
- Strong in: corporate banking, SWIFT service-bureau use cases, mid-market.

### Pelican AI — Pelican Payments
- Stack: AI-led payment processing with built-in NLP for repairs and sanctions disambiguation.
- Strong in: ISO 20022 transformation and STP optimisation.

### Form3
- Origin: London-based cloud-native challenger (2016).
- Stack: cloud-native payment processor with pre-integrated FPS / Bacs / SEPA / SEPA Inst / FedNow / RTP / SWIFT connectivity.
- Strong in: UK and EU; challenger banks + tier-1 modernisation programmes (e.g., LBG mandate).
- Notable: API-first delivery model, run as a managed service.

### SmartStream — TLM Payments / SmartStream Air
- Stack: known for reconciliation; growing payment-processing footprint and AI ops.
- Strong in: post-payment recon + intraday liquidity (TLM Intraday Liquidity is widely used).

### Mambu / Thought Machine / 10x — Cloud-Native CBS with Payment Modules
- Mambu, Thought Machine Vault, and 10x are cloud-native cores that increasingly include payment workflows.
- Strong in: neobank greenfields + tier-1 modernisation programmes.

### SWIFT — Transaction Manager (TM)
- Operator-side service (not a bank-side hub, but the centre of CBPR+ MX in-flight).
- All banks consuming CBPR+ MX cross-border have to design around TM.

### IBM Sterling B2B + IBM ACE + IBM MQ
- Often used as the **integration / messaging spine** behind the hub.
- Not a hub itself; pairs with FTM or similar.

---

## Cards-Specific Processing Engines

These are distinct from the general payment hub because card processing is rate-controlled by scheme membership and ISO 8583.

| Product | Vendor | Notes |
|---|---|---|
| ACI BASE24-eps | ACI Worldwide | Issuer + acquirer + ATM switch; dominant for several decades |
| TSYS (now Global Payments) | Global Payments | Large card issuer processor |
| FIS / Worldpay | FIS | Acquirer-side dominant |
| Fiserv First Data | Fiserv | Acquirer + merchant processing |
| Adyen | Adyen | Global acquirer + issuing platform; merchant-facing |
| Stripe | Stripe | Acquirer + issuer-as-a-service for fintech |
| Marqeta | Marqeta | Modern card issuing platform |
| Galileo | SoFi | Card issuer-processor |
| Worldline / Equens | Worldline | EU acquirer + issuer processing |
| Nets | Nexi Group | Nordic + EU acquirer + processor |

---

## Sanctions / Compliance Specialists Often Embedded with the Hub

| Product | Vendor | Note |
|---|---|---|
| Fircosoft Continuity / Fircosoft Trust | Accuity / LexisNexis | Most widely deployed sanctions filter in tier-1 banks |
| World-Check + screening | Refinitiv (LSEG) | List provider + screening integrations |
| ComplyAdvantage | ComplyAdvantage | Cloud-native AML + sanctions; common in challengers |
| Oracle FCCM | Oracle | Integrated compliance suite |
| NICE Actimize | NICE | Fraud + AML + compliance integrated suite |

---

## Fraud Specialists Often Embedded

| Product | Vendor | Note |
|---|---|---|
| Featurespace ARIC | Featurespace | Real-time behavioural — well suited to instant rails |
| FICO Falcon | FICO | Card fraud heritage; broader payments since |
| NICE Actimize Xceed / IFM | NICE | Integrated fraud + AML |
| SAS Fraud Management | SAS | Enterprise grade |
| BioCatch | BioCatch | Behavioural biometrics |
| ThreatMetrix | LexisNexis | Device + identity intelligence |

---

## Open Banking / API Front Ends

| Product | Vendor | Note |
|---|---|---|
| Token.io | Token.io | Open Banking PISP / AISP infrastructure |
| Yapily | Yapily | Open Banking aggregator (EU + UK) |
| Tink (Visa) | Visa | Aggregator + initiation |
| TrueLayer | TrueLayer | Aggregator + initiation |
| Plaid | Plaid | US + EU + UK; aggregator |
| Salt Edge | Salt Edge | Aggregator |

---

## Reconciliation Specialists

| Product | Vendor | Notes |
|---|---|---|
| SmartStream TLM Reconciliations Premium | SmartStream | Industry standard for nostro + cards + securities |
| FIS IntelliMatch | FIS | Multi-format matching |
| Fiserv Frontier Reconciliation | Fiserv | Strong in Americas |
| Broadridge Reconciliation | Broadridge | Securities + payments |
| Duco | Duco | Cloud-native; growing in tier-1 |

---

## Liquidity / Intraday

| Product | Vendor | Note |
|---|---|---|
| SmartStream TLM Intraday Liquidity | SmartStream | Widely deployed |
| Planixs Realiti | Planixs | Real-time intraday liquidity specialist |
| ION Treasury | ION | Treasury + liquidity |
| Calypso / Adenza | Nasdaq (acq.) | Treasury + risk + collateral |

---

## How a Modern Stack Looks (Conceptual)

```
Channels  →  Bank API Gateway  →  Volante / Finastra GPP / ACI UP (Hub)
                                       │
              ┌────────────┬────────────┼────────────┬────────────┐
              ▼            ▼            ▼            ▼            ▼
            Fircosoft   ACTIMIZE     Featurespace   FX Rate    Fee Engine
            (Sanctions) (AML)        (Fraud)        Service
                                       │
                                       ▼
          ┌──────────┬──────────┬──────────┬──────────┬──────────┐
          ▼          ▼          ▼          ▼          ▼          ▼
        FedNow      RTP       FedACH    FedWire   FPS/CHAPS    SEPA / TIPS
        adapter    adapter    adapter   adapter   adapter      adapter
                                       │
                                       ▼
                  Connectivity layer (FedLine / TCH / Pay.UK / EBA / SWIFT)
                                       │
                                       ▼
                   Settlement (Master account / Nostro / Liquidity)
                                       │
                                       ▼
                   Core Banking System (Finacle / Flexcube / T24 / BaNCS / Vault)
                                       │
                                       ▼
                   GL, Reporting (Axiom / OneSumX), Recon (SmartStream),
                   Disputes, Archive
```

---

## Selection Considerations Per Use Case

| Use Case | Strong Candidates |
|---|---|
| US tier-1 modernisation (FedNow + RTP + ACH + wires) | Volante, ACI UP, Finastra GPP, Form3 (for cloud-native), IBM FTM |
| UK challenger / modernisation (FPS + CHAPS + Bacs + SEPA) | Form3, Volante, Finastra GPP, ACI UP |
| Indian tier-1 (UPI + NEFT + RTGS + IMPS + cards) | TCS BaNCS Payments, Finacle Payments, Oracle Banking Payments, ACI BASE24 (cards) |
| Cross-border SWIFT MX modernisation | Volante, Finastra GPP, ACI MTS, IBM FTM, Pelican |
| Cards issuer + acquirer | ACI BASE24-eps, FIS, TSYS, Marqeta (issuer-fintech), Adyen, Stripe |
| Greenfield / neobank | Mambu + Form3, Thought Machine + Form3, 10x stack |
| Sanctions + AML | Fircosoft + NICE Actimize / Oracle FCCM / Featurespace |

---

## Open Questions

- [ ] Confirm bank's incumbent payment hub product (drives a lot of KB content; ingest its operations docs).
- [ ] Confirm cards platform (issuer + acquirer; very different from general payment hub).
- [ ] Confirm fraud / sanctions / AML vendor map per region.
- [ ] Confirm modernisation programme status (greenfield vs. wrap-and-replace vs. in-place upgrade).
- [ ] Confirm cloud strategy for payments (on-prem core, cloud-native augmentation, full cloud).
