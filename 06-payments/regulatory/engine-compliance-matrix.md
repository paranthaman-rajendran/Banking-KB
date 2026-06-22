# Payment Engine — Regulatory Compliance Matrix

Cross-jurisdiction view: for each regulatory requirement, **which engine feature implements it** and which jurisdiction it applies to. Use this as a coverage map when assessing a hub (e.g., Finastra GPP, Oracle OBPM, Volante, ACI UP, Form3) against the bank's geographic footprint.

> Per-jurisdiction detail: [usa.md](usa.md), [uk.md](uk.md), [europe.md](europe.md), [singapore.md](singapore.md), [china.md](china.md), [japan.md](japan.md), [cross-border-international.md](cross-border-international.md).

---

## Requirement → Engine Feature Map

| Requirement | Engine Feature | Applies in |
|---|---|---|
| **Real-time sanctions screening (multi-list)** | Pre-payment screening hook; list refresh; investigator queue; per-list audit | US (OFAC), EU (EU Consolidated), UK (OFSI), JP (FEFTA), CN (limited national + indirect OFAC), SG (MAS), Global (UN) |
| **Travel Rule (originator + beneficiary)** | Field validation + block-on-missing; propagation through hops | US (FinCEN — USD 3k), EU (Funds Transfer Reg), UK (PSRs 2017 derived), JP (FEFTA), SG (PSN01), CN (AML Law), Global (FATF R.16) |
| **AML transaction monitoring + STR/SAR** | Pattern detection layer; STR / SAR pipeline to FIU | US (BSA→FinCEN), EU (AML Reg→AMLA), UK (MLRs→NCA), JP (APTCP→JFIU), CN (AML Law→PBoC AMLB), SG (PSN01→STRO) |
| **CDD / EDD on customer + counterparty** | KYC integration + ongoing review trigger | All jurisdictions |
| **Strong Customer Authentication (SCA)** | Step-up authentication; exemption logic | EU (PSD2 + EBA RTS), UK (PSRs 2017), SG (in scheme-specific contexts), JP (FSA guidance) |
| **Open Banking APIs (AISP / PISP)** | PSD2-compliant API estate | EU (PSD2), UK (PSRs 2017 + CMA Order), US (CFPB Section 1033 roadmap), SG (SGFinDex / MAS), JP (developing) |
| **Confirmation / Verification of Payee** | Pre-payment name-check at initiation | UK (SD20), EU (IPR — VoP), emerging cross-border |
| **APP fraud reimbursement workflow** | Claim handling; sender + receiver split logic; evidence packaging | UK (SD18 — 50/50), US (CFPB-led pressure; voluntary at scale), others emerging |
| **Cross-border instant linkages** | Corridor adapters; multi-currency liquidity | SG ↔ IN / MY / TH / ID; future global (Project Nexus) |
| **ISO 20022 native** | CBPR+ / HVPS+ message stack; structured fields end-to-end | Cross-border SWIFT (Nov 2025); US (FedNow / RTP / CHIPS / FedWire); UK (CHAPS); EU (T2 / TIPS / SCT Inst / CT); CN (CIPS); SG (FAST in migration); JP (Zengin + BOJ-NET in migration) |
| **Multi-regime FX + currency controls** | Currency-routing tables; restricted-currency block / hold | CN (CNY onshore + offshore split), JP (FEFTA), IN (LRS / FEMA), KR / RU / IR (per programmes) |
| **Cross-border purpose / BoP code capture** | Per-payment purpose categorisation + reporting | CN (SAFE BoP), JP (FEFTA), IN (FEMA), others |
| **Data localisation + cross-border data export controls** | Geo-aware data storage + access | CN (CSL + DSL + PIPL), RU (data localisation), IN (RBI Master Direction), local privacy regimes |
| **Personal data protection (GDPR-class)** | Consent + DSR + breach notification pipeline | EU (GDPR), UK (UK GDPR + DPA), SG (PDPA), JP (APPI), CN (PIPL), US (state-level — CCPA/CPRA) |
| **Operational resilience + ICT incident reporting** | Impact-tolerance metrics; incident reporting pipeline | EU (DORA), UK (FCA/PRA op-res), US (FFIEC + OCC SR letters), SG (MAS TRM + BCM), JP (FSA op-res evolving) |
| **Direct Debit Guarantee** | Immediate-refund logic + recovery | UK (Bacs DD scheme) |
| **Pre-authorised mandate handling** | Mandate store + revocation | Universal (US Reg E pre-authorised EFT, UK Bacs DD, EU SDD, JP / SG schemes) |
| **Interchange caps** | Card-side fee logic | UK (IFR onshored), EU (IFR) |
| **Debit network routing (Reg II)** | Dual-unaffiliated-network routing | US |
| **Funds availability** | Posting + availability hold logic | US (Reg CC), other domestic schemes |
| **License-aware activity routing** | Activity classification per license tier | SG (PS Act tiers), JP (Funds Settlement Act tiers), US (state MTL), EU (PI / EMI / Credit Inst) |
| **Customer fund safeguarding (non-bank PSP)** | Segregated accounts + reconciliation | EU EMD2, UK EMRs, SG PS Act, JP Funds Settlement Act |
| **Sanctions tonality alongside USD chain** | Multi-regime screening when USD intermediary involved | Anywhere USD touched — OFAC secondary effect |
| **Settlement finality + recall handling** | Finality semantics per rail | All RTGS rails (FedWire, CHAPS, RTGS-IN, BOJ-NET, MEPS+, HVPS); recall workflow per scheme |
| **Audit trail + immutable retention** | Append-only event log; 5–10 year retention | All — universal |
| **gpi tracker integration** | UETR-keyed status updates | Cross-border SWIFT |
| **Pre-validation API support** | Beneficiary verification before send | SWIFT PPv, cross-border |
| **CBDC interface readiness** | Wholesale / retail CBDC adapter | CN (e-CNY), SG (Project Ubin / Orchid), EU (Digital Euro on roadmap), JP (BoJ pilot), US (limited research) |

---

## Per-Engine Feature Coverage Lens

A purchasing decision boils down to: does the chosen hub support **all the requirements in our footprint?** This grid is the checklist.

For an OBPM-vs-GPP decision in a bank operating US + UK + EU + SG:

| Requirement | OBPM | GPP | Notes |
|---|---|---|---|
| ISO 20022 native | Yes | Yes | Both |
| OFAC + EU + UK + MAS screening hooks | Yes (Oracle FCCM native) | Yes (Fircosoft preferred) | Both pluggable |
| FedNow + RTP adapters | Yes (newer) | Yes (mature) | Verify version |
| CHAPS ISO 20022 | Yes | Yes | Both |
| CHAPS + Bacs + FPS with CoP | Yes | Yes | Both |
| SCT Inst with VoP | Yes | Yes | Both rolling out for IPR |
| MAS FAST + PayNow | Yes (APAC strong) | Yes | Both |
| SG PayNow corridor adapters | Partial | Partial | Per release |
| CN CIPS adapter | Yes (APAC strong) | Yes | Per release |
| Multi-tenancy at group level | Strong | Strong (via PaaS) | Both |
| Travel Rule field enforcement | Yes | Yes | Both |
| gpi tracker integration | Yes | Yes | Both |

Both products cover the universal set; the picking decision is usually adjacent — CBS alignment, compliance vendor preference, cloud posture, implementation track record.

---

## Per-Jurisdiction Quick Reference

| Jurisdiction | Primary Reg | Sanctions Source | Instant Rail | Data Privacy | Key Engine Watchpoint |
|---|---|---|---|---|---|
| **US** | Reg E/J/CC/II + BSA + NACHA | OFAC | FedNow + RTP | GLBA + NYDFS + state | State MTL footprint; OFAC 50% Rule + secondary sanctions |
| **UK** | PSRs 2017 + PSR SDs | OFSI | FPS (NPA roadmap) | UK GDPR | SD18 APP fraud joint liability; SD20 CoP at initiation |
| **EU** | PSD2 → PSD3/PSR + IPR + AML Reg | EU Consolidated | SCT Inst + TIPS | GDPR | IPR mandate + VoP; DORA op-res |
| **Singapore** | PS Act 2019 + MAS Notices + TRM | MAS | FAST + PayNow | PDPA | MAS TRM rigour; cross-border corridors via PayNow |
| **China** | Non-Bank Payment Inst Regs + AML Law + CSL/DSL/PIPL | National + indirect OFAC | IBPS + Alipay/WeChat | PIPL + DSL | Onshore CNY vs offshore CNH; data localisation; SAFE BoP |
| **Japan** | Funds Settlement Act + APTCP + FEFTA | METI/MOF FEFTA-implemented | Zengin (24x7) + Zengin More | APPI | FEFTA cross-border reporting; ISO 20022 migration on programme |
| **Cross-border** | FATF + BIS + ISO + Wolfsberg | Multiple (US OFAC dominant via USD) | UPI ↔ PayNow + emerging linkages | Per leg | Travel Rule completeness; gpi tracker; G20 2027 targets |

---

## Practical Engineering Checklist for a Global Hub

Build a feature matrix per requirement × jurisdiction. For each cell, mark one of:

| Marker | Meaning |
|---|---|
| ✅ Built-in | Engine ships the feature; configuration only |
| 🔧 Configurable | Available through bank-side configuration / customisation |
| 🧩 Integration | Requires third-party integration (vendor for sanctions / fraud / VoP) |
| ❌ Missing | Not supported; programme work needed |

Aim for ✅ or 🔧 on every cell of the bank's footprint. 🧩 is acceptable when the integration partner is robust + the bank has the integration capability. ❌ is a programme risk.

---

## Sources

Per jurisdiction file in this folder; cross-border / international standards in [cross-border-international.md](cross-border-international.md).

---

## Open Questions

- [ ] Confirm engine selection criteria weighting (geographic breadth vs. depth in core markets).
- [ ] Confirm bank's footprint + product set for each cell in the matrix.
- [ ] Confirm acceptable level of customisation per requirement (🔧 vs. ✅ tolerance).
- [ ] Confirm vendor management process for 🧩 integrations.
