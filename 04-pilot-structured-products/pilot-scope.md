# Pilot Scope — Structured Products

**Goal**: end-to-end vertical slice. Small scope, high quality. This is the Phase 2 deliverable (Weeks 5–10) from the guide.

> If the pilot can't hit its success criteria, no other domain gets onboarded. The point is to prove the platform end-to-end.

---

## In Scope

### Sub-domain
- `CapitalMarkets / StructuredProducts` only.

### Product classes
- Autocallables & Barrier Products
- Principal Protected Notes (PPN)

(CLN, TRS, and exotic payoffs are explicit out-of-scope for the pilot.)

### Consumers
- Primary: Structuring Desk (read-write, agentic copilot)
- Secondary: Sales (read-only, Q&A copilot)

### Geographies
- EU + APAC (covers MiFID II + SEBI angles)

### Sources
See [source-checklist.md](source-checklist.md). Approximately 50–100 historical term sheets plus supporting policy and legal docs.

---

## Out of Scope (Phase 2)

- Other product classes (CLN, TRS, Exotics)
- Real-time pricing — fetched via tool calls, not retrieved
- Customer-facing assistants
- Entity layer / knowledge graph — added in Phase 3
- Cross-domain queries (touches Risk or Compliance docs across sub-domains)
- Restricted-tier content (no MNPI in the pilot)

---

## Build Components

| Component | Scope |
|---|---|
| Ingestion pipeline | Structure-aware chunking for term sheets (by Economics, Risks, Legal, Payoff sections) |
| Embedding | One finance-tuned model (recommendation: `voyage-finance-2`); fine-tuning deferred to Phase 3 |
| Hybrid retrieval | Dense + BM25 with metadata pre-filter; no reranker yet |
| Metadata enforcement | Full ingestion gate per [metadata-schema.md](../01-taxonomy/metadata-schema.md) |
| Approval workflow | Manual via SharePoint approval, machine-readable status sync |
| Evaluation | RAGAS-based eval over golden dataset of 50 Q&A pairs (see [golden-questions.md](golden-questions.md)) |
| Audit logging | Full retrieval and ingestion logs per [audit-controls.md](../03-governance/audit-controls.md) |
| Access control | Sensitivity-tier filter at retrieval; desk-level entitlement comes in Phase 5 |

---

## Interfaces (Phase 2)

- **Internal API**: REST endpoint for desk use, with citation contract.
- **Chat copilot**: Internal web UI wrapping the REST API. No MCP yet — that's Phase 4.

---

## Success Criteria

See [success-criteria.md](success-criteria.md) — must all be met before declaring pilot done.

---

## Timeline

| Week | Deliverable |
|---|---|
| 5 | Source corpus ingested, manual approval complete |
| 6 | Ingestion pipeline + chunking + metadata gate live in dev |
| 7 | Hybrid retrieval operational; golden dataset draft (40 questions) |
| 8 | Eval pipeline running; golden dataset finalized (50 questions) |
| 9 | Desk UAT with 5 structurers; iteration on retrieval precision |
| 10 | Pilot exit review — success criteria gate |

---

## Risks

| Risk | Mitigation |
|---|---|
| Term sheets are inconsistent in structure across vintages | Structure-aware chunker with fallback to header-based; manual QA on 10% sample |
| Golden dataset curation is the slowest path | Start at week 5, not week 8; pre-engage structurers for time |
| Compliance gate delays canonical approval | Pre-clear pilot scope with Compliance in Phase 1 |
| Embedding model precision insufficient for exotic payoff language | Acceptable for pilot; fine-tuning deferred to Phase 3 |
