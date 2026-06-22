# Payments — Golden Questions (Seed)

Seed eval dataset covering rails, standards, regulation, and operations. Expand to 50+ per use case before any Payments pilot launches.

> Curation owners: Payments Operations + Compliance + Engineering.
> Each question must have expected answer, expected citation source(s), difficulty tier.

---

## Tiers

| Tier | Description | Target Count |
|---|---|---|
| `easy` | Single-document lookup, explicit answer | 20+ |
| `medium` | Multi-section synthesis or 2-doc comparison | 20+ |
| `hard` | Cross-source (rail + regulation + SOP) reasoning | 10+ |

Seed coverage below: 96 questions across India, USA, UK, cross-border, standards, regulatory, ops, cards, architecture/engines, vendor deep-dives (Finastra GPP, Oracle OBPM), per-jurisdiction regulatory (USA, UK, EU, Singapore, China, Japan, cross-border), and foundational concepts (primary/secondary sanctions, CDD/EDD/SDD, nostro/vostro, finality, APP fraud, etc.).

---

## Seed Questions

### Domestic India — UPI / IMPS / NEFT / RTGS

1. `easy` — What is the current per-transaction limit for IMPS as per NPCI?
2. `easy` — Are NEFT charges applicable for online retail transactions today?
3. `medium` — A UPI payment failed with technical decline (TD) — what's the customer-facing SOP and the auto-reversal SLA?
4. `medium` — What's the difference between RTGS finality and IMPS settlement finality?
5. `hard` — A merchant wants to set up UPI AutoPay for SaaS subscriptions — which RBI recurring transactions framework clauses apply, and what's our PSP-side checklist?
6. `easy` — What does VPA stand for and how is it resolved?
7. `medium` — When does NPCI's DMS (Dispute Management System) become the canonical authority for a UPI dispute?
8. `hard` — A customer reports a UPI fraud (social engineering APP fraud) — walk through the playbook from PSP → bank → NPCI → law enforcement.

### Domestic USA — ACH / FedWire / FedNow / RTP / CHIPS / Zelle

34. `easy` — What is the per-transaction cap for Same-Day ACH today, and when was it last raised?
35. `easy` — What does SEC code "WEB" mean, and what's the ODFI's account validation obligation before first WEB debit?
36. `medium` — Compare FedNow and RTP (TCH) on settlement model, per-txn cap, and FI coverage.
37. `medium` — What is the return window for an unauthorized consumer ACH debit (R10), and which Reg E rights apply?
38. `hard` — A wholesale customer wants to recall a USD 10M FedWire sent to the wrong beneficiary 90 minutes ago. What's possible under Reg J, and what's the realistic outcome?
39. `medium` — When does Reg II's debit routing requirement apply to card-not-present transactions today?
40. `easy` — What's the difference between FedACH and EPN, and how does a bank choose?
41. `hard` — A Zelle customer reports an APP fraud where they were tricked into sending USD 5,000. Walk through the dispute path under the current EWS / CFPB framework.
42. `medium` — What's CHIPS's settlement model, and why do correspondent USD flows favour it over FedWire?
43. `easy` — When did FedWire complete or target ISO 20022 migration?
44. `medium` — A merchant aggregator wants to register as a Third-Party Sender for ACH origination — what NACHA obligations apply?

### Domestic UK — FPS / CHAPS / Bacs / CoP / APP Fraud / Open Banking

45. `easy` — What is the per-transaction scheme cap for Faster Payments today?
46. `easy` — What does CHAPS stand for, and who operates it post-2017?
47. `medium` — What's the Bacs Direct Debit cycle (input → processing → settlement) and what does ARUDD signal?
48. `hard` — An FPS payment was made to a fraudster after the customer ignored a CoP "name mismatch" warning. How does APP Fraud Reimbursement apply under PSR's mandate (Oct 2024)?
49. `medium` — What's the Direct Debit Guarantee and how does it shape originator-side risk?
50. `medium` — What's the difference between Sweeping VRP and Commercial VRP, and which one is mandated free under CMA9?
51. `hard` — A CHAPS payment for a property completion went to the wrong solicitor's account due to a typo not caught by CoP — what's the recovery path under CHAPS Reference Manual rules?
52. `easy` — Which UK regulator issues PSR SD18, and what does it require?
53. `medium` — How does the FCA Consumer Duty (July 2023) reshape payments customer-journey design?
54. `easy` — What's the cut-off for Bacs Direct Credit input on T-2 for value date T?
55. `hard` — A PSP receives a HMT sanctions match on an inbound FPS — what's the operational hold, customer comms, and OFSI reporting obligation?
56. `medium` — What changed for CHAPS message structure post-ISO 20022 migration (2023)?

### Architecture — Lifecycle, Systems, Engines

57. `easy` — In the canonical payment lifecycle, at which stage does sanctions screening run, and why is it serial relative to funding check?
58. `medium` — Describe the role of a payment hub in routing a USD 50,000 corporate payment to a US beneficiary — which rails would the hub consider and what drives the choice between FedWire, RTP, and FedNow?
59. `hard` — Map the systems involved (initiation, control, processing, settlement, posting) for a UK retail FPS payment with a CoP "close match" outcome — name a canonical sequence of system handoffs and the failure modes at each.
60. `medium` — What's the difference between Finastra GPP and ACI UP at a market-positioning level, and which would you pick for a US tier-1 FedNow + RTP rollout?
61. `easy` — Which vendor product is most commonly associated with sanctions screening at tier-1 banks?
62. `medium` — How does Volante's ISO 20022 transformation differ from a SWIFT Transaction Manager (TM)-based approach?
63. `hard` — A bank is modernising from a legacy in-house payment processor to a cloud-native stack. Which combinations (CBS + hub) appear most often in tier-1 modernisation programmes and what are the trade-offs?
64. `medium` — Why are intraday liquidity systems (SmartStream TLM IL, Planixs Realiti) increasingly critical with the rise of instant rails?
65. `easy` — Which products are commonly used for nostro reconciliation at tier-1 banks?
66. `medium` — Where does the SWIFT gpi tracker fit in the lifecycle, and which stages does it touch?
67. `easy` — What product line did Finastra Global PAYplus (GPP) originate from, and who owns it today?
68. `medium` — In Finastra GPP, what does SmartOps do and where does it sit in the lifecycle?
69. `hard` — A bank running Oracle Banking Payments wants to swap Oracle FCCM for Fircosoft sanctions. Walk through the integration design and the trade-offs that determine whether it's worth doing.
70. `medium` — Compare Finastra GPP and Oracle OBPM on cloud-native posture and CBS integration assumptions.
71. `easy` — Which CBS product is most tightly integrated with Oracle Banking Payments?
72. `medium` — Why do tier-1 GPP and OBPM implementation programmes typically run 18–36 months even though both products are mature?
73. `hard` — A Flexcube tier-1 bank is choosing between staying on OBPM and migrating to Finastra GPP for SWIFT cross-border + SEPA + FedNow. What's the decision frame?

### Regulatory — Per-Jurisdiction + Engine Compliance

74. `easy` — What's the threshold for the FinCEN Travel Rule on US wires, and how does it compare to the FATF baseline?
75. `medium` — Under EU Instant Payments Regulation, when must an EU PSP that offers SEPA Credit Transfer also offer SCT Inst, and at what price?
76. `hard` — A Singapore-licensed Major Payment Institution wants to route customer remittance from SG to IN via PayNow ↔ UPI. Which MAS, RBI, and FATF rules apply, and what does the payment engine need to do at each step?
77. `medium` — Compare US OFAC sanctions reach to UK OFSI sanctions reach in the context of a USD-denominated payment between two non-US banks.
78. `easy` — Which PSR specific direction mandates Confirmation of Payee in the UK?
79. `hard` — A foreign bank's CN entity wants to send customer transaction data to head office for global AML monitoring. Which laws apply (CSL / DSL / PIPL) and what mechanisms make this lawful?
80. `medium` — What is BoP code reporting under SAFE in China, and how does the payment engine integrate?
81. `easy` — Under Japan's Funds Settlement Act, what are the three tiers of Funds Transfer Service Provider and what limits attach to each?
82. `medium` — Under DORA, what does a tier-1 EU bank's payment hub vendor (e.g., Finastra, Oracle, Volante) need to expect in terms of EU direct oversight?
83. `hard` — Map five engine features (sanctions screening, Travel Rule enforcement, CoP/VoP, SCA, ISO 20022 nativeness) to the jurisdictions and regulations that drive them.
84. `medium` — Why is CNY routing decision (onshore CNY vs. offshore CNH) a critical engine routing concern?

### Foundational Concepts

85. `easy` — What's the difference between primary and secondary sanctions, and which one captures a non-US bank in a USD-correspondent chain?
86. `medium` — Walk through OFAC's 50% Rule and why beneficial-ownership data (not just name matching) is required to apply it.
87. `easy` — Distinguish "blocked" from "rejected" transactions under OFAC.
88. `medium` — What's the difference between CDD, EDD, and SDD, and what triggers a customer being moved from CDD to EDD?
89. `easy` — Define nostro, vostro, and loro from the same account perspective.
90. `medium` — Distinguish clearing from settlement; give one rail where they collapse into a single moment and one where they don't.
91. `hard` — Why is APP fraud structurally hard to reimburse under traditional "unauthorised transaction" frameworks, and how does UK PSR SD18 redefine the line?
92. `easy` — What does Herstatt risk mean and how does CLS solve it?
93. `medium` — Distinguish push from pull payments; explain why their fraud and liability profiles differ.
94. `easy` — What's the difference between source of funds and source of wealth?
95. `medium` — Distinguish a shell company from a front company in AML risk terms.
96. `hard` — Explain why ISO 20022 structured fields make "wire stripping" harder than the MT free-text era.

### Cross-Border — SWIFT / SEPA / Cards / FedNow

9. `easy` — What does UETR stand for, and which messages carry it?
10. `easy` — When does SWIFT MT sunset for cross-border payments?
11. `medium` — Translate the key fields of an MT103 into the equivalent pacs.008 structure.
12. `medium` — What's the EU IPR mandate on PSPs offering credit transfers?
13. `hard` — A cross-border USD payment is held by OFAC screening — what's the escalation, hold duration, and customer-communication SOP?
14. `medium` — What's the difference between MT202 and MT202COV, and when is each used?
15. `hard` — A pacs.008 message fails CBPR+ validation at the SWIFT FINplus gateway — describe the diagnostic flow.
16. `easy` — What is SCT Inst's per-transaction cap currently?
17. `medium` — Compare FedNow and RTP (TCH) on settlement model and reach.

### ISO 20022 & Standards

18. `easy` — What does pain.001 mean and who initiates it?
19. `medium` — In ISO 20022, how is the ordering customer's structured address represented?
20. `medium` — Map ISO 8583 DE 39 (response codes 00, 05, 51) to customer-facing failure messages.
21. `hard` — A network token in DE 2 needs to be detokenized for a chargeback investigation — what's the PCI scope implication?

### Regulatory & Sanctions

22. `easy` — Where is RBI's data localization requirement defined, and what's its scope?
23. `medium` — What SCA exemptions does PSD2 EBA RTS allow for low-value contactless?
24. `hard` — A cross-border MT103 has incomplete originator info (missing DE 50 address). Travel Rule status?
25. `medium` — What's UK PSR's APP Fraud Reimbursement obligation, and who funds it?
26. `easy` — Which OFAC list update cadence are we ingesting from?

### Operations

27. `easy` — What's our internal SLA for instant payment failure reversal alerts?
28. `medium` — Describe the reconciliation pipeline for nostro USD account at correspondent X — frequency, source of truth, exception handling.
29. `hard` — An NPCI degraded-mode incident is declared at 22:00 IST — what's the desk-side runbook, customer comms, and reporting obligation?
30. `medium` — How does the dispute SLA differ between a UPI P2P fraud and a card chargeback?

### Tokenization & Cards

31. `medium` — What's the difference between a network token and a PSP token, and what's their PCI implication?
32. `easy` — When did RBI's card tokenization mandate take effect, and what does it forbid?
33. `hard` — A 3DS v2 frictionless flow returned ECI=05 — what does that mean for liability shift on a chargeback?

---

## Curation Schema

```yaml
id: pay-q-001
text: "What is the current per-transaction limit for IMPS as per NPCI?"
difficulty: easy
expected_answer: "INR 5,00,000 per transaction as per NPCI Operating Circular dated YYYY-MM-DD."
expected_sources:
  - doc_id: npci-imps-circular-YYYY
    section: Transaction Limits
required_metadata_filters:
  domain: Payments
  sub_domain: DomesticIN
  product_class: IMPS
curated_by: <ops lead>
reviewed_by: <compliance reviewer>
curated_at: 2025-XX-XX
```

---

## Eval Targets (when promoted to pilot)

Same targets as the [Structured Products pilot](../04-pilot-structured-products/success-criteria.md):

| Metric | Target |
|---|---|
| Retrieval Precision@5 | > 80% |
| Retrieval Recall@10 | > 75% |
| Faithfulness | > 95% |
| Citation Accuracy | > 98% |
| Hallucination Rate | < 1% |
| Latency P95 | < 3s (copilot), < 500ms (API) |
| Access Control Leakage | 0% |

**Payments-specific addition**:

| Metric | Target | Rationale |
|---|---|---|
| Sanctions-content correct citation | 100% | Wrong sanctions guidance is regulator-reportable |
| Stale-rule citation rate (citing a superseded circular) | 0% | Rail rules change frequently |

---

## Open Questions

- [ ] Confirm which scenarios desk leads consider highest-value for the first pilot (UPI dispute? cross-border investigation? sanctions explainability?).
- [ ] Identify the SME curator per category.
- [ ] Establish refresh cadence for expected answers (some depend on time-bound limits / regulations).
