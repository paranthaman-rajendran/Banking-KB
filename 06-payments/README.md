# Payments Sub-Domain Knowledge

Knowledge base content for the `Payments` domain. Mirrors the [Structured Products pilot](../04-pilot-structured-products/) structure and follows the same governance, metadata, and approval rules.

> **Domain code**: `Payments`
> **Sub-domain codes**: `DomesticIN`, `CrossBorder`, `RealTimeRails`, `Cards`
> **Status**: knowledge scaffolding — not yet a funded pilot. Promote when ready.

---

## Navigation

| Folder / File | Purpose |
|---|---|
| [concepts.md](concepts.md) | Foundational concept explainers (primary vs secondary sanctions, CDD/EDD/SDD, nostro/vostro, RTGS vs DNS, finality, push vs pull, APP fraud, etc.) — start here |
| [taxonomy-detail.md](taxonomy-detail.md) | Deeper breakdown of Payments sub-domains, rails, and instruments |
| [rails/](rails/) | Per-rail knowledge — domestic India / USA / UK, cross-border, real-time |
| [standards/](standards/) | Message standards — ISO 20022, SWIFT MT/MX, ISO 8583 |
| [architecture/](architecture/) | Lifecycle, systems landscape, top global payment engines |
| [architecture/vendors/](architecture/vendors/) | Per-engine deep-dives — Finastra GPP, Oracle OBPM |
| [regulatory.md](regulatory.md) | High-level regulatory overview (entry point) |
| [regulatory/](regulatory/) | Per-jurisdiction deep-dives — USA, UK, Europe, Singapore, China, Japan + cross-border + engine compliance matrix |
| [source-inventory.md](source-inventory.md) | Source documents to ingest |
| [golden-questions.md](golden-questions.md) | Seed eval dataset |
| [glossary.md](glossary.md) | Payments terminology |

---

## Scope by Sub-Domain

| Sub-Domain | Rails / Instruments | Primary Geography |
|---|---|---|
| `DomesticIN` | NEFT, RTGS, IMPS, UPI, AePS, NACH, BBPS | IN |
| `DomesticUS` | ACH (standard + Same-Day), FedWire, FedNow, RTP, CHIPS, Check 21, Zelle | US |
| `DomesticUK` | FPS, CHAPS, Bacs (DC + DD), ICS, LINK, CoP, Open Banking PISP, VRP | UK |
| `CrossBorder` | SWIFT (MT/MX), SEPA, IAT (cross-border ACH), correspondent USD, RippleNet | GLOBAL |
| `RealTimeRails` | UPI (IN), FPS (UK), TIPS (EU), FedNow (US), Pix (BR), NPP (AU), PayNow (SG) | GLOBAL |
| `Cards` | Visa, Mastercard, RuPay, Amex; ISO 8583; tokenization | GLOBAL |

---

## Why Payments Differs from Capital Markets

| Dimension | Capital Markets | Payments |
|---|---|---|
| Document types | Term sheets, ISDA, prospectuses | Scheme rulebooks, message specs, settlement SOPs |
| Freshness | Mostly T+0 for new issuance, otherwise static | Scheme rule changes are continuous; sanctions lists are real-time |
| Regulatory load | MiFID II, Basel, EMIR | RBI Master Directions, PSD2/PSR, BIS CPMI, FATF |
| Sensitivity | Client + position data | Transaction-level PII + sanctions hits |
| Operational tempo | T+1 / T+2 settlement | Real-time (UPI ~6s P95), 24x7 windows |

These differences flow into chunking, freshness SLAs, and access control. Payments-specific deviations from the master governance are called out per doc.

---

## Phase-2 Style Pilot (when funded)

A future Payments pilot would target one of:

1. **Cross-border SWIFT MT→MX (ISO 20022) migration knowledge** — high regulatory urgency, dense spec.
2. **UPI dispute resolution copilot for Ops** — high transaction volume, well-bounded SOPs.
3. **Sanctions screening explainability** — risk-critical, structured data + policy retrieval.

Recommendation: **Option 2 (UPI Ops copilot)** — narrowest scope, clearest ROI, lowest sensitivity-tier exposure. See [pilot ideas](#pilot-candidates-when-funded) for details to flesh out when funded.

---

## Phase 1 (Knowledge Prep) Exit Checklist

- [ ] Taxonomy-detail reviewed by Payments product + Ops leads
- [ ] Per-rail knowledge docs spot-checked against current scheme rulebooks
- [ ] Source inventory mapped to authoritative systems
- [ ] Regulatory mapping reviewed by Compliance (RBI + PSD2 leads)
- [ ] Glossary cross-checked with internal payments product team
- [ ] Golden questions reviewed by Payments Operations

---

## Cross-References

- Domain taxonomy and codes: [../01-taxonomy/taxonomy.md](../01-taxonomy/taxonomy.md)
- Metadata schema (mandatory fields): [../01-taxonomy/metadata-schema.md](../01-taxonomy/metadata-schema.md)
- Data classification tiers: [../03-governance/data-classification.md](../03-governance/data-classification.md)
- Source curation policy: [../02-source-curation/source-inventory.md](../02-source-curation/source-inventory.md)
