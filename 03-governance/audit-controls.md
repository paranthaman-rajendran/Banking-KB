# Audit & Lineage Controls

Every retrieval and every change to the index must be reconstructable for audit and regulatory investigation.

---

## What Must Be Logged

### Retrieval events
- `user_id`, `agent_id` (if agentic), `session_id`
- `query_text` (full)
- `filter_set` (effective entitlement filter applied)
- `chunk_ids_returned` (full list, pre-rerank and post-rerank)
- `chunks_used_in_response` (post-LLM citation set)
- `llm_model_id` and `llm_version`
- `response_text`
- `timestamp` (UTC)
- `latency_ms`
- `cost_estimate` (token + infra)

### Ingestion events
- `document_id`, `document_version`
- `source_system`, `source_url`
- `chunking_strategy`, `embedding_model`, `embedding_version`
- `approval_chain` (full state transitions with approver IDs)
- `chunk_count` and per-chunk hashes
- `ingested_at`, `indexed_at`

### Entitlement events
- All entitlement reads, role changes, wall-crossing approvals
- Stored separately with longer retention than retrieval logs

---

## Storage & Retention

| Log Type | Retention | Storage | Access |
|---|---|---|---|
| Retrieval events | 7 years (regulator default) | Append-only, immutable (S3 + Object Lock) | Audit, Compliance |
| Ingestion events | 10 years | Append-only, immutable | Audit, Compliance, Engineering |
| Entitlement events | 10 years | Append-only, immutable | Audit, Compliance, HR |
| LLM input/output pairs | Per data classification + 1 year minimum | Encrypted at rest | Audit (with approval) |

---

## Lineage Chain

For any response, the audit log must allow reconstruction of:

```
User Query
  → Entitlement Snapshot at query time
  → Filter Set applied
  → Candidate chunks from vector + sparse search
  → Reranker scores
  → Final chunks sent to LLM
  → LLM prompt (with model + version)
  → LLM response
  → Citations returned to user
```

And for each chunk in that chain:

```
Chunk
  → Document version + chunk hash
  → Source document (path + system)
  → Approval chain (who approved, when, on what state)
  → Ingestion run (when, with what pipeline version)
```

This is required for any regulatory investigation (e.g., "show me everything the system told the trader about Product X on 2025-05-12").

---

## Point-in-time Reconstruction

The platform must support:
- "What did the KB return for query Q at time T?" — replay against the index state at T.
- "What was the canonical version of policy P on date D?" — return the chunk set that was `Canonical` at D.
- "Who approved version V of document X?" — return the full approval chain.

These features are non-negotiable for regulator-facing audit.

---

## Required Monitoring

| Metric | Alert threshold |
|---|---|
| Access control leakage (restricted chunk to unauthorized user) | Any occurrence — page on-call Compliance |
| Faithfulness drop in production sampling | < 90% over 1h window |
| Citation accuracy drop | < 95% over 1h window |
| Hallucination rate | > 2% over 1h window |
| Ingestion failures | Any failure on a `Canonical` doc |
| Stale chunks in index (past `expiry_date`) | Any occurrence |
| Entitlement TTL violations | > 15 min stale entitlement used |

Dashboards in Grafana; alerts via on-call rotation.

---

## Open Questions for Phase 1 Sign-off

- [ ] Confirm immutability requirements with Compliance (regulator-specific).
- [ ] LLM input/output retention policy — bank policy vs. regulator minimum.
- [ ] Who owns the audit dashboard — Compliance, Tech Risk, or shared?
