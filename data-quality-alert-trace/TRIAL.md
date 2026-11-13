# Data-quality alert trace: tried on its example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-12

This record is of the second run. The template was first run the same day. That run found gaps in the instructions (listed below under "What the first run found"), and the instructions and the invented example were edited to close them. The second run, recorded here, was made by the same assistant that made the edits, after reading the first run's record. It is therefore not an independent check, and it shows only that the edited instructions can be followed to the brief below; it does not show that a reader who has not seen the first run would reach the same brief.

The inputs were the invented example in [example.md](example.md): the alert, the lineage notes, the change log, the run log, the report users list and the notes (which now include the time the brief is prepared), with default settings. No client data was used. The instruction block and output format were followed as written, and the brief was written from the inputs before it was compared with the example's published brief.

## What the first run found

The first run's brief differed from the example's in these ways, each a gap in the instructions at the time:

- A note had no kind, so the provider event was "not judged" and ranked Possible, where the example had read it as kind source and ranked it Strong.
- The preparation time was not an input; the run took it from the example's introduction.
- No rule said how to compute a difference against "at least 1,800", where a part of a day ends, whether the symptom step also gets the "beyond the threshold" mark, whether a Weak candidate must say why it stays, how far "a refresh depends on it" reaches in the gaps, or which candidate's time a "may also be affected" refresh is compared with.

## What came out

```
DATA-QUALITY ALERT TRACE: orders_clean daily row count, fired 2026-11-11 06:10 Pacific time

For: Data team lead. Prepared 2026-11-11 08:15 Pacific time from: the alert; lineage notes, 10 rows; change log, 6 entries; run log, 6 runs; report users list, 4 reports; notes.
Window: last known good 2026-11-10 06:10 Pacific time (the same check passed at 06:10 on 10 November for 9 November, with 1,934 rows). First bad 2026-11-11 06:10 Pacific time (the alert). Considered from 2026-11-03 06:10 Pacific time (7-day lookback).
Settings: lookback 7 days, row change 20%, late start 60 minutes (defaults).
Notes on the inputs: Times read in the alert's zone: last known good in the notes (06:10 on 10 November) and the next_use values in the report users list. Times placed at the latest they could mean: the upstream event, "the evening of 10 November", placed at 2026-11-10 23:59.

1. The alert
Check: volume on orders_clean. Expected at least 1,800 rows for the previous day. Observed 1,212 rows for 10 November 2026. Difference -588 against the 1,800 minimum (-32.7% of expected).
Raised by scheduled check in the monitoring tool. Severity high.

2. Affected reports and users
Downstream of orders_clean: 3 reports.
Daily sales report. Owner Head of e-commerce. Used by Trading team. Next use 2026-11-12 09:00. Refresh: by schedule, refreshed at 06:00 on 2026-11-11 after the bad build; not confirmed by the run log. Path: orders_clean → daily_sales_model → Daily sales report.
Retention dashboard. Owner CRM lead. Used by CRM team. Next use 2026-11-13 (time not stated). Refresh: by schedule, refreshed at 06:30 on 2026-11-11 after the bad build; not confirmed by the run log. Path: orders_clean → customer_model → Retention dashboard.
Weekly trading pack. Owner Finance lead. Used by Leadership team. Next use 2026-11-16 10:00. Refresh: not due since the bad build; next Monday 2026-11-16. Path: orders_clean → daily_sales_model → Weekly trading pack.
End points not in the report users list: none.
May also be affected if a Strong candidate is confirmed: Payments reconciliation, via candidate 1 and 2. Owner Finance lead. Used by Finance team. Next use 2026-11-11 10:00. Refresh: by schedule, refreshed at 07:00 on 2026-11-11, after candidate 1 (finished 03:41) and candidate 2 (placed 23:59 on 2026-11-10); not confirmed by the run log. Path: payments_raw → Payments reconciliation.

3. The path the data takes
Upstream: shop_platform_export → (load_orders, daily 02:00, Data engineering) → orders_raw → (build_orders_clean, daily 04:00, Analytics engineering) → orders_clean
Upstream: payments_feed → (load_payments, daily 02:30, Data engineering) → payments_raw → (build_orders_clean, daily 04:00, Analytics engineering) → orders_clean
Downstream: orders_clean → (build_daily_sales, daily 05:00, Analytics engineering) → daily_sales_model → (refresh_daily_sales, daily 06:00, BI team) → Daily sales report
Downstream: orders_clean → (build_daily_sales, daily 05:00, Analytics engineering) → daily_sales_model → (manual, weekly Monday, Finance) → Weekly trading pack
Downstream: orders_clean → (build_customers, daily 05:00, owner not stated) → customer_model → (refresh_retention, daily 06:30, BI team) → Retention dashboard
Row flow: load_orders: 1,951 (2026-11-10 02:00) → 1,948 (2026-11-11 02:00): -3 (-0.2%).
Row flow: load_payments: 1,890 (2026-11-10 02:30) → 1,236 (2026-11-11 02:30, partial): -654 (-34.6%). Beyond the threshold.
Row flow: build_orders_clean: 1,934 (2026-11-10 04:00) → 1,212 (2026-11-11 04:00): -722 (-37.3%). Beyond the threshold. Writes the alerted object: this is the symptom.
Rows into and out of build_orders_clean, from orders_raw: last good 1,951 in, 1,934 out, 17 dropped (0.9%); bad run 1,948 in, 1,212 out, 736 dropped (37.8%).
Gaps in the lineage: build_customers (orders_clean → customer_model) has no owner. No run-log rows for build_daily_sales, build_customers, refresh_daily_sales, refresh_retention, the manual step into the Weekly trading pack, or build_recon (the step into Payments reconciliation).

4. Candidate causes, ranked by the evidence supplied
1. Strong. Run of load_payments, partial, on load_payments (writes payments_raw), 2026-11-11 02:30. 1,236 rows against 1,890 in the previous successful run (-654, -34.6%); note: "provider file arrived in two parts; second part not loaded". Hops from the alerted object: 1. Timing: inside the window. Fits a volume check: yes, partial run and row change. Who to ask: Data engineering. Linked with candidates 2, 3 and 4.
2. Strong. Note, on payments_feed, 2026-11-10 23:59 (placed; "the evening of 10 November"). Payment provider P's status page said settlement files for that day could arrive in two parts. Hops from the alerted object: 2. Timing: inside the window. Fits a volume check: yes, source (an upstream event in the notes is read as kind source). Who to ask: Data engineering, owner of load_payments, which reads payments_feed. Linked with candidate 1.
3. Strong. Change DATA-320, logic, on build_orders_clean, 2026-11-10 11:30. Changed the payments join from a left join to an inner join so unpaid orders drop out. Hops from the alerted object: 0. Timing: inside the window. Fits a volume check: yes, logic. Who to ask: Analytics engineering. Linked with candidates 1 and 4.
4. Weak. Change DATA-318, schema, on payments_raw, 2026-11-09 16:45. Settlement file adds a payment_ref column; order_id now arrives as text. Hops from the alerted object: 1. Timing: before last known good. Fits a volume check: yes, schema. Stays because an earlier change can combine with a later one; it was already in place for the runs of load_payments (2026-11-10 02:30) and build_orders_clean (2026-11-10 04:00, 1,934 rows) before last known good. Who to ask: Data engineering. Linked with candidates 1 and 3.
Set aside: DATA-322, check, on orders_clean, 2026-11-11 07:05 (reviewed the alert threshold after it fired; no change made): after the first bad data.
Off the path, not ranked: DATA-311, logic, on daily_sales_model, 2026-11-03 15:20: downstream of the alerted object. DATA-321, access, on Retention dashboard, 2026-11-10 14:00: downstream of the alerted object.
Older than the lookback, not considered: 1 (DATA-305, schedule on load_orders, 2026-10-29 10:00).

5. What to check next
1. Candidate 1, ask Data engineering: compare the number of settlements in both parts of Payment provider P's file for 10 November with the 1,236 rows load_payments wrote to payments_raw on 11 November (1,890 the day before). Confirms it if the second part holds settlements that are not in payments_raw. Rules it out if payments_raw already holds every settlement in both parts.
2. Candidate 2, ask Data engineering: find when the second part of the 10 November settlement file reached payments_feed. Confirms it if it arrived after load_payments started at 02:30 on 11 November. Rules it out if it was there before 02:30.
3. Candidate 3, ask Analytics engineering: count the 10 November orders in orders_raw that have no matching order_id in payments_raw. Confirms it if that count, with the test and cancelled orders the build removes (17 in the last good run), comes close to the 736 rows dropped in the bad run. Rules it out if few orders lack a match.
4. Candidate 4, ask Data engineering: compare how order_id is stored in payments_raw and in orders_raw for 10 November, since DATA-318 says it now arrives as text. Confirms it if the two differ and orders fail to match on order_id because of it. Rules it out if they are stored the same way, as the last good build, which ran after DATA-318, produced 1,934 rows.
Gaps to close: build_customers has no owner, ask Analytics engineering, owner of build_orders_clean, the hop just upstream. Whether the steps with no run-log rows ran at their scheduled times on 11 November: ask Analytics engineering for build_daily_sales and build_customers, BI team for refresh_daily_sales and refresh_retention, Finance for the manual step into the Weekly trading pack and for build_recon.

6. Decisions for the Data team lead
1. Whether and when to tell the owners and users of the three affected reports. By schedule, the Daily sales report (06:00) and the Retention dashboard (06:30) refreshed on 2026-11-11 with the data in question. The soonest next use is the Daily sales report, 2026-11-12 09:00 (Head of e-commerce; Trading team). The Weekly trading pack is next used 2026-11-16 10:00 (Finance lead; Leadership team).
2. Whether to tell the Finance lead before the Payments reconciliation is used at 10:00 today, 2026-11-11. It may also be affected if candidate 1 or 2 is confirmed, and by schedule it refreshed at 07:00, after the partial load.
3. Who confirms the cause and, with the owner of the step concerned, authorizes any fix or rerun? The notes name no data owner for the orders and payments tables, and say nothing has been rerun or changed since the alert.

Draft for the Data team lead. No query has been run; nothing has been changed, rerun, muted or sent; no candidate is confirmed as the cause.
```

## What was observed

Every part of the output format was produced. No header mismatched, nothing was missing from the alert or the notes, and no input held a secret, a personal detail or text that read as an instruction. Nothing made the assistant stop. The provider event was ranked Strong by the new rule (kind source, which fits a volume check), and every figure recomputes: -588 (-32.7%), -3 (-0.2%), -654 (-34.6%), -722 (-37.3%), 17 (0.9%) and 736 (37.8%).

Because the second run was made by the assistant that made the edits, the match with the published example is expected and proves little. The differences that remain are in wording only: this run wrote ISO dates and the decisions and checks are worded slightly differently from the example. The example's check on candidate 4 states the 10 November 04:00 build fact in a separate sentence, and this run folds it into the rule-out condition.

Still open, not closed by this run:

- **Linking is generous.** Under the rule as written, almost every candidate around payments_raw is linked with every other. It is correct but says little. The rule was left as it is.
- **The weekly pack's refresh.** Its step is "manual" with a weekly schedule and no time, so "next [when]" can only give a day.
- **Check wording.** The assistant's check on candidate 2 (when the second part of the provider file arrived) assumes the second part arrived late, which the inputs do not say. The checks describe what to compare and are not findings.
- **Facts not in the inputs:** none. The preparation time is now in the notes, and "today" in decision 2 follows from it.

The brief named no candidate as the cause, ran no query and changed nothing. Whether the Strong candidates are right is for the data owner to confirm.

## Edits made after this run

After an independent review, these edits were made. The template was not run again, and the record above is unchanged:

- The window rule now says that last known good is the time the check last passed, not the time the checked data was built, and that an item in either gap is noted. The example's inputs have no item in either gap, so the brief above is not affected.
- The rule for a Weak candidate now names "the step that writes the changed object". The brief above already named load_payments and build_orders_clean for candidate 4; the published example now does too.
- The instruction block now defines "the bad build" and says that a time with no zone is read in the alert's zone.
- In the published example (not in the run above), the check on candidate 2 now reads "find whether and when the second part ... reached payments_feed", and the check on candidate 3 refers to "the 17 rows the build dropped in the last good run". The run above still has the earlier wording for both, so the third open item above was closed in the example only.
