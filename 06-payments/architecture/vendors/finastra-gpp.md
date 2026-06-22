# Finastra Global PAYplus (GPP)

Finastra's flagship payment hub. Marketed as **Fusion Global PAYplus** (sometimes branded **Fusion Payments**). ISO 20022-native, multi-rail, multi-tenant capable.

> Parent reference: [../payment-engines.md](../payment-engines.md)
> Vendor docs are member-only — official answers must cite the contract version of the documentation in force at the bank.

---

## Product Heritage

- Original product line from **D+H** (formerly DH Corporation), built around the IBM mainframe-era SmartStream lineage in a different sense than the SmartStream vendor.
- D+H acquired the GPP product through its 2017 acquisition of the relevant business units.
- **Finastra** was formed in 2017 by the merger of **Misys** and **D+H Corp**, putting GPP into the Finastra portfolio.
- Continuously evolved since; current focus areas are ISO 20022 nativeness, cloud-native deployment (Fusion Cloud), and Payments-as-a-Service (PaaS).

---

## Positioning

| Dimension | Position |
|---|---|
| Target customer | Tier-1 / large tier-2 universal banks |
| Geography strength | EU SEPA, SWIFT cross-border, US Fed (FedNow, RTP, Wires, ACH), UK (FPS, CHAPS, Bacs), MEA, parts of APAC |
| Deployment | On-prem (legacy + still common), private cloud, Fusion Cloud (managed), Payments-as-a-Service |
| Differentiation | One of the broadest rail libraries; ISO 20022 native for many years; strong implementation track record at scale |

---

## Architecture (Conceptual)

```
                ┌────────────────────────────────────────────────────┐
                │              Channels / Initiators                  │
                │  Corporate H2H • Digital • API • SWIFT FI Inbound   │
                └──────────────────────┬─────────────────────────────┘
                                       ▼
   ┌──────────────────────────────────────────────────────────────────┐
   │                    GPP — Payment Hub Core                         │
   │                                                                   │
   │   ┌──────────────┐  ┌──────────────┐  ┌────────────────────┐    │
   │   │  Canonical   │  │   Routing &  │  │   Format / Schema  │    │
   │   │  Payment     │  │  Orchestration│  │   Transformation  │    │
   │   │  Repository  │  │   Engine     │  │   (ISO 20022 ↔     │    │
   │   │              │  │              │  │   MT / NACHA /     │    │
   │   │              │  │              │  │   scheme formats)  │    │
   │   └──────────────┘  └──────────────┘  └────────────────────┘    │
   │                                                                   │
   │   ┌──────────────┐  ┌──────────────┐  ┌────────────────────┐    │
   │   │  Workflow /  │  │  Operations  │  │  Status / UETR /   │    │
   │   │  Repair      │  │  Console     │  │  gpi Tracker       │    │
   │   │  (GPP SmartOps)│ │ (web UI)     │  │  Integration       │    │
   │   └──────────────┘  └──────────────┘  └────────────────────┘    │
   └─────────────────────────────┬────────────────────────────────────┘
                                  ▼
   ┌─────────┬─────────┬─────────┬─────────┬─────────┬─────────┐
   │  SWIFT  │  SEPA   │  US     │  UK     │  India  │  Cards  │
   │ Adapter │ Adapter │ Rails   │ Rails   │ Rails   │ Switch  │
   └─────────┴─────────┴─────────┴─────────┴─────────┴─────────┘
              │
              ▼
       External operators / schemes
              │
              ▼
    Pre-processing controls (sanctions, fraud, AML) integrated as services
              │
              ▼
       Bank's CBS + GL (Finacle / Flexcube / T24 / FIS / in-house)
```

The hub is **stateful** for the in-flight payment (workflow state machine) and **stateless** for ancillary services (sanctions, fraud, AML are pluggable).

---

## Core Modules

### GPP for SWIFT
- CBPR+ compliant MX (pacs.008, pacs.009, pacs.009.cov, pacs.002, pacs.004, camt.054 / 053 / 052, camt.056, camt.029, camt.087).
- Legacy MT support during co-existence (MT103, MT202, MT202COV, MT199 / 299, MT900 / 910, MT940 / 942, etc.).
- gpi UETR tracking + tracker integration.
- Translation MT ↔ MX with CBPR+ translation rules.

### GPP for SEPA
- SCT, SCT Inst (sub-10s), SDD Core, SDD B2B.
- EPC rulebook compliance per current annual revision.
- EBA STEP2 / RT1 + Eurosystem T2 / TIPS connectivity.

### GPP for US (Wires / ACH / FedNow / RTP)
- FedWire (ISO 20022 migrated state) + legacy field map.
- FedACH + EPN with NACHA file format + SEC codes + Same-Day ACH windows.
- FedNow (pacs.008 ISO 20022 native, RfP via pain.013).
- TCH RTP (pacs.008, pain.013, camt.056 cancellation).
- Wire repair workbench + STP rule engine.

### GPP for UK (FPS / CHAPS / Bacs)
- FPS with CoP (Confirmation of Payee) integration.
- CHAPS (ISO 20022 since 2023 in BoE format).
- Bacs DC + DD with ARUDD / ARUCS / ADDACS handling and 3-day cycle management.
- PSR specific direction handling (SD18 APP fraud joint liability surfaces).

### GPP for India
- NEFT, RTGS-IN (ISO 20022 since 2021), IMPS, UPI rail adapters.
- NPCI-prescribed connectivity patterns.
- Common at Indian tier-1 GPP deployments, often paired with Finacle CBS.

### GPP SmartOps (Operations Console)
- Web-based operations UI for investigations, repairs, holds, releases, audits.
- Configurable repair rules.
- Role-based access; integrates with bank's SSO + entitlement.

### GPP Smart Router
- Routing engine. Rules-based + table-driven; can incorporate cost optimisation + reachability + SLA tier.
- Hot-swappable rules without redeployment.

### Compliance Integration
- Pre-integrated points for sanctions filters (commonly **Fircosoft**, also LexisNexis / NICE Actimize), fraud (FICO, Featurespace, etc.), and AML (Actimize, SAS, Oracle Mantas).
- Hooks at well-defined lifecycle stages — call-out, response handling, hold queues, manual override paths.

---

## Data Model (Canonical Payment)

GPP holds a canonical payment object across its lifecycle. Conceptual structure:

```
Payment
├── Header (id, UETR, channel, creation, status)
├── Business Identifier (purpose, message type, scheme)
├── Parties
│   ├── Debtor (party + agent + account)
│   ├── Creditor (party + agent + account)
│   ├── Intermediary agents (n)
│   └── Ultimate parties (originating / final)
├── Amounts
│   ├── Instructed amount
│   ├── Interbank settled amount
│   └── Charge amounts per agent (CHRG_BR)
├── Dates
│   ├── Creation, requested execution, interbank settlement, value date
├── Charges
│   └── ChargeBearer + per-agent charge records
├── Compliance markers
│   ├── Sanctions outcome
│   ├── Fraud score
│   ├── AML status
│   └── Travel Rule completeness flags
├── Routing decision
│   └── Chosen rail + reason
├── Lifecycle state machine
│   └── states + transitions + timestamps + operator IDs
├── Investigation thread
│   └── camt.027 / 029 / 087 message refs
└── Audit trail
    └── append-only events
```

This is the **single source of truth** for any one payment. Downstream systems (recon, customer notification, audit, reporting) consume from this object.

---

## Lifecycle Coverage

GPP covers stages **1–13 and 19** of the [lifecycle](../lifecycle.md):
- Initiation through routing, transformation, submission, clearing acknowledgment.
- Exception handling — returns, repairs, investigations.

Stages 14–18 (settlement, posting, notification, reconciliation, reporting) typically depend on adjacent systems — CBS posting, dedicated recon, MI / reporting — though GPP supplies the events that drive them.

---

## Deployment Models

| Model | Notes |
|---|---|
| On-premise traditional | Long-running deployments; some at 10+ years vintage |
| Bank-private cloud | Tenancy in bank's IaaS (e.g., AWS / Azure / OCI / on-prem private cloud) |
| Fusion Cloud (Finastra-managed) | Managed-service variant |
| Payments-as-a-Service (PaaS) | Multi-tenant managed; faster onboarding; usually scoped to specific rails (e.g., FedNow PaaS) |

PaaS adoption is growing fast for **new instant rails** (FedNow, RTP) where a "wrap-and-extend" approach is preferred over rebuilding the entire stack.

---

## Tech Stack (Typical Profile)

- Java EE / Jakarta EE-based core.
- Relational database backbone — Oracle DB historically dominant; PostgreSQL appears in newer deployments.
- Message broker — IBM MQ (most common at tier-1), Kafka emerging.
- Application server — historically WebLogic / WebSphere; modernised deployments use containerised runtimes.
- Web UI — modern web (Angular-era + later evolutions).

Modern Finastra direction is **container-native + cloud-portable**; older deployments still have heavy WebLogic / IBM MQ footprints.

---

## Integration Surface

| Integration | Mechanism |
|---|---|
| Channels in | REST/SOAP APIs, file ingest, MQ, ISO 20022 inbound |
| Sanctions filter | Sync service call at defined hook |
| Fraud engine | Sync scoring + async feedback |
| AML / monitoring | Async event stream |
| CBS posting | API or MQ (varies by CBS vendor) |
| SWIFT connectivity | Via SWIFT Alliance suite (Access / Gateway / Lite2) |
| Domestic scheme connectivity | Via bank's scheme gateways (FedLine, TCH connectivity, Pay.UK gateway, NPCI MPLS, etc.) |
| Status events out | Kafka / MQ event stream |
| Operations UI | SmartOps web UI |

---

## Strengths

- Very broad rail library — most major schemes globally are covered.
- ISO 20022 native for many years; less retrofit risk than younger products.
- Mature operations tooling (SmartOps) — important at tier-1 ops scale.
- Strong implementation track record at multiple very large banks.
- Healthy ecosystem of consulting partners (Accenture, TCS, Infosys, Wipro, Cognizant, Capgemini).

---

## Weaknesses / Common Concerns

- Heritage stack at older deployments can be operationally heavy (WebLogic + IBM MQ + Oracle DB monoliths).
- License + run-rate cost is at the high end.
- Customisation tends to accumulate over years; upgrades to current versions can be programme-scale work.
- Some banks find the data model rigid relative to greenfield ISO 20022 designs; modernisation programmes can run multi-year.

---

## When to Choose GPP

- Existing GPP installed (most common reason — modernise in place).
- Need broad rail coverage in one product.
- Tier-1 bank with multi-region payments operation and complex internal entitlement / signing rules.
- Already invested in Finastra ecosystem (Fusion CBS, Fusion Markets, etc.).

---

## When NOT to Choose GPP

- Greenfield neobank — Form3 / Volante PaaS / cloud-native peers tend to be faster to onboard.
- Very narrow scope (e.g., just FedNow) — narrower products can be cheaper TCO.
- If the bank wants a single-pane all-in-one including CBS + payments — Temenos / Oracle Banking Suite integrate more tightly.

---

## Implementation Reality Check

- Tier-1 GPP implementation programmes typically run **18–36 months**.
- Cutover is rail-by-rail, often with a SWIFT MT → MX cutover overlay.
- Common failure modes:
  - Underestimation of repair-rule complexity at scale.
  - Sanctions integration latency under load.
  - Reconciliation breaks during cutover windows.
- Post-go-live, dedicated GPP run team is normal; ~10–30 engineers + ops at tier-1 scale.

---

## Cross-References

- Lifecycle stages it covers: [../lifecycle.md](../lifecycle.md)
- Sanctions / fraud / AML integration partners: [../systems-landscape.md](../systems-landscape.md)
- SWIFT MT/MX standards it transforms: [../../standards/swift-mt-mx.md](../../standards/swift-mt-mx.md), [../../standards/iso-20022.md](../../standards/iso-20022.md)

---

## Sources to Ingest

- Finastra GPP product documentation (member-only)
- GPP SmartOps administrator + operator guides
- GPP Smart Router rule reference
- GPP per-rail adapter guides (SWIFT, SEPA, FedNow, RTP, FPS, CHAPS, NPCI, etc.)
- GPP integration guides (sanctions, fraud, AML, CBS)
- Internal: bank's own GPP customisation catalogue, repair-rule library, support runbooks, performance baselines, programme RCA documents

---

## Open Questions

- [ ] Confirm which GPP version (and patch level) is in force at the bank.
- [ ] Confirm deployment posture (on-prem vs. private cloud vs. Fusion Cloud vs. PaaS) per rail.
- [ ] Confirm sanctions filter integration (Fircosoft most common; verify).
- [ ] Confirm CBS integration mechanism (API vs. MQ; sync vs. async posting).
- [ ] Confirm internal repair-rule ownership team.
- [ ] Confirm SmartOps role mapping to bank's entitlement service.
- [ ] Confirm modernisation roadmap (cloud move, container migration, ISO 20022 cutover state).
