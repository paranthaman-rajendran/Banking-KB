# Canonical Approval Lifecycle

Only `Canonical` documents enter the production retrieval index. This is non-negotiable.

```
Draft → Under Review → Compliance Reviewed → Approved → Canonical
                                                         │
                                                         ▼
                                              Superseded / Archived
```

---

## States

| State | Description | Indexed in Prod? | Indexed in Dev/Staging? |
|---|---|---|---|
| `Draft` | Author working copy | No | No |
| `Under Review` | Peer / desk review in progress | No | Optional |
| `Compliance Reviewed` | Compliance sign-off received | No | Yes |
| `Approved` | Final approver signed off | No | Yes |
| `Canonical` | Active in production | **Yes** | Yes |
| `Superseded` | Replaced by newer Canonical version | No (retrievable point-in-time) | Yes |
| `Archived` | End-of-life, kept for audit | No | No |

---

## Transitions & Required Approvers

| From → To | Required Approver | Audit Event |
|---|---|---|
| `Draft → Under Review` | Author submit | Submission logged |
| `Under Review → Compliance Reviewed` | Compliance reviewer | Comp reviewer ID + timestamp |
| `Compliance Reviewed → Approved` | Final approver (owner team head) | Approver ID + timestamp |
| `Approved → Canonical` | System (automatic when ingestion pipeline succeeds) | Indexed timestamp + chunk count |
| `Canonical → Superseded` | System (automatic when newer Canonical version supersedes) | Predecessor/successor link |
| `* → Archived` | Owner team head + Compliance | Reason code required |

Any transition outside the table requires a justification record and Compliance review.

---

## Gating Rules

1. **A Draft can never be retrieved by an LLM.** No exceptions, including for the author.
2. **Compliance review is mandatory** for any document with `regulatory_tag` set or `sensitivity_tier >= Confidential`.
3. **Two-person rule**: `Approved → Canonical` requires the approver to be a different person than the author.
4. **Re-approval on material change**: any change to a `Canonical` doc that touches `effective_date`, `expiry_date`, `sensitivity_tier`, `regulatory_tag`, or substantive content (>5% diff) sends it back to `Under Review`.
5. **Cosmetic-only changes** (formatting, typos) can be fast-tracked by the owner team head with single approval, but must still log the diff.

---

## Point-in-time Retrieval

For regulatory investigations and audits:

- `Superseded` documents stay in cold storage with full metadata.
- A query can specify `as_of: 2025-03-01` to retrieve only chunks that were `Canonical` at that date.
- Point-in-time retrieval is logged separately and requires the requester's role to include `audit_query`.

---

## Open Questions for Phase 1 Sign-off

- [ ] Who is the "final approver" per source category? Need named role mapping.
- [ ] What counts as a "material change" for re-approval — 5% diff threshold or content-based rule?
- [ ] Cold storage retention period for `Archived` documents (regulatory minimum vs. business need).
