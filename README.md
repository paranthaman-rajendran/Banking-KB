# Banking GenAI Knowledge Base — Workspace

Phase 1 scaffolding for a Governed Retrieval Platform serving Products & Capital Markets.

> Source: `E:\developer\domain\Banking_GenAI_Knowledge_Base_Guide_v2.md`
> Phase: **1 — Foundations (Weeks 1–4)**
> Pilot domain: **Structured Products**

This workspace contains the non-code assets the guide says must come first: taxonomy, metadata schema, source curation policy, governance, and pilot scope. No technology decisions yet — those are last.

---

## Navigation

| Folder | Purpose | Phase 1 Deliverable |
|---|---|---|
| [consumers.md](consumers.md) | Consumer matrix (Step 1) | Defines who the KB serves |
| [01-taxonomy/](01-taxonomy/) | Domain tree + metadata schema | **Taxonomy document**, **metadata schema** |
| [02-source-curation/](02-source-curation/) | Sources, freshness, lifecycle | Source curation policy |
| [03-governance/](03-governance/) | Classification, access control, audit | **Governance policy** |
| [04-pilot-structured-products/](04-pilot-structured-products/) | Pilot scope and success criteria | **Pilot scope** |
| [05-roadmap/](05-roadmap/) | Phase 1–6 timeline | Sequencing |
| [06-payments/](06-payments/) | Payments sub-domain knowledge (rails, standards, regulatory, vendors) | Sub-domain content prep |
| [07-core-banking/](07-core-banking/) | Core Banking sub-domain — CBS platforms + Retail + Wholesale/Corporate | Sub-domain content prep |

---

## Phase 1 Exit Checklist

- [ ] Domain taxonomy reviewed and approved by capital markets desks + compliance
- [ ] Metadata schema agreed (8–10 mandatory fields)
- [ ] Pilot domain confirmed (Structured Products)
- [ ] Document lifecycle workflow signed off (Draft → Canonical)
- [ ] Success metrics for pilot defined
- [ ] Stakeholders identified for each consumer segment
- [ ] Governance policy approved by Compliance and Legal

---

## Principal Engineer Priority Order

Do not reorder:

1. Consumer definition + use cases
2. Domain taxonomy (capital markets sub-domains)
3. Metadata schema
4. Governance + access control design
5. Source curation + canonical lifecycle
6. Retrieval architecture (hybrid RAG)
7. Entity layer / knowledge graph
8. Agentic workflows
9. Evaluation framework
10. Vector database + embedding model selection ← last

The vector store is an implementation detail. It can be swapped. The long-term assets — taxonomy, governance, entity relationships, retrieval contracts, evaluation datasets — take years to build and cannot be bought.
