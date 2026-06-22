# Payments Glossary

Working vocabulary for the Payments domain. Used by the structurer / curator / evaluator to disambiguate terms. Where a term has different meanings across rails or geographies, both are listed.

> One-liners only. For paragraph-style explainers and concept framing (primary vs. secondary sanctions, RTGS vs. DNS, finality, CDD/EDD/SDD, nostro/vostro/loro, push vs. pull, APP fraud, etc.) see [concepts.md](concepts.md).
>
> Prepend the disambiguated term as context when chunking — many payments terms are heavily overloaded.

---

## A

- **ACH** — Automated Clearing House. In the US, NACHA-operated batched rail. Elsewhere can refer to similar batch systems.
- **ADDACS** — Automated Direct Debit Amendment and Cancellation Service (UK Bacs). Notifies originators of mandate changes.
- **APP fraud reimbursement** — UK PSR mandate (Oct 2024) requiring 50/50 PSP cost split for Authorised Push Payment fraud over FPS/CHAPS.
- **ARUDD** — Automated Return of Unpaid Direct Debits (UK Bacs).
- **ARUCS** — Automated Return of Unapplied Credits Service (UK Bacs).
- **AUDDIS** — Automated Direct Debit Instruction Service (UK Bacs) — paperless mandate setup.
- **AePS** — Aadhaar-enabled Payment System. Indian rail for Aadhaar-biometric cash withdrawal at BC outlets.
- **AISP** — Account Information Service Provider (PSD2). Read-only access to account info via Open Banking.
- **AML** — Anti-Money Laundering.
- **APP fraud** — Authorised Push Payment fraud. The customer is deceived into authorising the payment themselves (vs. unauthorised).
- **ASPSP** — Account Servicing PSP (PSD2 terminology for the bank holding the account).
- **AutoPay** — UPI's e-mandate flow for recurring debits.

## B

- **Bacs** — UK batched payment scheme (Direct Credit + Direct Debit), operated by Pay.UK.
- **BBPS** — Bharat Bill Payment System (India).
- **BIC** — Business Identifier Code (ISO 9362). 8 or 11 char SWIFT address.
- **BSA** — Bank Secrecy Act (US). Foundation of US AML.

## C

- **camt** — ISO 20022 Cash Management messages (camt.052, camt.053, camt.054).
- **CBPR+** — Cross-Border Payments and Reporting Plus. SWIFT's ISO 20022 profile for cross-border.
- **CHAPS** — UK high-value RTGS, operated by Bank of England. ISO 20022 since 2023.
- **Check 21** — US Act (2003) enabling electronic image exchange of cheques; IRD = Image Replacement Document.
- **CHIPS** — Clearing House Interbank Payments System (US, TCH-operated). ISO 20022 since 2024.
- **Consumer Duty** — FCA outcomes-based supervisory framework (July 2023). Applies to payments customer journeys.
- **CoP** — Confirmation of Payee (UK name-check). Mandatory for FPS, CHAPS, Bacs Direct Credit at most participants.
- **CSM** — Clearing & Settlement Mechanism (SEPA terminology).
- **CTR** — Currency Transaction Report (US BSA, threshold-based).

## D

- **DE** — Data Element (ISO 8583 field).
- **DNS** — Deferred Net Settlement. Settlement model where positions are netted and settled later (e.g., NEFT).
- **DMS** — Dispute Management System (NPCI's UPI dispute platform).

## E

- **EMI** — Electronic Money Institution (EU regulatory category).
- **EMV** — Europay-Mastercard-Visa chip card standard.
- **EPC** — European Payments Council (operator of SEPA scheme rulebooks).

## F

- **FATF** — Financial Action Task Force. Sets AML/CFT standards.
- **FedNow** — US Federal Reserve real-time instant payment service (live July 2023). ISO 20022 native. USD 500k default cap.
- **FedWire** — US Federal Reserve RTGS. Final, irrevocable. ISO 20022 migration ongoing.
- **FIN** — SWIFT's legacy MT-message store-and-forward network.
- **FINplus** — SWIFT's ISO 20022 message store-and-forward (CBPR+ MX).
- **FOS** — Financial Ombudsman Service (UK consumer dispute resolution).
- **FPS** — Faster Payments Service (UK). Pay.UK-operated, 24x7, scheme cap GBP 1M.
- **FSCS** — Financial Services Compensation Scheme (UK deposit / investor protection).

## G

- **gpi** — Global Payments Innovation. SWIFT's tracker-enhanced cross-border standard.
- **GDPR** — General Data Protection Regulation (EU).

## H

- **HVPS+** — High-Value Payment Systems profile of ISO 20022.

## I

- **IAT** — International ACH Transaction. SEC code for cross-border ACH carrying Travel Rule fields.
- **IBAN** — International Bank Account Number (ISO 13616).
- **ICS** — Image Clearing System (UK cheque image exchange operated by Pay.UK).
- **IFR** — Interchange Fee Regulation (EU origin; UK has onshored version).
- **IFSC** — Indian Financial System Code (used in NEFT/RTGS/IMPS).
- **IMAD/OMAD** — Input/Output Message Accountability Data — FedWire transaction identifiers.
- **IMPS** — Immediate Payment Service (India, NPCI).
- **IPR** — Instant Payments Regulation (EU; Nov 2024 in force).
- **IRD** — Image Replacement Document (US Check 21).
- **ISO 20022** — Modern payments messaging standard.
- **ISO 8583** — Card industry messaging standard.

## K

- **KID** — Key Information Document (PRIIPs; required for some structured products to retail).
- **KYC** — Know Your Customer.

## M

- **Mandate** — Customer authorization for recurring debits.
- **MMID** — Mobile Money Identifier (IMPS).
- **MNPI** — Material Non-Public Information. *(Same as Capital Markets — wall-crossing applies.)*
- **MT** — SWIFT Message Type (legacy text format).
- **MTI** — Message Type Indicator (ISO 8583, 4 digits).
- **MX** — ISO 20022 message in SWIFT context.

## N

- **NACH** — National Automated Clearing House (India).
- **NACHA** — National Automated Clearing House Association (US ACH operator org).
- **NEFT** — National Electronic Funds Transfer (India, RBI).
- **NPA** — New Payments Architecture (UK FPS migration target).
- **NPCI** — National Payments Corporation of India.
- **NPP** — New Payments Platform (Australia's real-time rail).

## O

- **OCT** — One-leg Cross-border (proposed EU instant scheme).
- **OFAC** — Office of Foreign Assets Control (US Treasury sanctions).
- **ODR** — Online Dispute Resolution.

## P

- **pacs** — ISO 20022 Payments Clearing & Settlement messages (pacs.008, pacs.009).
- **pain** — ISO 20022 Payments Initiation messages (pain.001).
- **PAN** — Primary Account Number (card industry).
- **PA-PG** — Payment Aggregator / Payment Gateway (RBI category).
- **PCI DSS** — Payment Card Industry Data Security Standard.
- **PEP** — Politically Exposed Person.
- **PFMI** — Principles for Financial Market Infrastructures (BIS CPMI / IOSCO).
- **Pix** — Brazil's real-time instant rail (BCB).
- **PIN** — Personal Identification Number; or, separately, **PIN translation** in payment HSMs (Hardware Security Modules).
- **PISP** — Payment Initiation Service Provider (PSD2).
- **PPI** — Prepaid Payment Instrument (RBI category — wallets).
- **PSD2 / PSD3** — Payment Services Directive (EU); PSR is the new Payment Services Regulation in PSD3 package.
- **PSP** — Payment Service Provider. In UPI context, the bank or app provider serving the customer.

## R

- **RBI** — Reserve Bank of India.
- **RDFI** — Receiving Depository Financial Institution (US ACH).
- **Reg CC** — US Federal Reserve regulation on funds availability + Check 21.
- **Reg E** — US Federal Reserve regulation on consumer electronic fund transfer protections.
- **Reg II** — US Federal Reserve regulation on debit interchange + routing (Durbin).
- **Reg J** — US Federal Reserve regulation on FedWire / FedACH.
- **RMA** — Relationship Management Application (SWIFT bilateral authorization).
- **RTGS** — Real-Time Gross Settlement. Generic; also the specific Indian RTGS rail.
- **RTP** — Real-Time Payments. Generic; also the US TCH-operated RTP rail (USD 10M cap, live 2017).
- **RTGS Renewal Programme** — Bank of England's renewal of the UK RTGS infrastructure underpinning CHAPS.

## S

- **Same-Day ACH** — US ACH variant with three intraday settlement windows; per-txn cap USD 1M.
- **SAR** — Suspicious Activity Report (US BSA / UK MLRs equivalent).
- **SCA** — Strong Customer Authentication (PSD2 / PSRs 2017).
- **SCT** — SEPA Credit Transfer.
- **SCT Inst** — SEPA Credit Transfer Instant.
- **SD18** — UK PSR specific direction on APP Fraud Reimbursement.
- **SD20** — UK PSR specific direction on Confirmation of Payee.
- **SDD** — SEPA Direct Debit.
- **SEC code** — Standard Entry Class code (US ACH); identifies authorisation channel (PPD, CCD, WEB, TEL, IAT, etc.).
- **SEPA** — Single Euro Payments Area.
- **SoT** — Source of Truth (used in reconciliation).
- **STAN** — System Trace Audit Number (ISO 8583 DE 11).
- **STP** — Straight-Through Processing.
- **STR** — Suspicious Transaction Report (FIU-IND, India).
- **SWIFT** — Society for Worldwide Interbank Financial Telecommunication.

## T

- **TCH** — The Clearing House (US).
- **TIPS** — TARGET Instant Payment Settlement (EU instant rail run by Eurosystem).
- **TLV** — Tag-Length-Value (EMV encoding inside ISO 8583 DE 55).
- **TPAP** — Third-Party App Provider (UPI). E.g., GPay, PhonePe, Paytm.
- **TR** — Trade Repository.
- **Travel Rule** — FATF Rec 16. Mandates originator + beneficiary info on transfers above threshold.
- **TR1 / RT1** — EBA CLEARING's CSMs (TR1 = SCT, RT1 = SCT Inst).

## U

- **UETR** — Unique End-to-end Transaction Reference (gpi / ISO 20022).
- **UPI** — Unified Payments Interface (India).

## T

- **TPS** — Third-Party Sender (US ACH terminology for non-bank entities originating ACH on behalf of others).

## V

- **VPA** — Virtual Payment Address. UPI's `handle@psp` identifier.
- **VRP** — Variable Recurring Payments (UK Open Banking). Sweeping (CMA9-mandated, free) and Commercial variants.

## W

- **Wall crossing** — Compliance-controlled process to allow access to MNPI / Restricted info for specific people for specific deals.

## Z

- **Zelle** — US P2P payment service operated by Early Warning Services (EWS). Directory + risk overlay; settles over RTP / FedNow / ACH depending on FI.

---

## Open Questions

- [ ] Many terms above are bank-internal-overloaded — confirm internal usage with Payments product before promoting any of these to canonical.
- [ ] Some entries lean to India / EU / US bias — flag gaps for other geographies (APAC: NPP, PayNow, PromptPay; LATAM: Pix, SPEI; MEA).
- [ ] Confirm spelling / capitalization conventions match internal style guide.
