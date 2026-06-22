# Payment Systems Landscape — Tier-1 Bank

A real payment in a large bank touches **15–30 systems** between initiation and archival. This document maps the system categories and the canonical responsibilities of each.

> Companion: [lifecycle.md](lifecycle.md) maps the stages; [payment-engines.md](payment-engines.md) names commercial products that implement these categories.

---

## Layered Architecture

```
┌────────────────────────────────────────────────────────────────────────────┐
│                     CHANNEL / ORIGINATION LAYER                             │
│  Digital banking • Branch teller • Corporate H2H • Open API • SWIFT-FI in   │
│  Card terminals • Mobile wallet • PISP                                      │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                   PAYMENT INITIATION / ORCHESTRATION                        │
│  Payment Gateway • Canonical Payment Hub                                    │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                   PRE-PROCESSING / CONTROL LAYER                            │
│  Fraud Engine • Sanctions Screening • AML Transaction Monitoring •          │
│  KYC / CIF • Entitlement / Limits • FX Rate Service • Fee Engine            │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                   PROCESSING / EXECUTION LAYER                              │
│  Payment Processing Engine (Hub) • Rail Adapters (ACH / Wire / RTP /        │
│  FedNow / FPS / CHAPS / Bacs / UPI / SEPA / Card Switch) • Format Library   │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                   CONNECTIVITY / GATEWAY LAYER                              │
│  SWIFT Alliance Gateway / FINplus • FedLine • TCH connectivity • Pay.UK     │
│  gateway • NPCI connectivity • EBA STEP2 / RT1 / T2 • Card scheme links     │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                   SETTLEMENT / LIQUIDITY                                    │
│  Nostro Manager • Intraday Liquidity • Position Keeper • Treasury           │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                   POSTING / BOOKING                                         │
│  Core Banking System (CBS) • General Ledger • Customer Account Master       │
└──────────────────────────────────┬──────────────────────────────────────────┘
                                   ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                   POST-PROCESSING                                           │
│  Reconciliation • Investigations • Reporting • Statement Engine •           │
│  Dispute Management • Archival                                              │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Channel / Origination Layer

| System Category | Purpose | Examples (internal / vendor) |
|---|---|---|
| Digital Banking | Customer-facing web + mobile payment initiation | Internally-built; Backbase, Temenos Infinity, Finastra Fusion Digital |
| Corporate Channel | Host-to-host file ingestion + portal | Bottomline PTX, Finastra Fusion Corporate Channels, Bank-built |
| API Gateway | Programmatic payment APIs (Open Banking + corporate) | MuleSoft, Apigee, Kong, Tyk, AWS API Gateway |
| Branch / Teller | In-person payment capture | FIS Branch, Finacle Branch, Bank-built |
| ATM | Cash withdrawal, transfers | NCR, Diebold Nixdorf software; ATM driver — see card switch |
| POS / Acceptance | Card-present + contactless | Verifone, Ingenico, PAX terminals; merchant acquirer software |
| PISP (Open Banking) | Third-party initiated | OBIE-compliant interfaces |
| SWIFT FI Inbound | Bank-to-bank initiations arriving | SWIFT Alliance Access / Gateway |

---

## Payment Initiation / Orchestration

This is where the payment becomes a **canonical record** independent of the channel of origin.

| System | Purpose |
|---|---|
| **Payment Initiation Gateway** | Normalises channel-specific input to canonical schema; first-line validation; routes to downstream |
| **Canonical Payment Hub** | Single source of truth for the payment object from creation to closure |
| **Workflow / BPM** | Manages multi-step approvals (corporate signing rules, manual reviews) |

This layer is increasingly delivered by **payment hubs** — see [payment-engines.md](payment-engines.md).

---

## Pre-Processing / Control Layer

### Fraud Detection
| Product | Notes |
|---|---|
| FICO Falcon | Long-running scheme leader, especially in cards |
| SAS Fraud Management / Viya | Enterprise-grade, broad rail coverage |
| Featurespace ARIC | Adaptive behavioural analytics; strong in real-time rails |
| NICE Actimize Xceed / IFM | Fraud + AML integrated |
| ACI Fraud Management | Card + cross-rail |
| Pelican Fraud | AI-driven, ISO 20022 native |
| ThreatMetrix / LexisNexis Risk Solutions | Device + identity intelligence |
| Bank-built ML | Common at very large banks |

### Sanctions Screening
| Product | Notes |
|---|---|
| Fircosoft Continuity / Fircosoft Trust | Industry-leading filter; deep SWIFT integration |
| LexisNexis Bridger Insight XG | Enterprise list management + screening |
| Accuity / LexisNexis Compliance Catalyst | Real-time payments screening |
| Oracle Financial Services Sanctions | Tied with Oracle Mantas AML |
| NICE Actimize Watch List Filtering | Integrated suite |
| SAS Sanctions Screening | Within SAS Compliance Suite |
| Refinitiv World-Check (list provider) + screening overlay | Often pairs with a filter |
| Bank-built filters | At the biggest banks |

### AML Transaction Monitoring
| Product | Notes |
|---|---|
| NICE Actimize AML / SAM | Market-leading at tier-1 banks |
| SAS AML | Strong analytic depth |
| Oracle Mantas / FCCM | Oracle's compliance suite |
| Featurespace ARIC | Behavioural-led, RT-friendly |
| ComplyAdvantage | Cloud-native; common at fintech / mid-market |
| FIS Prime Compliance Suite | FIS bundle |
| BAE Systems NetReveal | Strong in EU, financial crime detection |
| Quantexa | Network-analytic entity resolution |

### KYC / CIF
- Customer Information File (CIF) is the bank's master record.
- KYC orchestration vendors: Fenergo, NICE Actimize KYC, Oracle FCCM, Bank-built.

### Entitlement / Limits
- Authorisation service: who can initiate what, for whom, up to what limit.
- Often integrated with corporate signing-rule engines.

### FX Rate Service + Fee Engine
- Treasury rate source, customer-tier markup, retail/wholesale segmentation.
- Fee schedules applied based on currency / corridor / customer tier.

---

## Processing / Execution Layer — The Payment Hub

The **payment processing engine** (payment hub) is the core of the architecture. Modern hubs are ISO 20022 native and rail-aware. They:

1. Hold the canonical payment record.
2. Orchestrate the control layer (parallelised where possible).
3. Decide routing per the rail-selection rules.
4. Convert to rail-specific format.
5. Hand off to the connectivity gateway.
6. Track end-to-end status using UETR + scheme refs.
7. Manage retries, returns, repairs.

Top products: see [payment-engines.md](payment-engines.md).

### Rail Adapters
Each rail has its own adapter inside the hub:

| Rail | Adapter Responsibility |
|---|---|
| FedWire | Sign-on, FedWire field map, BTR codes, IMAD/OMAD tracking |
| FedNow | ISO 20022 native, ACK/NACK handling, RfP flow |
| RTP (TCH) | Same as FedNow; different connectivity |
| ACH | NACHA file build, SEC codes, Same-Day windows |
| FPS | Pay.UK API, CoP integration |
| CHAPS | ISO 20022 BoE format, purpose codes |
| Bacs DC/DD | 3-day cycle, AUDDIS, ARUDD return processing |
| UPI | NPCI APIs, VPA resolution |
| NEFT / RTGS-IN | RBI structured network connectivity |
| SEPA CT / Inst | EPC rulebook compliance, EBA / TIPS routing |
| Cards (issuer) | ISO 8583 issuer host; 3DS interplay |
| Cards (acquirer) | ISO 8583 acquirer host; scheme routing |
| Cross-border SWIFT | CBPR+ MX (and legacy MT during co-existence) |

---

## Connectivity / Gateway Layer

Physical and logical connectivity from the bank to the operator.

| Operator / Rail | Connectivity |
|---|---|
| SWIFT (cross-border + select domestic) | SWIFT Alliance Access / Alliance Gateway / Alliance Connect; SWIFT Lite2 for smaller participants |
| Federal Reserve (FedACH, FedWire, FedNow) | FedLine Direct / FedLine Advantage / FedLine Web |
| The Clearing House (RTP, CHIPS, EPN) | TCH-managed connectivity (direct + service provider) |
| Pay.UK (FPS, Bacs, ICS) | Pay.UK direct gateway + Pay.UK approved service providers (e.g., Bottomline, FIS, Form3) |
| Bank of England (CHAPS) | BoE-managed direct participant connectivity |
| NPCI (UPI, IMPS, NEFT-channel, AePS, NACH) | RBI/NPCI prescribed connectivity (encrypted MPLS) |
| EBA Clearing (STEP2, RT1) | EBA Clearing connectivity |
| Eurosystem (TARGET2 / T2 / TIPS) | NSP (Network Service Provider — SIA-Colt or SWIFT) |
| Card schemes (Visa, Mastercard, RuPay, Amex, Discover, JCB, UnionPay) | Scheme-defined IPSec / leased line / network |

---

## Settlement / Liquidity

| System | Purpose |
|---|---|
| Nostro / Vostro Manager | Tracks bank's accounts at correspondents + correspondents' accounts at the bank |
| Intraday Liquidity Manager | Real-time view of available balance across nostros + central bank account; throttling for high-value queues |
| Position Keeper | Aggregated currency-level position used by treasury |
| Settlement Engine | Manages netting, prefunding, end-of-day cut-offs |

Vendor examples: SmartStream TLM Intraday Liquidity, FIS Trax, IBM Financial Transaction Manager, Calypso/Adenza (settlement), bank-built.

---

## Posting / Booking

| System | Purpose |
|---|---|
| **Core Banking System (CBS)** | Customer account master; debit / credit posting; balance tracking |
| **General Ledger (GL)** | Bank's accounting truth |
| **Customer Account Master / CIF** | Identity + relationship data |
| **Sub-Ledgers** | Per-product sub-ledgers for cards, deposits, loans |

Top global CBS products:

| Product | Vendor | Notes |
|---|---|---|
| Finacle | Infosys | Very widely deployed in India, MEA, APAC, EMEA |
| Flexcube | Oracle | Global footprint; many tier-1 deployments |
| T24 / Transact | Temenos | Strong in Europe, Africa, fast-growing globally |
| BaNCS | TCS | Tier-1 deployments including very large banks (e.g., SBI) |
| FIS Profile / Systematics | FIS | US-strong; large bank legacy + modern variants |
| Fiserv DNA / Premier / Signature | Fiserv | US community + regional |
| Jack Henry SilverLake | Jack Henry | US community banks |
| Mambu | Mambu | Cloud-native, API-first; popular with neobanks |
| Thought Machine Vault | Thought Machine | Cloud-native; tier-1 modernisation (Lloyds, JPMC) |
| 10x Banking | 10x | Cloud-native; tier-1 modernisation |
| SAP Banking | SAP | German + EU strong; integrated with SAP S/4HANA |

---

## Post-Processing

### Reconciliation
| Product | Notes |
|---|---|
| SmartStream TLM Reconciliations Premium | Industry-standard for nostro + card recon |
| Fiserv Frontier Reconciliation | Strong in Americas |
| FIS IntelliMatch | Multi-format matching |
| Broadridge Reconciliation | Securities + payments breadth |
| NICE Actimize Reconciliation | Compliance-integrated |
| Bank-built recon | Common where workflows are highly bespoke |

### Reporting + MI
- Regulatory: bespoke per regulator + Axiom (FIS Regulatory Reporting), Wolters Kluwer OneSumX, BearingPoint Abacus.
- MI / dashboards: Tableau, Power BI, Qlik, ThoughtSpot, Looker.

### Investigations / Disputes
- SWIFT gpi tracker integration.
- Case management: Pega, Salesforce Financial Services Cloud, Bank-built.
- Card disputes: ACI Issuer Card Management, Visa Resolve Online (VROL), Mastercom.

### Archival
- Document mgmt: OpenText, IBM FileNet, custom S3 + Glacier strategies.
- Immutable audit: append-only stores; see [../03-governance/audit-controls.md](../../03-governance/audit-controls.md).

---

## Integration Patterns

- **Synchronous** for fraud + sanctions + funding check on real-time rails (latency-critical).
- **Asynchronous / event-streamed** for notifications, AML monitoring, reporting (Kafka or similar).
- **File-based batch** for legacy ACH / Bacs file workflows.
- **Saga-style orchestration** within the payment hub for multi-step reservations + commit / rollback.

Modern hubs typically expose a **payment status event stream** consumed by treasury, MI, and customer notification services.

---

## Resilience Patterns

| Concern | Pattern |
|---|---|
| Scheme outage | Hub failover to alternate rail (e.g., FedWire ↔ CHIPS for USD wholesale) |
| Hub outage | Active-active, multi-region with shared state |
| Sanctions list failure | Last-known-good list + monitoring + escalation |
| CBS outage | Suspense booking + replay on recovery |
| Connectivity loss (e.g., SWIFT) | Store-and-forward queue; SWIFT Lite2 + Alliance Connect dual links |
| Data centre failover | DR site with continuous replication |

---

## Open Questions

- [ ] Confirm bank's CBS vendor + version (drives many ingestion details).
- [ ] Confirm payment hub product if external (Finastra GPP, Volante VolPay, etc.) or in-house.
- [ ] Confirm fraud + sanctions + AML vendor stack.
- [ ] Confirm SWIFT connectivity (Alliance Access vs. Lite2 vs. service bureau).
- [ ] Confirm reconciliation product per asset class (different vendors are common per stream).
- [ ] Confirm cloud-strategy direction (hybrid? full-cloud? specific to non-regulated workloads?).
