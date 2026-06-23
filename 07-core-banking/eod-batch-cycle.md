# EOD / BOD Batch Cycle

Deep-dive on the End-of-Day (EOD) and Beginning-of-Day (BOD) batch cycle in a Core Banking System (CBS). Expands the short definition in [concepts.md](concepts.md#daily-cycle--bod-eod-and-the-days-posting-window).

> Domain: `CoreBanking` / `Platform`
> Applies across `Retail` and `WholesaleCorporate` (job content differs, the cycle mechanics don't).

---

## Where EOD Sits in the Day

```
BOD → Online Day → Cut-off (Daily Cut) → EOD → BOD (next day)
```

EOD is the batch window between the daily cut-off and the next BOD. On a 24x7 CBS this is a logical job sequence rather than a physical downtime window; on a legacy batch-bound CBS it is a hard blackout (see [Batch-Bound vs 24x7 Impact](#batch-bound-vs-24x7-impact) below).

---

## EOD Job Sequence

Jobs typically run in this dependency order — each stage gates the next.

| # | Stage | Activity | Typical Owner |
|---|---|---|---|
| 1 | Cut-off enforcement | Close the books for value-date T; queue/reject late transactions to T+1 | CBS platform |
| 2 | Transaction validation | Confirm all same-day postings are complete; no orphaned/suspended entries | CBS platform / Ops |
| 3 | Interest accrual | Accrue daily interest on loans and deposits (CASA, term deposits, term loans) | CBS platform |
| 4 | Interest capitalization | Post due interest credits/debits (savings credit, loan EMI interest) | CBS platform |
| 5 | Average balance computation | Compute daily average balances for Account Analysis (AA) and Earnings Credit Rate (ECR) on corporate accounts | CBS platform |
| 6 | Charges & fees | Apply service charges, minimum-balance penalties, NACH/ECS return charges | CBS platform |
| 7 | Standing instructions | Execute due recurring transfers, loan EMI debits, scheduled bill payments | CBS platform |
| 8 | Sweeps & pooling | Run zero-balance sweeps to concentration accounts, notional pooling calculations | Treasury Services module |
| 9 | Classification batches | NPA ageing/classification, dormancy classification, limit/exposure recalculation | Risk / CBS platform |
| 10 | Sub-ledger reconciliation | Reconcile deposits/loans/cards sub-ledgers against the General Ledger; flag breaks | GL / Finance |
| 11 | Statement generation | Generate account statements, e-statements, passbook updates, FD maturity notices | CBS platform |
| 12 | Batch-mode settlement | Net/settle deferred-net-settlement rails (e.g., NEFT-style, ACH) not handled real-time | Payment Hub (see [Payments](../06-payments/)) |
| 13 | Regulatory & MIS extracts | Generate reserve/liquidity reports, AML/transaction-monitoring extracts, management MIS | Compliance / Finance |
| 14 | Archive & backup | Archive audit trails/logs; snapshot/backup the day's books | Ops / Infra |
| 15 | Calendar roll | Advance the system date; hand off to BOD | CBS platform |

BOD (next day) then runs: calendar roll confirmation, scheduled standing-instruction setup for the new day, overnight interest accrual posting, forward-dated payment release, FX rate refresh.

---

## Retail vs. Wholesale/Corporate EOD Differences

| Aspect | Retail | Wholesale / Corporate |
|---|---|---|
| Dominant batch jobs | Interest capitalization, dormancy classification, statement generation | Sweeps/pooling, ECR/AA computation, large-value settlement |
| Volume profile | Very high transaction count, low value | Lower count, high value — small errors are high-impact |
| Sweep complexity | Minimal | Multi-tier sweep hierarchies, multi-currency notional pooling |
| Reporting | Consumer statements | Account Analysis statements, ECR invoices |
| Failure tolerance | Can often resolve T+1 | Same-day resolution frequently required (cut-off-sensitive corporate flows) |

---

## Batch-Bound vs 24x7 Impact

Legacy CBS (older Finacle / Flexcube / T24 variants) cannot post during EOD — there is a **blackout window** (30–120 minutes) where retail rails degrade or queue. Modern CBS (Vault, 10x, Mambu, recent Finacle releases) run jobs as a **continuous logical sequence with no posting blackout**, which is what makes 24x7 real-time rails (UPI, FedNow, FPS, SCT Inst) viable. See [core-banking-systems.md — 24x7 Posting](core-banking-systems.md#24x7-posting) for the vendor-by-vendor posture.

---

## EOD-Specific Failure Modes

| Failure | Cause | Mitigation |
|---|---|---|
| EOD overrun into next day's online window | Volume growth outpacing legacy batch design | 24x7 architecture migration; job parallelization |
| Sweep failure leaves concentration account short | Upstream account balance not final at sweep job time | Sequence sweeps after all debit-posting jobs complete |
| Interest miscalculation | Day-count convention or rate-table error | Automated interest-accrual reconciliation vs. expected |
| GL break discovered only at month-end | Nightly recon insufficient frequency | Move toward real-time or intra-day recon |
| Statement generation delay | Upstream job chain delay cascades | Job-dependency monitoring with SLA alerting |
| Batch settlement file rejected by payment hub | Format/cut-off mismatch between CBS and hub | Pre-validate format; align cut-off calendars |
| Dormancy/NPA misclassification | Stale parameter table (days-past-due thresholds) | Workflow-managed parameter changes, not manual edits |

---

## Metadata Tagging (per [metadata-schema.md](../01-taxonomy/metadata-schema.md))

```yaml
domain: CoreBanking
sub_domain: Platform
product_class: EODBatchCycle
sensitivity_tier: Internal
source_system: <CBS vendor docs / bank Ops runbook>
owner_team: Core Banking Operations
geography: [GLOBAL]
language: en
approval_status: Canonical
```

---

## Sources to Ingest

- Bank-internal EOD/BOD job-scheduler runbooks (Control-M, Autosys, Tivoli Workload Scheduler job chains)
- Per-CBS batch architecture documentation (vendor)
- Interest accrual / AA / ECR calculation specifications
- GL reconciliation SOP
- Incident post-mortems for EOD overruns or sweep failures

---

## Cross-References

- Daily cycle definition: [concepts.md](concepts.md#daily-cycle--bod-eod-and-the-days-posting-window)
- CBS 24x7 posting posture by vendor: [core-banking-systems.md](core-banking-systems.md)
- Sweep/pooling product detail: [taxonomy-detail.md](taxonomy-detail.md#product-classes--wholesale--corporate)
- Dormancy classification detail: [retail/operations.md](retail/operations.md)
- Batch-mode payment rail settlement: [../06-payments/](../06-payments/)

---

## Open Questions

- [ ] Confirm per-bank job scheduler tooling (Control-M / Autosys / other) — affects ingestion source format.
- [ ] Confirm whether sweep execution sits inside CBS EOD or in a separate Treasury Services batch.
- [ ] Confirm SLA for EOD completion vs. next-day BOD start (varies by bank/region).
- [ ] Confirm whether real-time-rail CBS instances still run a "logical EOD" for reporting/accrual purposes even without a blackout window.
