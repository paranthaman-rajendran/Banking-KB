# Implementation Roadmap

Full Phase 1–6 timeline mirroring the guide's roadmap. Phase 1 is the current focus; later phases are sketched so the platform direction stays consistent.

---

## Phase 1 — Foundations (Weeks 1–4) ← CURRENT

**Goal**: don't touch technology yet. Design the taxonomy and governance.

- Finalize domain taxonomy with capital markets desks and compliance — [01-taxonomy/taxonomy.md](../01-taxonomy/taxonomy.md)
- Define metadata schema (minimum viable — 8–10 fields) — [01-taxonomy/metadata-schema.md](../01-taxonomy/metadata-schema.md)
- Identify first pilot domain (selected: Structured Products) — [04-pilot-structured-products/pilot-scope.md](../04-pilot-structured-products/pilot-scope.md)
- Establish document lifecycle workflow (Draft → Canonical) — [02-source-curation/canonical-lifecycle.md](../02-source-curation/canonical-lifecycle.md)
- Define success metrics for the pilot — [04-pilot-structured-products/success-criteria.md](../04-pilot-structured-products/success-criteria.md)

**Deliverables**: Taxonomy document, metadata schema, governance policy, pilot scope. (All scaffolded in this workspace.)

---

## Phase 2 — Pilot Domain: Structured Products (Weeks 5–10)

**Goal**: end-to-end vertical slice, small scope, high quality.

Source documents:
- 50–100 historical term sheets
- Product Approval Memos
- Payoff definitions and risk policies
- Relevant ISDA / CSA templates
- MiFID II suitability rules

Build:
- Ingestion pipeline with structure-aware chunking
- Hybrid retrieval (dense + BM25) with metadata filters
- Golden dataset: 50 Q&A pairs curated by structuring desk
- Evaluation pipeline (RAGAS)

Success criteria: Retrieval Precision@5 > 80%, Faithfulness > 95%, no access control leakage.

---

## Phase 3 — Expand Sources + Add Entity Layer (Weeks 11–16)

- Ingest regulatory corpus (MiFID II, EMIR, SEBI circulars)
- Add research reports and credit ratings
- Build Entity Catalog: Products ↔ Regulations ↔ Risk Rules
- Introduce reranker
- Add audit logging at production grade

---

## Phase 4 — Agentic Workflows (Weeks 17–22)

- Build Product Structuring Agent (Pattern 1 from the guide)
- Build Regulatory Change Impact Agent (Pattern 2)
- Expose as MCP servers for internal consumers:
  - `mcp://capital-markets-kb/products`
  - `mcp://capital-markets-kb/risk`
  - `mcp://capital-markets-kb/compliance`
  - `mcp://capital-markets-kb/operations`
  - `mcp://capital-markets-kb/research`
  - `mcp://capital-markets-kb/reference-data`
- Load test at desk scale

---

## Phase 5 — Governance Hardening (Weeks 23–26)

- Full RBAC + desk-level entitlements
- Data lineage end-to-end
- Approval workflow automation
- Point-in-time retrieval (for regulatory investigations)
- Regression gate in CI/CD pipeline

---

## Phase 6 — Scale Out (Months 7–12)

Expand to remaining domains:

| Domain | Key Sources | Consumer |
|---|---|---|
| Fixed Income | Prospectuses, Bloomberg data, risk models | Rates desk, Risk |
| FX & Rates | ISDA definitions, FRTB docs | FX desk |
| Risk & XVA | CVA model docs, SA-CCR methodology | Risk Engineering |
| Compliance | Full regulatory corpus by jurisdiction | Compliance |
| Operations | All SOPs, SWIFT specs, settlement runbooks | Middle/Back Office |
| Wealth | Product shelf, suitability rules, fund docs | Advisory |

Expose production MCP servers, REST APIs, and agentic interfaces.

---

## Critical Pitfalls (Reminders)

| Pitfall | Why It Hurts | Mitigation |
|---|---|---|
| Starting with vector DB selection | Wrong anchor — tech is the last decision | Start with taxonomy and governance |
| Ingesting unapproved documents | Hallucinations from outdated/incorrect sources | Canonical approval gate before indexing |
| Fixed-size chunking | Destroys semantic structure of term sheets and clauses | Structure-aware chunking by document type |
| Access control in the prompt | Restricted data leaks to LLM, compliance breach | Pre-filter at retrieval, never post-filter |
| No evaluation before launch | Can't detect hallucinations or precision drops | Golden dataset + regression gate |
| Single embedding model | Poor precision on financial jargon | Finance-tuned embeddings (voyage-finance-2) |
| Ignoring real-time vs. static data | Stale pricing or rates in responses | Separate pipelines; live data via tool calls |
| Monolithic KB | Access control becomes impossible at scale | Domain-scoped namespaces from day one |
