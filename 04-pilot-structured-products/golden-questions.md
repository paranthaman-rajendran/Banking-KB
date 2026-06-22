# Golden Dataset — Structured Products Pilot

Domain expert-curated Q&A pairs. Target: 50 questions covering the product, regulatory, risk, and operational angles.

> Curation owner: Structured Products Desk lead, with Compliance and Operations spot-checks.
> Each question must have: expected answer, expected citation source(s), difficulty tier.

---

## Difficulty Tiers

| Tier | Description | Target Count |
|---|---|---|
| `easy` | Single-document lookup with explicit answer | 20 |
| `medium` | Multi-section synthesis from one document, or comparison across 2 docs | 20 |
| `hard` | Cross-source (term sheet + policy + regulation) reasoning | 10 |

---

## Seed Questions (to be expanded to 50)

### Product specification

1. `easy` — What is the barrier observation frequency for the Autocallable Note ISIN XS1234567890?
2. `easy` — What is the autocall trigger level for the [issuer X] PPN dated 2024-09-15?
3. `easy` — What is the coupon barrier for the Phoenix Autocallable on EuroStoxx 50?
4. `medium` — Compare the participation rates of the two most recently issued PPNs on NIFTY 50.
5. `medium` — For the autocallable issued 2025-02-01, what's the worst-case payoff if all underlyings breach the barrier at maturity?

### Regulatory

6. `medium` — Under MiFID II Article 25, which suitability checks apply when selling a barrier product to a retail client in Germany?
7. `hard` — Does the current [issuer X] autocallable require a KID under PRIIPs? Cite the determining clause.
8. `medium` — Which SEBI provisions govern the distribution of equity-linked structured notes to Indian retail clients?
9. `hard` — A client is reclassified from professional to retail mid-trade — what does our internal policy require? Reference the policy and the underlying regulation.

### Risk & Hedging

10. `medium` — What is the delta hedge construction for an Autocallable Note with two underlyings?
11. `easy` — What is the vega risk limit for the Structured Products desk per the current risk policy?
12. `hard` — For a CPPI-style PPN, how does the bond floor calculation affect the risk allocation at issuance?

### Operations & Settlement

13. `easy` — What is the settlement SOP for a structured note traded on Euroclear?
14. `medium` — A coupon payment failed to settle on T+2 — what's the escalation matrix?

### Comparison / Precedent

15. `hard` — Find the three most recent autocallable issuances with NIFTY 50 as an underlying and summarize their key differences (autocall level, coupon, barrier).
16. `medium` — For a new structuring idea on a worst-of basket of [3 Indian banks], which historical precedents are most similar?

### Pricing & Models

17. `medium` — What pricing model is approved for barrier products on equity baskets?
18. `hard` — A structurer wants to use a stochastic-local-vol model for a new exotic — which model risk policy clauses apply, and what's the approval path?

---

## Curation Process

For each question added:

```yaml
id: q-001
text: "What is the barrier observation frequency for the Autocallable Note ISIN XS1234567890?"
difficulty: easy
expected_answer: "Daily, with closing prices on each trading day, per the term sheet dated 2024-11-12."
expected_sources:
  - doc_id: term-sheet-xs1234567890
    section: Economic Terms
required_metadata_filters:
  domain: CapitalMarkets
  sub_domain: StructuredProducts
  product_class: Autocallable
curated_by: <structurer name>
reviewed_by: <compliance reviewer>
curated_at: 2025-XX-XX
```

---

## Eval Pipeline

```
Golden Dataset (50 questions)
    ↓
Automated Retrieval Eval (RAGAS)
  - Retrieval Precision@5 per question
  - Retrieval Recall@10 per question
  - Citation accuracy
    ↓
LLM-as-Judge for Faithfulness
    ↓
Domain Expert Review (spot-check 10%)
    ↓
Regression Gate (eval must pass before KB update ships)
    ↓
Production Monitoring (live query sampling)
```

---

## Targets (Pilot Exit)

| Metric | Target |
|---|---|
| Retrieval Precision@5 | > 80% |
| Retrieval Recall@10 | > 75% |
| Faithfulness | > 95% |
| Citation Accuracy | > 98% |
| Hallucination Rate | < 1% |
| Latency P95 | < 3s |
| Access Control Leakage | 0% |
