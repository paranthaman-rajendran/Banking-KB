# Pilot Success Criteria

The Phase 2 pilot exits successfully only when ALL criteria are met. Partial credit does not unlock Phase 3.

---

## Quantitative

| Metric | Target | Measurement |
|---|---|---|
| Retrieval Precision@5 | > 80% | RAGAS on golden dataset |
| Retrieval Recall@10 | > 75% | RAGAS on golden dataset |
| Faithfulness | > 95% | LLM-as-judge + spot-check |
| Citation Accuracy | > 98% | Automated source verification |
| Hallucination Rate | < 1% | LLM-as-judge + UAT feedback |
| Latency P95 (REST) | < 500ms (retrieval) / < 3s (with LLM) | Production sampling |
| Access Control Leakage | **0%** | Red-team test + audit log review |
| Ingestion failures on Canonical docs | 0 | Pipeline metrics |

---

## Qualitative

- [ ] Five structurers complete UAT and report the copilot is "useful for everyday work" (3 of 5 minimum).
- [ ] Compliance signs off that the pilot meets MiFID II and SEBI handling requirements for the in-scope sources.
- [ ] Risk signs off that no Restricted-tier content leaked into the pilot corpus.
- [ ] Operations confirms SOP retrieval works for the three most common settlement scenarios.

---

## Process

- [ ] Golden dataset of 50 questions exists, fully curated and reviewed.
- [ ] Eval pipeline runs on every ingestion or retrieval-config change.
- [ ] Regression gate is wired into the deploy path — no ship without eval pass.
- [ ] Full audit log exists for every retrieval during UAT.
- [ ] Point-in-time replay demonstrated to Compliance.

---

## Documentation

- [ ] Architecture decision records (ADRs) for: chunking strategy, embedding choice, namespace strategy.
- [ ] Runbook for ingestion pipeline operators.
- [ ] Runbook for retrieval failures (slow, no results, leakage).
- [ ] Phase 3 plan drafted and reviewed.

---

## Hard Stops (Pilot Fails If…)

- Any single access control leakage incident — no matter how small. The platform must be structurally incapable of leaking, not just statistically unlikely.
- Hallucination rate over 1% sustained across the eval set.
- Compliance unable to sign off on data handling.
- Latency above 5s P95 — UX unusable.

A hard stop means the pilot does not exit. Iterate or restart.
