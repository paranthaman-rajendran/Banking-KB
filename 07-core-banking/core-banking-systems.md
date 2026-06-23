# Core Banking Systems — Landscape

Inventory of the CBS products most commonly seen in tier-1 banks globally. Expands the brief catalogue in [../06-payments/architecture/payment-engines.md](../06-payments/architecture/payment-engines.md).

> Disclaimer: vendor product positioning shifts. Treat below as a directional reference; confirm with the vendor before quoting versions or capabilities.

---

## Selection Lens

When a tier-1 bank evaluates a CBS, the recurring criteria are:

1. **24x7 posting capability** — supports real-time rails (FedNow, UPI, FPS, SCT Inst) without blackout windows.
2. **Product configurability** — can launch a new product via metadata config, not code changes.
3. **Customer + account hierarchy support** — for corporate / wholesale segments.
4. **Multi-currency, multi-entity, multi-tenancy** — for group-level deployments.
5. **Integration surface** — modern API + event-stream + legacy file support.
6. **Cloud-native posture** — multi-region active-active, container-portable.
7. **Operational tooling** — branch UI, ops UI, investigation, audit.
8. **Total Cost of Ownership** — license + ops + run-rate.
9. **Implementation track record** at similar-size banks.
10. **Vendor strategic alignment** — long-term roadmap fit.

---

## Tier-1 Universal-Bank CBS Products

### Infosys Finacle
- Origin: Infosys-built; one of the most globally deployed CBS.
- Strong in: India, MEA, APAC, Africa, parts of EU; growing in Americas.
- Architecture: Java EE; Oracle DB historically (also moving to other RDBMS support); microservices direction in recent releases; modular adoption.
- Variants: Finacle Universal Banking, Finacle Digital Engagement Suite, Finacle Payments, Finacle Treasury, Finacle Cash Management, Finacle Online Banking.
- Modernisation: significant 24x7 posting + cloud-native delivery investment.
- Implementation tempo: 18–36 months at tier-1 scale.
- Notable deployments: many tier-1 Indian banks (ICICI, Axis, IDBI, Kotak, etc.), MEA banks, African banks.

### Oracle Flexcube Universal Banking (FCUBS)
- Origin: i-flex Solutions (acquired by Oracle, 2005).
- Strong in: India, MEA, APAC, EU; reasonable presence in Americas via Oracle ecosystem.
- Architecture: Oracle DB (mandatory historically), Java EE on WebLogic, ADF / JET UI; OCI-native direction.
- Variants: FCUBS core, Oracle Banking Payments (OBPM), Oracle Banking Trade Finance, Oracle Banking Treasury, Oracle Banking Liquidity Management, Oracle Banking APIs.
- Deeply integrated suite — Oracle's value proposition is the cross-module integration.
- Implementation tempo: 18–36 months at tier-1 scale.
- Notable deployments: many tier-1 banks globally including in MEA (Emirates NBD, FAB), APAC, EU.

### Temenos T24 / Transact
- Origin: Temenos, Switzerland-based.
- Strong in: Europe (Switzerland, Germany, France, UK, Nordics), Africa, fast-growing in APAC + Americas.
- Architecture: T24-on-jBASE historically; modern Transact on J2EE / containers; Temenos Banking Cloud variant.
- Variants: Transact (core), Infinity (digital), Wealth, Payments, Financial Crime Mitigation.
- Modernisation: aggressive cloud-native push; very large R&D spend per revenue.
- Notable deployments: HSBC (private banking), Itaú Unibanco, several tier-1 EU + APAC banks.

### TCS BaNCS
- Origin: TCS Financial Solutions.
- Strong in: India, APAC; tier-1 global deployments including in custody / securities + core banking.
- Architecture: Java EE; modular suite covering CBS, payments, capital markets, insurance, securities settlement.
- Variants: BaNCS Universal Banking, BaNCS Payments, BaNCS Securities Processing, BaNCS Wealth Management.
- Strong in: very-large-scale deployments (e.g., State Bank of India, one of the world's largest by customer count).
- Notable: BaNCS handles SBI's > 500M customer base — a stress-test no other CBS has matched.

### FIS — Profile, Systematics, Horizon, Bankway, Quantum
- Origin: FIS has grown by acquisition (eFunds, Metavante, SunGard, etc.).
- Variants:
  - **Profile** — modern, used in US large banks.
  - **Systematics** — mainframe-era, still in use at large US institutions.
  - **Horizon** — community + regional US bank focus.
  - **Bankway**, **Quantum** — various community-bank tiers.
- Strong in: US banking; broad US footprint from community to large.
- Tech: mix of mainframe + distributed; modernisation programmes in flight.
- Notable: extremely common in US regional + large banks.

### Fiserv — DNA, Premier, Signature, Cleartouch
- Origin: Fiserv (often pre-FIS-merger competitor for community / regional US banks).
- Variants:
  - **DNA** — modern API-friendly core.
  - **Premier** — long-standing community-bank core.
  - **Signature** — large community / mid-size focused.
  - **Cleartouch** — Lendingfocus.
- Strong in: US community banks, credit unions, regional banks.
- Notable: heavy US footprint; broad credit-union presence.

### Jack Henry SilverLake / Symitar / Episys
- Origin: Jack Henry, US-focused.
- Strong in: US community banks (SilverLake), credit unions (Symitar / Episys).
- Tech: in-house developed; very loyal customer base.
- Notable: dominant in US community-bank sector.

### Mambu
- Origin: cloud-native, founded 2011.
- Strong in: greenfield neobanks, fintech partnerships, embedded finance; broad EU + APAC + Americas.
- Architecture: cloud-native, API-first, multi-tenant SaaS.
- Notable: behind many neobanks (N26 earlier, Tonik in PH, etc.); growing tier-1 augmentation (alongside legacy CBS for specific products).

### Thought Machine Vault
- Origin: London-based; founded 2014.
- Strong in: tier-1 universal-bank modernisation (Lloyds, JPMorgan-Chase, Standard Chartered, ATB Financial); cloud-native.
- Architecture: cloud-native, Kubernetes-based, smart-contract approach where each product is configured by a "Smart Contract" in Python.
- Notable: Lloyds Banking Group's "Stockmate" + Chase UK selected Vault; JPMC selected Vault for some US retail.

### 10x Banking
- Origin: founded 2016 (Antony Jenkins, ex-Barclays CEO).
- Strong in: tier-1 modernisation (West Pac in AU, Chase UK rumoured at various stages).
- Architecture: cloud-native, API-first; ledger-led design.

### SAP Banking Services
- Origin: SAP, German.
- Strong in: EU; integrated with SAP S/4HANA for ERP + financial accounting.
- Notable: heavy in DE / AT / CH; growing in Latin America.

### nCino + Salesforce Financial Services Cloud
- Not full CBS, but **front-office layer over the CBS** — increasingly common at large banks for commercial banking origination, servicing, relationship management.
- Notable: pairs with nearly any CBS.

### Backbase
- Not a CBS — **digital engagement layer over the CBS**. Customer + employee channels.

### Legacy / In-house
- Many tier-1 US banks (JPMC core retail, BofA, Wells, Citi parts) still run **legacy in-house cores**, often mainframe-era, undergoing multi-year modernisation programmes. The modernisation target is typically Vault, 10x, or a Fiserv / FIS modern variant — sometimes with phased segment migration (digital-first sub-brand → mainstream retail → wholesale).

---

## CBS Selection by Bank Archetype

| Archetype | Typical CBS Choices |
|---|---|
| Tier-1 universal — US, modernisation track | Legacy in-house → Vault / 10x / Mambu / FIS Profile (varies by segment) |
| Tier-1 universal — EU | Temenos Transact (large EU footprint), SAP Banking (DE / AT), or in-house legacy |
| Tier-1 universal — India | Finacle, Flexcube, BaNCS (all three dominate the Indian large-bank market) |
| Tier-1 universal — MEA / APAC | Finacle, Flexcube, Transact, BaNCS |
| Regional US bank | FIS Profile / Systematics / Horizon, Fiserv DNA / Premier, Jack Henry SilverLake |
| Community US bank | Fiserv Premier / Cleartouch, Jack Henry SilverLake, FIS Bankway |
| Credit union | Jack Henry Symitar / Episys, Fiserv DNA / Premier |
| Neobank / fintech-first | Mambu, Vault, 10x; sometimes paired with Form3 for payments |
| Embedded finance / BaaS provider | Mambu, Galileo, Marqeta (cards) |

---

## Architecture Considerations

### Single CBS vs Multiple CBS
Many tier-1 universal banks operate **multiple CBS platforms** in parallel:
- One for retail; one for corporate / wholesale; one for private banking / wealth; one for a digital-only sub-brand.
- This is partly historical (acquisitions), partly architectural (corporate needs differ sharply from retail).

The downside: a customer who is both a retail customer and a small-business customer has two CIFs, two product catalogues, two channels. Many modernisation programmes target consolidation.

### Cloud-Native vs On-Prem
Modern CBS (Vault, 10x, Mambu) are cloud-native by design. Legacy CBS (Finacle, Flexcube, T24) have container-native variants but the most stable deployments remain on-prem or private-cloud.

The cloud move for CBS is **higher-stakes than for payments**:
- Customer data residency.
- Regulatory comfort with cloud (varies by jurisdiction — strict in CN, IN; permissive in UK, US, SG).
- Long batch windows have to be re-architected for cloud cost economics.

### 24x7 Posting
Critical for FedNow / RTP / UPI / FPS / SCT Inst real-time rails. Without 24x7, the bank takes incoming funds and parks them in suspense until the CBS opens — risky and customer-unfriendly.

Vault, 10x, Mambu — all 24x7 by design. Modern Finacle / Flexcube / Transact releases — 24x7 capable but typically require redeployment / re-architecture. Legacy mainframe cores — often NOT 24x7.

---

## Integration Surface (Universal Pattern)

| Integration | Mechanism |
|---|---|
| Channels (mobile, internet, branch, ATM) | REST / GraphQL APIs, MQ, file |
| Payment hub | API (sync) + event stream (async) |
| Cards platform | API + ISO 8583 feeds |
| Compliance (sanctions / AML / KYC) | Sync call + event stream |
| GL | Native posting + nightly reconciliation file |
| Risk engines | Event stream + nightly extract |
| Data warehouse / lakehouse | Change Data Capture (Debezium et al.) + extracts |
| Treasury workstations | Statement files (MT940 / camt.053 / BAI2) |
| Regulatory reporting | Extracts to dedicated platform (Axiom / OneSumX) |

---

## Common Failure Modes at Scale

| Failure | Cause | Mitigation |
|---|---|---|
| EOD overruns into the next day's window | Volume growth + legacy batch design | 24x7 architecture migration |
| Customer master inconsistency across CBS instances | Multi-CBS without strong sync | Consolidate to single CIF |
| Posting latency under instant-rail load | CBS designed for ~100 TPS, instant rails push 1500+ TPS | Modernise CBS or front with caching layer |
| Stale product config | Manual product-master changes | Workflow-managed product config |
| GL break at month-end | Sub-ledger errors not caught | Real-time recon vs. nightly |
| Cross-jurisdictional FATCA / CRS report errors | Customer tax-status field gaps | Tighten KYC + customer-master discipline |

---

## Sources to Ingest

- Per-CBS product documentation (vendor / member-only)
- Per-CBS implementation guides + customisation references
- Bank-internal: CBS customisation catalogue, parameter library, upgrade history, batch / EOD windows, performance baselines
- Industry analyst reports (Gartner CBS Magic Quadrant, IBS Intelligence rankings)

---

## Open Questions

- [ ] Confirm CBS product(s) in scope per segment (retail vs corporate vs wealth).
- [ ] Confirm 24x7 posting status per CBS instance.
- [ ] Confirm modernisation roadmap per CBS.
- [ ] Confirm single-CIF vs multi-CIF posture.
- [ ] Confirm cloud strategy for CBS (on-prem, private cloud, hyperscaler).
