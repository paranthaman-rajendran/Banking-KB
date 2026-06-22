# Foundational Concepts — Payments & Compliance

Paragraph-style explainers for the generic terms that recur across rails, regulatory regimes, and engine designs. Where the [glossary](glossary.md) gives a one-liner, this file gives the conceptual frame — what the term *means*, what it *contrasts* with, and why it matters operationally.

> Read this before diving into [regulatory/](regulatory/) per-jurisdiction files. Many regulatory disputes turn on the difference between two terms here.

---

## Sanctions

### Primary Sanctions
Restrictions imposed by a sanctioning state on **its own persons and territory**. A US person, US entity, US-located activity, or USD-denominated transaction touching the US financial system is subject to **US primary sanctions** regardless of where the parties to the underlying business sit. Primary sanctions are legally binding under the sanctioning state's law and breach exposes the violator to that state's criminal and civil enforcement.

Engine implication: the bank's pre-payment screening must apply primary sanctions of every jurisdiction the bank has a touchpoint in — its head office, branches, subsidiaries, and customer accounts denominated in that state's currency.

### Secondary Sanctions
Restrictions a sanctioning state imposes on **non-residents and foreign entities** that do business with sanctioned persons, even when the activity has no other connection to the sanctioning state. **US secondary sanctions** are the dominant example: a non-US bank with no US offices can still be cut off from the US financial system if it knowingly facilitates significant transactions for an SDN.

Secondary sanctions are not "law" in the way primary sanctions are — they are *coercive*: the cost of being designated yourself, losing USD-clearing access, or being shut out of the US financial system is the enforcement lever, not direct prosecution. This is why non-US banks often comply with US sanctions even when their home regulator does not require it.

Engine implication: even purely non-US payments routed through a USD correspondent leg become exposed to OFAC. The hub must screen every party in every USD-touching chain, not just at the home jurisdiction.

### Sectoral Sanctions
A *narrower* form than full SDN designations. Sectoral sanctions restrict only specified types of activity (e.g., new equity or debt financing of designated Russian energy firms beyond a maturity threshold) rather than blocking all dealings. Found in directives like OFAC's CAPTA / SSI lists. Operationally harder than SDN — the engine must understand the *transaction characteristics*, not just match a name.

### Specially Designated Nationals (SDN)
Persons or entities subject to **full blocking** by the sanctioning regime — all property and interests in their property within reach of the regime are frozen, and all dealings prohibited absent a licence. The US OFAC SDN list is the dominant global reference; EU, UK, UN, etc. maintain equivalents.

### 50% Rule
An OFAC interpretive doctrine: any entity in which one or more SDNs hold a **combined 50% or greater** ownership (directly or indirectly) is *itself* blocked, even if not separately named. Operational impact is large — the engine cannot rely on direct name-match alone; it needs UBO (beneficial ownership) data to compute the rule. Many false negatives originate here. EU and UK have similar (but not identical) thresholds and aggregation rules.

### Blocked vs. Rejected Transaction
A **blocked** transaction is one where the funds are frozen and reported to the sanctioning authority — funds stay on the bank's books but are not released. A **rejected** transaction is one that doesn't trigger blocking obligations but is refused (returned to sender). The distinction matters: blocked funds require holding + ongoing reporting; rejected funds are simply returned.

OFAC: blocking applies for SDNs and most country programmes; rejection applies for some other prohibited dealings (e.g., touching certain jurisdictions where the underlying parties aren't designated but the dealing itself is prohibited).

### Asset Freeze
The legal effect of blocking — title can pass but no economic interest can be released. Funds remain segregated; investment income accrues but cannot be paid; ongoing reporting on holdings required.

### General Licence vs. Specific Licence
A **general licence** is a public authorisation by the sanctioning regime allowing a *class* of transactions that would otherwise be prohibited (e.g., humanitarian aid, specific wind-down activities). Anyone meeting the conditions can act under it without separately applying. A **specific licence** is a case-by-case written permission to a named party for a named transaction.

Engine implication: when a screening hit is justified by a general licence, the engine must capture which GL applies and the supporting evidence in the audit trail.

### Wind-Down Period
A grace period that sanctions regimes typically provide between designation and full prohibition, during which counterparties may settle pre-existing obligations with the newly-designated person without violating sanctions. Operationally tight — the engine must distinguish wind-down-eligible from new-business transactions, often within days.

### Dual-Use Goods
Goods or technology with both civilian and military or proliferation applications. Trade-finance-linked payments touching dual-use goods are subject to export-control regimes (US EAR, EU Dual-Use Regulation, UK Export Control Order). Engines processing trade-finance flows need controls beyond sanctions screening alone.

---

## AML / CFT (Anti-Money Laundering / Counter-Financing of Terrorism)

### KYC vs. KYB vs. CDD
**KYC** (Know Your Customer) is the colloquial umbrella term for verifying who you're dealing with — usually retail or sole-trader customers. **KYB** (Know Your Business) is the corporate-equivalent — verifying entity structure, beneficial owners, and control. **CDD** (Customer Due Diligence) is the formal regulatory term that captures both: the FATF / EU AML rulebook structure. The engine and onboarding system enforce CDD; the customer-facing colloquialism is KYC.

### CDD / EDD / SDD
- **CDD** is the *standard* level — identification, verification, business-purpose understanding, ongoing monitoring proportional to risk.
- **EDD** (Enhanced Due Diligence) applies to higher-risk customers — PEPs, high-risk jurisdictions, complex ownership, unusual transaction patterns. Adds senior-management approval, source-of-funds verification, more frequent review.
- **SDD** (Simplified Due Diligence) applies to lower-risk customers (e.g., listed companies, public authorities) — reduced scope, more reliance on documentary evidence.

### Risk-Based Approach (RBA)
FATF's foundational principle. Rather than uniform CDD for everyone, financial institutions assess each customer's risk and apply controls proportional to that risk. This means SDD for the boring, EDD for the unusual. The bank's customer risk rating model is the operational implementation.

### Beneficial Owner (UBO) / Ultimate Beneficial Owner
The natural person(s) who ultimately own or control a customer, typically defined at a 25% ownership or control threshold (FATF baseline; jurisdictions vary). Critical for the OFAC 50% Rule, sanctions screening, and PEP detection. UBO data is structurally hard to obtain accurately — onboarding workflows often need iteration with the customer to nail down the structure.

### PEP — Politically Exposed Person
Individuals in prominent public functions (heads of state, ministers, senior judiciary, central-bank officials, military top brass) plus their close family and close associates. PEPs are not presumed corrupt — they are presumed to carry elevated AML/CFT risk and trigger EDD. Jurisdictional definitions differ on domestic-vs-foreign PEPs and on how long someone remains a PEP after leaving office (often 12 months; some jurisdictions keep them flagged longer).

### Source of Funds vs. Source of Wealth
**Source of Funds** explains where the specific money in a transaction came from (e.g., proceeds from sale of an apartment). **Source of Wealth** explains how the customer accumulated their overall wealth over time (e.g., founded a company in 1998, sold it in 2019). EDD typically requires both. Engines and onboarding flows must capture and link both.

### Placement / Layering / Integration
The classical three stages of money laundering:
- **Placement**: introducing illicit cash into the financial system (e.g., cash deposits, smurfing).
- **Layering**: moving funds through multiple transactions to obscure origin (rapid movement, shell companies, cross-border hops).
- **Integration**: returning funds to the launderer in apparently legitimate form (asset purchases, business investments).

Transaction monitoring rules typically target the *layering* phase — that's where unusual patterns are visible to the payment hub.

### Structuring / Smurfing
Deliberately breaking up transactions to avoid reporting thresholds (US CTR at USD 10,000, EU cash thresholds at EUR 10,000, etc.). Often the first pattern detected by AML monitoring. Sometimes called "smurfing" (smurfs being the small repeated bits).

### Wire Stripping
Removing or altering payment-message fields (originator name, beneficiary name, country) to avoid sanctions screening at a downstream party. The classic 2000s scandal — multiple global banks paid billions in OFAC settlements for routine wire stripping. Modern controls: structured ISO 20022 fields that resist stripping, gpi UETR end-to-end, plus Wolfsberg-aligned correspondent diligence.

### Shell Company vs. Front Company
A **shell company** is a legal entity with no significant operations — used as a vehicle for ownership, financing, or asset-holding. Shell companies are not inherently illegal but are heavily abused for layering and beneficial-owner obfuscation. A **front company** is a real-operating business that deliberately serves as a cover for illicit activity (e.g., a restaurant used to launder cash). The distinction matters because shell-company transactions need beneficial-owner scrutiny; front-company transactions need transactional-pattern detection.

### Nested Correspondent
A correspondent banking arrangement in which the **respondent bank's own customers** (or further-removed entities) use the correspondent banking relationship — without the correspondent bank knowing who those entities are. Treated as high-risk because the correspondent loses visibility. Most major banks now restrict or prohibit nested arrangements absent specific approval. Wolfsberg CBDDQ Question 11 covers this.

### SAR / STR
**Suspicious Activity Report** (US) / **Suspicious Transaction Report** (EU, UK, most other jurisdictions) — a formal filing by a regulated entity to the local Financial Intelligence Unit (FinCEN, NCA, FIU-IND, JFIU, AUSTRAC, etc.) when the entity has reasonable grounds to suspect money laundering or terrorist financing. SARs are confidential — the customer cannot be told ("tipping off" is a separate offence). The engine and AML system produce alerts; investigators triage; final SARs are submitted by the bank's MLRO (Money Laundering Reporting Officer).

### Money Mule
A person who receives and forwards illicit funds on behalf of others — sometimes unwittingly (e.g., recruited via fake job ads), sometimes knowingly. Mule accounts are a key endpoint in APP fraud and online fraud. Receiver-side fraud controls now target mule-account detection (rapid in-out, large unusual receipts, network linkage to other mules).

### Travel Rule
FATF Recommendation 16 — wire transfers above a threshold must carry originator + beneficiary identifying information through the entire payment chain. See [regulatory/cross-border-international.md](regulatory/cross-border-international.md) for full mechanics. The engine must enforce field completeness on outbound, and refuse to process inbound payments missing required fields (typically held for repair / RFI back to sender).

---

## Correspondent Banking

### Nostro / Vostro / Loro
Three Italian-origin terms that describe the **same account from three perspectives**:
- **Nostro** ("ours") — *your account at me*, as seen by you. "My USD account at Citi" — to me, that's my nostro.
- **Vostro** ("yours") — *your account at me*, as seen by me. To Citi, the same account is my vostro.
- **Loro** ("theirs") — *their account*, when referenced by a third party. Rarely used in modern English-language banking.

Engine implication: nostro/vostro management is a core function — every cross-border payment moves money between two banks' nostro/vostro positions. The intraday liquidity manager tracks them in real time.

### Correspondent Bank / Respondent Bank
A **correspondent bank** provides services (USD clearing, cheque collection, FX) to another bank (the **respondent**) that doesn't have local presence or licence. The correspondent does the work; the respondent's customer is invisible to the correspondent (unless explicitly disclosed). Wolfsberg CBDDQ governs the diligence the correspondent must do on the respondent.

### Continuous Linked Settlement (CLS)
A specialised settlement infrastructure that eliminates settlement risk in FX trades by settling both legs of a trade *only when both legs are funded* (Payment-versus-Payment). Operated by CLS Bank; covers the major freely-tradeable currencies. Critical to wholesale FX; the bank's treasury and the payment engine handling FX-leg payments interface with CLS.

---

## Settlement & Clearing

### Clearing vs. Settlement
Often confused; they are distinct:
- **Clearing** is the *process of computing what each participant owes* — message validation, matching, netting where applicable.
- **Settlement** is the *actual money movement* on the operator's or central bank's books — the moment of payment finality.

A scheme like ACH does both, in sequence. Bacs runs a 3-day clearing → settlement cycle. FedWire collapses them into the same moment (clearing + settlement = receipt by Fed).

### RTGS vs. DNS
- **RTGS** (Real-Time Gross Settlement) — every transaction settles individually, in real time, with finality. FedWire, CHAPS, RTGS-IN, BOJ-NET, MEPS+, TARGET2.
- **DNS** (Deferred Net Settlement) — transactions accumulate within a window; at window close, the net position per participant settles. ACH (US standard), NEFT (IN), Bacs (UK), SCT non-Inst (EU).

RTGS has higher liquidity demand (you need the cash now) but lower settlement risk. DNS economises on liquidity but introduces inter-window risk. Instant rails (FedNow, RTP, UPI, FPS, SCT Inst, Pix) are typically RTGS-on-prefunded-account at the central bank — gross finality on a prefunded position.

### Finality
The point at which a payment becomes **irrevocable** — cannot be reversed unilaterally by the sender, the scheme, or anyone other than by mutual agreement of the parties. Finality is what RTGS provides at the moment of settlement; deferred-settlement schemes provide finality at the end of the settlement window. Reg J (US) and BoE CHAPS rules formalise finality for those rails.

Common misconception: instant ≠ irrevocable in all schemes. UPI has dispute mechanisms with reversal possibilities within defined windows. FedNow and RTP messages are final on credit but can be reversed via *return* messages if the receiver cooperates — there is no scheme-level unilateral reversal.

### Irrevocability
The legal status — once final, the payment cannot be undone. Distinguished from "reversibility under scheme rules" which some instant rails offer within tight time windows.

### Payment-versus-Payment (PvP)
Both currency legs of an FX trade settle *only if both can settle*. CLS is the dominant PvP infrastructure for FX. Eliminates **Herstatt risk** (the risk that you settle one leg of an FX trade before the counterparty fails on the other leg). The 1974 Herstatt collapse — German bank Herstatt was closed mid-day after counterparties had already paid DEM but before USD had moved — is the canonical historical example.

### Delivery-versus-Payment (DvP)
The securities-side analogue: cash and securities move atomically. CSDs (Central Securities Depositories) provide DvP. Payment engine intersects DvP when a securities settlement triggers a payment.

### Settlement Risk
The risk that a counterparty fails to deliver its leg after you've delivered yours. RTGS and PvP infrastructures exist to eliminate or minimise it. In retail rails, settlement risk is borne by the scheme operator or by prefunded participants.

### Daylight Overdraft
A short-term overdraft on a bank's central-bank account during the operating day — used at peak hours when outbound payments exceed inbound. US Fed prices daylight overdrafts (Reg DD); ECB has similar mechanisms for T2 participants. Critical for high-value RTGS flow; the intraday liquidity manager calculates and throttles to avoid breaches.

### Prefunding
For some instant rails (FedNow, RTP), the bank holds a pre-positioned balance at the operator (Fed Master Account for FedNow; TCH-held position at Fed for RTP) from which outbound payments draw and into which inbound payments credit. The scheme cannot settle outbound payments if the bank's prefunded balance is insufficient — driving the need for Liquidity Management Transfer (LMT) tools.

---

## Payment Flow Mechanics

### Push vs. Pull
- **Push** payments are initiated by the *payer* (e.g., online bank transfer, UPI P2P, FedWire). The payer authorises and the funds move forward.
- **Pull** payments are initiated by the *payee* against a pre-authorised mandate (e.g., Direct Debit, card POS — though card is more nuanced, ACH debit). The payer's bank checks the mandate, then debits.

This distinction matters because fraud and dispute economics differ sharply: push fraud (APP fraud) is hard to reverse and shifts liability towards the customer / receiving bank; pull fraud (unauthorised debit) is well-protected by Reg E and Bacs Direct Debit Guarantee.

### Credit Transfer vs. Direct Debit
The ISO 20022 / scheme terminology for push (Credit Transfer — SCT, pacs.008) vs. pull (Direct Debit — SDD, pain.008 / pacs.003).

### Authorised vs. Unauthorised Transactions
- **Authorised** — the customer (or their authorised agent) intended the payment. Even when fraud is involved (e.g., APP fraud), if the customer authorised the actual send, the transaction is authorised in the legal sense.
- **Unauthorised** — the customer did not authorise the transaction (e.g., account takeover, card cloning). Reg E (US), PSRs 2017 (UK), PSD2 (EU) give strong customer protections on unauthorised transactions: typically refund within 1 business day.

The line between the two is the central battleground for APP fraud reimbursement debates. UK PSR SD18 effectively recategorises *some* authorised fraud (APP) as reimbursable in a way that resembles unauthorised treatment.

### APP Fraud (Authorised Push Payment)
A push payment authorised by the customer themselves, but where the customer was deceived (impersonation, romance, investment scam, invoice redirection). Difficult to reverse because the underlying authorisation is valid. UK PSR SD18 mandates 50/50 sender-receiver bank reimbursement; US CFPB pressure on Zelle is in similar direction; EU is debating.

### Mandate
A pre-authorisation given by the customer for recurring or future payments. Examples: SEPA DD mandate, Bacs DD mandate, UPI AutoPay mandate. The engine stores mandates with effective dates, amounts, frequency, revocation rights. Mandate management is a sub-system in its own right.

### STP — Straight-Through Processing
A payment that flows from initiation to settlement without human intervention. The opposite is a payment that hits a **repair queue** for manual fixing (missing field, sanction hit needing investigation, format error). STP rate is a top operational KPI; below 90% is typically considered poor.

### Repair vs. Exception
- **Repair** — fixable issues (missing intermediary BIC, malformed remittance text); operator corrects + resubmits.
- **Exception** — unfixable in this run (sanction true hit, counterparty bank unreachable, customer instruction needed); routed to dedicated workflow.

### gpi Tracker / UETR
A SWIFT-defined unique end-to-end transaction reference. The UETR is generated at the originating bank and travels through every hop. gpi banks update a central tracker, allowing real-time end-to-end visibility. UETR is mandatory on CBPR+ MX cross-border payments.

---

## Capacity / Operational Metrics

### TPS — Transactions per Second
Throughput unit. Real-time rails define peak TPS targets — UPI handles >1500 TPS sustained, FedNow + RTP target similar order of magnitude. Engine procurement decisions hinge on peak + sustained TPS requirements over the bank's footprint.

### Latency vs. Throughput
- **Latency** — time to process a single payment (initiation → ACK).
- **Throughput** — payments processed per unit time.

A system can have low latency and low throughput, or high throughput with bursty latency. Instant rails need both — low latency *and* high throughput.

### RTO / RPO
Resilience metrics:
- **Recovery Time Objective** — maximum tolerable downtime after a failure.
- **Recovery Point Objective** — maximum tolerable data loss.

For tier-1 payment engines, RTO is typically minutes, RPO is typically zero (no committed payment can be lost). Drives active-active multi-region architectures.

---

## Currency / FX

### Convertibility
The ease with which a currency can be freely exchanged for another. **Fully convertible**: USD, EUR, GBP, JPY, CHF, AUD, CAD, SGD. **Partially convertible**: INR (current-account convertible, capital-account restricted), CNY (limited capital-account), RUB (under sanctions). **Non-convertible** or heavily restricted: many emerging-market currencies.

### Onshore vs. Offshore Currency
A currency traded *within* its issuing jurisdiction (onshore) vs. *outside* it (offshore). For currencies with capital controls, the two markets are price-distinct. **CNY** (onshore) vs. **CNH** (offshore in HK / SG / London) is the canonical example: same currency code, different settlement infrastructure, different rates, different rule sets.

### NDF — Non-Deliverable Forward
An FX forward contract on a non-fully-convertible currency, settled in a freely-deliverable currency (typically USD). No actual delivery of the restricted currency. Used heavily for INR, CNY, KRW, BRL hedging.

---

## Open Banking

### AISP / PISP / CBPII
PSD2 / PSRs 2017 service categories:
- **AISP** (Account Information Service Provider) — read-only access to account data.
- **PISP** (Payment Initiation Service Provider) — initiates a payment on the customer's behalf, typically over the existing scheme.
- **CBPII** (Card-Based Payment Instrument Issuer) — issues a card-based instrument backed by an account at another bank.

### ASPSP
**Account Servicing Payment Service Provider** — the bank that holds the customer's account. The ASPSP exposes the regulated APIs that AISPs / PISPs / CBPIIs use.

### TPP — Third Party Provider
Umbrella term for AISP / PISP / CBPII. The TPP needs FCA / EBA / national authorisation and dynamic registration.

### SCA Exemptions
Defined under EBA RTS on SCA — situations where SCA is not required. Includes: low-value (< EUR 30 single, EUR 100 cumulative), trusted beneficiary whitelisted by the customer, transaction risk analysis (TRA) for low-fraud PSPs, recurring transactions of identical amount, secure corporate channels. Each exemption has eligibility conditions the engine must enforce.

---

## Regulatory Structure (EU / UK)

### Directive vs. Regulation (EU)
- A **Directive** sets out objectives that each member state must transpose into national law. Transposition gives flexibility but also fragmentation. PSD2 is a Directive.
- A **Regulation** is directly applicable across all member states without national transposition. GDPR, DORA, MiCA, Instant Payments Regulation are Regulations.

The PSD3 / PSR package deliberately moves some PSD2 content from Directive to Regulation form (the PSR), reducing fragmentation.

### RTS / ITS
- **Regulatory Technical Standards** (RTS) — binding technical rules drafted by the EBA / ESMA / EIOPA and adopted by the European Commission. RTS on SCA defines acceptable factors, exemptions, and the dedicated Open Banking interface.
- **Implementing Technical Standards** (ITS) — binding standards on uniform application — e.g., ITS on data submission formats.

Both have direct legal force.

### Guidance vs. Rules
Regulators issue **rules** (binding) and **guidance** (non-binding but practically expected). FCA Handbook rules are binding; FCA finalised guidance is heavily expected in supervision but not formal law. Most regulators publish "Dear CEO" letters that fall in the guidance category but are practically binding for the named institutions.

### Onshoring (UK)
The process by which the UK, post-Brexit, retained EU legislation as UK law as of 1 January 2021. The retained EU laws can now be amended unilaterally by the UK. PSRs 2017 (UK's PSD2 implementation) and onshored IFR are examples.

### Equivalence
A determination by one jurisdiction that another's regulatory regime delivers equivalent outcomes — used for market-access decisions (e.g., third-country CCPs accessing the EU). Different from passporting, which is automatic intra-EU.

### Passporting
The right of an EU-authorised PSP to operate across the EU on the basis of its home authorisation. UK PSPs lost EU passporting post-Brexit.

---

## Data Privacy

### Data Controller / Processor / DPO
- **Controller** — the party that determines the purposes and means of processing.
- **Processor** — the party that processes on the controller's behalf, on instruction.
- **DPO** — Data Protection Officer; mandatory for many regulated entities under GDPR; independent and reports to the highest management.

The payment engine vendor is typically a **processor**; the bank is the **controller**. Contractually formalised in Data Processing Agreements (DPA).

### Lawful Basis (GDPR Art. 6)
For each processing activity, the controller must identify a lawful basis: consent, contract necessity, legal obligation, vital interests, public task, legitimate interests. Most bank-payment processing relies on contract necessity (executing the customer's payment) or legal obligation (AML / sanctions). Marketing-adjacent profiling needs consent.

### Adequacy Decision
EU Commission determination that a third country's data-protection regime is adequate — allowing data transfer without additional safeguards. EU-UK has an adequacy decision; EU-US has Data Privacy Framework (replacing Privacy Shield); many other countries do not.

### SCC / BCR
Mechanisms for lawful cross-border data transfer when no adequacy exists:
- **Standard Contractual Clauses (SCC)** — EC-approved contract templates between exporter and importer.
- **Binding Corporate Rules (BCR)** — for intra-group transfers; approved by competent authority.

### DPIA — Data Protection Impact Assessment
Required for high-risk processing (e.g., large-scale profiling, new tech, sensitive data). Identifies risks and mitigations. Payment fraud monitoring with ML typically requires a DPIA.

---

## Other Useful Distinctions

### Customer-Initiated vs. Merchant-Initiated Transaction (CIT vs. MIT)
Card industry term. **CIT** is the customer actively triggering the transaction. **MIT** is the merchant initiating against a customer-on-file credential (e.g., recurring subscription, no-show charge, top-up). PSD2 SCA treats them differently — MITs after the first CIT can be exempt from SCA.

### Funds Availability vs. Settlement
Customer's *funds-availability* is when the customer can use the money — typically governed by consumer-protection rules (Reg CC in US, scheme rules elsewhere). *Settlement* is when the inter-bank money has moved. The two often differ — banks may make funds available before underlying settlement, taking the risk.

### Soft Decline vs. Hard Decline
Card-issuing terminology. **Soft decline** is a temporary refusal where the merchant is expected to retry (or step-up) — e.g., insufficient funds in current state, SCA challenge needed. **Hard decline** is permanent for that attempt — e.g., closed account, fraud-blocked card.

### Reachability
For a payment hub, *reachability* means whether a target BIC / sort code / account is addressable through a chosen rail. SEPA reachability is a directory query; bilateral reach via correspondent BICs is a relationship database. Reachability data is foundational to the routing engine.

---

## How To Use This File

- Linking from other docs: prefer `[primary sanctions](concepts.md#primary-sanctions)` over inline paragraph repetition.
- Updating: when a regulator changes a definition (e.g., 50% Rule clarification), update here and let other docs cite.
- For one-line lookup of an acronym, see [glossary.md](glossary.md). For framing — read this file.

---

## Open Questions

- [ ] Confirm the bank's standard internal definitions where they differ from the above (e.g., the bank's PEP risk-rating model may differ from FATF baseline).
- [ ] Decide whether to extract sub-files (e.g., a dedicated "sanctions concepts" file) as content grows.
- [ ] Identify which concepts need diagrams (push vs. pull flows, nostro/vostro mechanics, settlement-vs-clearing timeline) — candidate for a dedicated diagrams file.
