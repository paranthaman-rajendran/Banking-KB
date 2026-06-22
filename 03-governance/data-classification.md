# Data Classification

Four-tier sensitivity model. Drives the `sensitivity_tier` metadata field and all access-control decisions downstream.

---

## Tiers

| Tier | Description | Examples | Default for |
|---|---|---|---|
| `Public` | Externally publishable, no restriction | External marketing materials, public prospectuses, regulatory circulars, published indices | Marketing, regulator content |
| `Internal` | Staff-only, no external exposure | Internal policies, standard SOPs, internal research summaries, taxonomy docs | Internal Confluence by default |
| `Confidential` | Restricted to relevant function or desk | Client data, trade data, risk positions, term sheets, ISDA agreements | Trade and client data |
| `Restricted` | Need-to-know, wall-crossing controls | M&A deal data, insider information (MNPI), proprietary model IP, deal pipeline | Deal teams, model owners |

---

## Tier Assignment Rules

1. **Default deny upward**: if uncertain, choose the more restrictive tier. Demoting requires Compliance review.
2. **Client data is at least `Confidential`** — never `Internal` or `Public`.
3. **MNPI is always `Restricted`** — no exceptions. Storage and retrieval go through the wall-crossing log.
4. **Model documentation is `Restricted` if it includes calibration parameters or proprietary methodology**; `Internal` if only conceptual.
5. **Externally-published material is `Public`** only after Legal/Compliance sign-off — drafts stay `Internal`.

---

## Handling Per Tier

| Tier | Storage Namespace | Encryption | Cross-Border | Retention Default |
|---|---|---|---|---|
| `Public` | Shared namespace | At-rest standard | Unrestricted | Indefinite |
| `Internal` | Shared namespace | At-rest standard | Per geography metadata | 7 years |
| `Confidential` | Function-scoped namespace | At-rest standard + per-field keys | Per geography + entitlement | 7 years (regulator min) |
| `Restricted` | Dedicated isolated namespace | At-rest + per-record keys + access broker | Same geography only | Per Compliance directive |

---

## Wall Crossing (Restricted Tier)

- Every retrieval of a `Restricted` chunk is logged with: user, query, chunk IDs returned, justification code, business purpose.
- Wall-crossing requires pre-approval from Compliance for the user-deal pair.
- Restricted chunks are NEVER returned in mixed-result sets — a query that touches Restricted data receives only Restricted results in that response, and the user is flagged.

---

## LLM Exposure Rules

- `Public` and `Internal` chunks can be sent to any approved LLM.
- `Confidential` chunks may only be sent to LLMs deployed in approved environments (no third-party shared inference for raw text).
- `Restricted` chunks NEVER leave the bank's controlled environment. Inference uses self-hosted or VPC-isolated models only.

The LLM gateway enforces these rules — not the retrieval layer alone.

---

## Open Questions for Phase 1 Sign-off

- [ ] Confirm retention periods per tier against Legal's data retention policy.
- [ ] Confirm which LLM endpoints qualify as "approved environments" for `Confidential`.
- [ ] Define the wall-crossing pre-approval workflow and Compliance team integration.
