# Consumer Matrix

The architecture depends on who uses the KB and what decisions they make with it. Every retrieval contract, access control rule, and SLA flows from this table.

## Primary Consumers

| Consumer | Characteristics | Key Requirements | Sensitivity Tier Access |
|---|---|---|---|
| Structuring Desks | Design new products, term sheets | Deep product spec retrieval, precedent search | Internal, Confidential |
| Sales & Coverage | Client pitches, pricing queries | Fast retrieval, plain-language answers, citations | Internal, Confidential (client-scoped) |
| Quants & Research | Model calibration, market analytics | Data lineage, formula retrieval, structured data | Internal, Confidential, Restricted (model IP) |
| Risk & Stress Testing | Exposure analysis, scenario queries | Auditability, regulation traceability | Internal, Confidential |
| Compliance & Legal | Regulatory filings, ISDA/CSA review | Strict access control, version locking, audit trail | All tiers including Restricted |
| Product Builders (Internal) | Build market-facing AI products | MCP endpoints, APIs, stable schemas | Per-product scoped |
| Operations & Middle Office | Trade booking, settlement queries | SOPs, runbooks, SLA retrieval | Internal |
| Customer-facing Assistants | External client queries | Strict hallucination controls, restricted data scope | Public only |

---

## Interface Per Consumer

| Consumer | Preferred Interface | Latency Target |
|---|---|---|
| Structuring Desks | Agentic copilot + MCP | < 3s |
| Sales & Coverage | Chat copilot | < 3s |
| Quants & Research | REST API + notebook tools | < 2s |
| Risk & Stress Testing | REST API + dashboards | < 2s |
| Compliance & Legal | Chat copilot with full audit | < 5s |
| Product Builders | MCP servers, REST APIs | < 500ms (API) |
| Operations | Chat copilot embedded in OMS | < 3s |
| Customer-facing | REST API (proxied through compliance filter) | < 2s |

---

## Governance Decision

Build a **Governed Retrieval Platform**, not a single KB. Each consumer connects through a domain-scoped interface (MCP, REST, or agentic) that enforces its own entitlements.

```
┌─────────────────────────────────────────────┐
│           Governed Retrieval Platform        │
│                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │  MCP     │  │  REST    │  │ Agentic  │  │
│  │ Servers  │  │  APIs    │  │   AI     │  │
│  └──────────┘  └──────────┘  └──────────┘  │
│                                             │
│  ┌──────────────────────────────────────┐   │
│  │     Domain Retrieval Services        │   │
│  │  (Capital Markets | Risk | Ops | ...)│   │
│  └──────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

---

## Open Questions for Phase 1 Sign-off

- [ ] Confirm primary pilot consumer (recommendation: Structuring Desk — Structured Products)
- [ ] Identify executive sponsor per consumer segment
- [ ] Confirm whether customer-facing assistants are in scope for v1 (recommend: no)
- [ ] Map each consumer to an existing entitlement source (LDAP group, desk code, etc.)
