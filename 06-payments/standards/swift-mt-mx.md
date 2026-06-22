# SWIFT MT and MX

The legacy (MT) and current (MX / ISO 20022) message standards on the SWIFT network. Both are in scope for the KB during the co-existence period; MT is sunsetting for cross-border payments in **November 2025**.

> Sub-domain: `Payments / Standards`

---

## MT — Legacy

SWIFT MT messages are flat-text, character-delimited, with rigid block + field structure.

### Block Structure

```
{1: Basic Header}
{2: Application Header}
{3: User Header}     (optional)
{4: Text Block — body fields}
{5: Trailer}
```

### Body Field Format

Each field is `:NN[L]: content` where NN is a 2-digit number (sometimes with a letter qualifier).

Example MT103 body:
```
:20:REF12345
:23B:CRED
:32A:250612USD12345,67
:50K:/123456789
ACME CORP
1 MAIN ST
:59:/987654321
BENEFICIARY LTD
:71A:OUR
```

### Common MT Messages

| MT | Purpose |
|---|---|
| MT101 | Request for Transfer (corp → bank, multi-format) |
| MT103 | Single Customer Credit Transfer |
| MT103 STP | MT103 with STP constraints (no free-form, fully structured beneficiary) |
| MT202 | General Financial Institution Transfer |
| MT202COV | Cover payment (sister message to MT103) |
| MT199 / MT299 | Free-format informational |
| MT900 | Confirmation of Debit |
| MT910 | Confirmation of Credit |
| MT940 | Customer Statement (EOD) |
| MT942 | Interim Transaction Report |
| MT950 | Statement Message (legacy variant) |
| MT196 / MT296 | Answer to a previous message |

### Key MT Field IDs

| Field | Purpose |
|---|---|
| 20 | Sender's Reference |
| 21 | Related Reference |
| 23B | Bank Operation Code (CRED, SPRI, SSTD, CRTS) |
| 32A | Value Date + Currency + Amount |
| 33B | Original Currency / Amount |
| 50A/F/K | Ordering Customer |
| 52A/D | Ordering Institution |
| 53A/B/D | Sender's Correspondent |
| 54A/B/D | Receiver's Correspondent |
| 56A/C/D | Intermediary Institution |
| 57A/C/D | Account With Institution |
| 59 / 59A / 59F | Beneficiary Customer |
| 70 | Remittance Information (free text) |
| 71A | Details of Charges (OUR / SHA / BEN) |
| 72 | Sender to Receiver Information |
| 121 | UETR (gpi) |

---

## MX — ISO 20022

See [iso-20022.md](iso-20022.md) for the full standard. MX messages on the SWIFT network are CBPR+-profile-compliant.

### MT → MX Mapping Highlights

| MT 103 | MX (pacs.008) |
|---|---|
| 20 (Sender Ref) | `<TxId>` + `<InstrId>` |
| 32A (Value Date / Currency / Amount) | `<IntrBkSttlmDt>` + `<IntrBkSttlmAmt Ccy="…">` |
| 50K (Ordering Customer) | `<Dbtr>` block — structured `Nm`, `PstlAdr`, `Id` |
| 59 (Beneficiary) | `<Cdtr>` block — structured |
| 71A (Charges) | `<ChrgBr>` (OUR=DEBT, SHA=SHAR, BEN=CRED) |
| 70 (Remittance) | `<RmtInf>` — structured fields preferred over unstructured |
| 121 (UETR) | `<UETR>` |

Mapping is **one-way lossless from MT to MX** for STP cases. **MX → MT is lossy** — structured fields collapse to free text.

---

## Validation

### MT
- Field format validation at SWIFT FIN gateway.
- Message authorization controlled by RMA (Relationship Management Application) — bilateral.
- Bank-internal rules layered on top.

### MX
- Schema validation at SWIFT FINplus.
- CBPR+ usage guideline rules (some advisory, some mandatory).
- Bank-internal rules layered on top.

---

## Operational Considerations

| Concern | Status |
|---|---|
| MT sunset for cross-border | November 2025 |
| MT support continuing for | Domestic systems on their own schedules (e.g., RTGS local schemes) |
| Translation services | SWIFT Transaction Manager (MX-only internally; legacy banks can submit MT, which is auto-translated) |
| Audit trail | UETR + tracker (gpi) for both |
| Speed | gpi banks credit beneficiary within 30 min for >50% of payments |

---

## Sources to Ingest

- SWIFT Standards MT Release Notes (annual, November)
- SWIFT Standards MX Release Notes (CBPR+ annual)
- SWIFT Transaction Manager guides
- gpi Customer Credit Transfer rulebook
- Bank-internal: SWIFT field validation rules, message translation library, RMA matrix

---

## Open Questions

- [ ] Confirm whether the bank operates a single SWIFT BIC or multiple (affects metadata routing).
- [ ] Confirm internal cutover date for MT → MX (may precede or follow Nov 2025 industry deadline).
- [ ] Current gpi membership and tracker subscription status.
