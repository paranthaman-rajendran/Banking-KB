# Access Control

**Critical rule**: access control filtering happens at the **retrieval layer**, not in the LLM prompt. Never send restricted chunks to an LLM and rely on instructions to suppress them.

---

## Architecture

```
User / Agent
    ↓
Identity Provider (SSO / LDAP)
    ↓
Entitlement Service
    (role, desk, geography, product class)
    ↓
Retrieval Service receives:
    - allowed sensitivity tiers
    - allowed domains
    - allowed geographies
    - allowed product classes
    ↓
Metadata Pre-filter applied BEFORE retrieval
    ↓
Filtered Document Set → LLM → Cited Response
```

---

## Entitlement Dimensions

A user's effective entitlement is the intersection of these dimensions:

| Dimension | Source | Example Values |
|---|---|---|
| Role | LDAP / HR system | `Structurer`, `Trader`, `RiskAnalyst`, `Compliance`, `Operations` |
| Desk | Trading system / HR | `EquityDerivatives`, `Rates`, `FXOptions`, `StructuredProducts` |
| Product class | Per-user product entitlement | `Autocallable`, `IRS`, `CLO` |
| Geography | HR + regulatory mapping | `IN`, `EU`, `US`, `APAC` |
| Sensitivity ceiling | Role + tier matrix | `Internal`, `Confidential`, `Restricted` |
| Wall-crossing flags | Compliance system | Per deal, time-bounded |

---

## Pre-filter Construction

When a user issues a query, the retrieval service constructs a filter set:

```python
filter = {
    "sensitivity_tier": {"$lte": user.sensitivity_ceiling},
    "domain": {"$in": user.allowed_domains},
    "sub_domain": {"$in": user.allowed_sub_domains},
    "product_class": {"$in": user.allowed_product_classes},
    "geography": {"$overlap": user.allowed_geographies},
    "effective_date": {"$lte": today()},
    "$or": [
        {"expiry_date": None},
        {"expiry_date": {"$gt": today()}}
    ],
    "approval_status": "Canonical"
}
```

Pre-filter is applied to the vector index search itself — restricted chunks never enter the candidate pool.

---

## Required Controls for Capital Markets

| Control | Mechanism |
|---|---|
| Desk-level entitlement | RBAC per trading desk, product class |
| Instrument-level restriction | Sensitivity tag + entitlement check |
| Client data isolation | Namespace separation in vector index |
| MNPI / Insider info isolation | Restricted namespace, wall-crossing log |
| Audit trail | Every retrieval event logged (user, query, chunks returned, timestamp) |
| Versioning | Immutable document versions; rollback to point-in-time |
| Data lineage | Source system → ingestion → chunk → response chain |

---

## Namespace Strategy

| Namespace | Contents | Cross-namespace queries |
|---|---|---|
| `public` | `Public` tier chunks | Allowed |
| `internal` | `Internal` tier chunks | Allowed within bank |
| `confidential-<desk>` | `Confidential` chunks scoped to a desk | Same-desk only |
| `client-<client_id>` | Client-specific data | Same client + entitled users only |
| `restricted-<deal_id>` | MNPI / deal data | Wall-crossed users only |
| `model-ip` | Restricted model documentation | Model risk + approved users |

A single retrieval request may span only namespaces the user is entitled to. The vector DB enforces this — entitlement is part of the index partitioning, not a post-filter.

---

## Failure Modes (Must Be Tested)

1. **Restricted chunk surfaced to unauthorized user** — automatic alert + access revoked pending review.
2. **Cross-desk leak via shared agent context** — agents must re-fetch entitlement per query, not cache across users.
3. **Stale entitlement after role change** — entitlement TTL <= 15 min, with push-revocation on role change.
4. **Bypass via prompt injection** — pre-filter at retrieval makes this structurally impossible. Verify with red-team test.

---

## Open Questions for Phase 1 Sign-off

- [ ] Confirm entitlement service source of truth (existing system vs. new build).
- [ ] Confirm entitlement TTL and push-revocation mechanism.
- [ ] Define namespace strategy with vector DB owners — many DBs limit total namespace count.
- [ ] Agree on wall-crossing UX (in-line consent vs. pre-flight Compliance approval).
