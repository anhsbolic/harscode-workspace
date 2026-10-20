# idempotent-scheduled-jobs.md

**Location:** `background-jobs/idempotent-scheduled-jobs.md`

**Principle**
A periodic batch job that computes something over a time window (a monthly calculation, a daily reconciliation) has two separate ways to run twice for the same window: the scheduler itself overlapping (a slow run still executing when the next tick fires, or a retry after a timeout that actually succeeded) and a human manually re-triggering it during an incident without realizing it already ran. An application-level "don't overlap" guard (a scheduler's built-in overlap prevention, or a distributed lock) stops the first case but not the second — a manual re-trigger is a *new* process, not an overlapping one, so it sails past an overlap guard entirely. A database-level uniqueness constraint on the identifying key of the period (e.g. `(subject_id, period)`) is the second, independent line of defense that catches both cases, because it doesn't care how or why the job ran twice — it just refuses the second write. Design the job to also survive a partial failure (it stops halfway through a batch) without either double-processing already-completed items or losing track of what wasn't finished.

**Bad**
```python
# Relies entirely on the scheduler's own overlap prevention — nothing
# stops a manual re-run (e.g. during an incident) from double-processing.
def run_monthly_commission_job():
    for account in Account.objects.filter(active=True):
        commission = calculate_commission(account, period=current_period())
        CommissionPayout.objects.create(
            account=account,
            period=current_period(),
            amount=commission,
        )
        # No uniqueness constraint on (account, period) — a second run
        # (scheduler overlap OR manual re-trigger) creates a duplicate payout.
```

**Good**
```python
# Database migration: uniqueness constraint is the real safety net,
# independent of however many times or ways the job gets triggered.
# ALTER TABLE commission_payouts ADD CONSTRAINT uniq_account_period
#     UNIQUE (account_id, period);

def run_monthly_commission_job():
    period = current_period()
    for account in Account.objects.filter(active=True):
        commission = calculate_commission(account, period=period)
        try:
            with transaction.atomic():
                CommissionPayout.objects.create(
                    account=account,
                    period=period,
                    amount=commission,
                )
        except IntegrityError:
            # Already processed this account+period — either an overlapping
            # run or a manual re-trigger. Skip and move to the next account
            # instead of failing the whole batch.
            logger.info(f"Skipping {account.id}/{period}: already processed")
            continue

# Scheduler-level overlap guard is still worth keeping as the first,
# cheaper line of defense — it just isn't sufficient alone:
# schedule.every().month.do(run_monthly_commission_job).tag('no-overlap')
```

**Checklist**
- [ ] A scheduler-level overlap guard exists (e.g. `withoutOverlapping()`, a distributed lock) as the first, cheap line of defense against concurrent runs
- [ ] A database-level uniqueness constraint on the period-identifying key exists as a second, independent line of defense — one that also catches a manual re-trigger, not just scheduler overlap
- [ ] The job's per-item write is wrapped so a uniqueness violation on one item (already processed) is caught and skipped, not treated as a fatal error that aborts the rest of the batch
- [ ] A partial failure (job stops halfway through) can be safely resumed by re-running the job — already-processed items are skipped via the uniqueness constraint, not reprocessed or duplicated
- [ ] Manual re-triggering during an incident is a scenario explicitly considered, not just automatic scheduler overlap — an on-call runbook or job design that assumes "it'll never be re-run by a person" is a gap
