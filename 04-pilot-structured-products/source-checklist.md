# Pilot Source Checklist — Structured Products

Concrete documents to ingest for the Phase 2 pilot.

| # | Source | Target Count | Owner | Status |
|---|---|---|---|---|
| 1 | Historical term sheets — Autocallables | 30–50 | Structured Products Desk | [ ] |
| 2 | Historical term sheets — PPNs | 20–30 | Structured Products Desk | [ ] |
| 3 | Product Approval Memos (PAM / NPAC) | 10–20 | Product Approval Committee | [ ] |
| 4 | Payoff definitions (formal spec) | 1 per product class | Quants | [ ] |
| 5 | Risk policy — Structured Products section | 1 | Risk Management | [ ] |
| 6 | ISDA Master Agreement (2002) template | 1 | Legal | [ ] |
| 7 | CSA template (VM-CSA) | 1 | Legal | [ ] |
| 8 | MiFID II Articles 24–25 (Suitability) | Official text + bank interpretation memo | Compliance | [ ] |
| 9 | Internal pricing methodology doc | 1 per product class | Quants | [ ] |
| 10 | Sales suitability checklist | 1 | Sales / Compliance | [ ] |
| 11 | Settlement SOP for structured notes | 1 | Operations | [ ] |
| 12 | Escalation matrix for the desk | 1 | Structured Products Desk | [ ] |

Target total: ~80–120 documents.

---

## Per-document Intake Checklist

For each document, confirm before sending to the ingestion pipeline:

- [ ] All mandatory metadata fields present (per [metadata-schema.md](../01-taxonomy/metadata-schema.md))
- [ ] Document is in `Approved` state in its source system
- [ ] Owner team confirms it can be promoted to `Canonical` for the pilot
- [ ] Sensitivity tier reviewed by Compliance (no MNPI / Restricted in the pilot)
- [ ] Effective and expiry dates set
- [ ] Geography correctly tagged

---

## Quality Sample

Before pilot ingestion goes live, manually QA 10% of the corpus:
- Verify chunking did not split mid-clause or mid-payoff formula.
- Verify metadata propagated to every chunk.
- Spot-check 5 chunks against the source document for fidelity.

---

## Open Items

- [ ] Confirm whether legacy term sheets (pre-2020) are in scope. They use older payoff conventions and may pollute retrieval precision.
- [ ] Decide whether to redact specific issuer or client names in the pilot corpus to allow broader desk access.
