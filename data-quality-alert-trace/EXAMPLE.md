# Data-quality alert trace: an invented example

*Illustrative example with invented data.* The shop, the people, the tables, the tickets, the payment provider and every figure below are invented. The business is an invented online kitchenware shop of about 60 people, with a small data team: a data team lead, two data engineers and an analytics engineer. At 06:10 on 11 November 2026 the daily row count on the cleaned orders table fails. The data team lead runs the workflow template at 08:15. First come the inputs, in full, then the brief it returned.

## The inputs

### 1. The alert

```
Alert name: orders_clean daily row count
Check type: volume
Object checked: orders_clean
Expected: at least 1,800 rows for the previous day
Observed: 1,212 rows for 10 November 2026
Fired at: 2026-11-11 06:10 Pacific time
Raised by: scheduled check in the monitoring tool
Severity: high
```

### 2. Lineage notes

```
from_object,to_object,step,transform,schedule,owner
shop_platform_export,orders_raw,load_orders,copy of the day's orders file,daily 02:00,Data engineering
payments_feed,payments_raw,load_payments,copy of the day's settlement file,daily 02:30,Data engineering
orders_raw,orders_clean,build_orders_clean,removes test and cancelled orders; joins payments on order_id,daily 04:00,Analytics engineering
payments_raw,orders_clean,build_orders_clean,joined to orders on order_id,daily 04:00,Analytics engineering
orders_clean,daily_sales_model,build_daily_sales,sums by day and channel,daily 05:00,Analytics engineering
orders_clean,customer_model,build_customers,first and latest order per customer,daily 05:00,
daily_sales_model,Daily sales report,refresh_daily_sales,dashboard refresh,daily 06:00,BI team
daily_sales_model,Weekly trading pack,manual,copied into slides,weekly Monday,Finance
customer_model,Retention dashboard,refresh_retention,dashboard refresh,daily 06:30,BI team
payments_raw,Payments reconciliation,build_recon,matches settlements to bank deposits,daily 07:00,Finance
```

### 3. Recent change log

```
changed_at,object,kind,change,changed_by,ticket
2026-10-29T10:00:00-07:00,load_orders,schedule,moved the daily start from 01:30 to 02:00,Data engineering,DATA-305
2026-11-03T15:20:00-08:00,daily_sales_model,logic,added the marketplace channel to the channel mapping,Analytics engineering,DATA-311
2026-11-09T16:45:00-08:00,payments_raw,schema,"settlement file adds a payment_ref column; order_id now arrives as text",Data engineering,DATA-318
2026-11-10T11:30:00-08:00,build_orders_clean,logic,changed the payments join from a left join to an inner join so unpaid orders drop out,Analytics engineering,DATA-320
2026-11-10T14:00:00-08:00,Retention dashboard,access,added CRM team viewers,BI team,DATA-321
2026-11-11T07:05:00-08:00,orders_clean,check,reviewed the alert threshold after it fired; no change made,Data engineering,DATA-322
```

### 4. Run log

```
step,run_started,run_finished,status,rows_out,note
load_orders,2026-11-10T02:00:00-08:00,2026-11-10T02:06:00-08:00,success,1951,
load_payments,2026-11-10T02:30:00-08:00,2026-11-10T02:34:00-08:00,success,1890,
build_orders_clean,2026-11-10T04:00:00-08:00,2026-11-10T04:09:00-08:00,success,1934,
load_orders,2026-11-11T02:00:00-08:00,2026-11-11T02:07:00-08:00,success,1948,
load_payments,2026-11-11T02:30:00-08:00,2026-11-11T03:41:00-08:00,partial,1236,provider file arrived in two parts; second part not loaded
build_orders_clean,2026-11-11T04:00:00-08:00,2026-11-11T04:08:00-08:00,success,1212,
```

### 5. Report users list

```
report,owner,used_by,next_use
Daily sales report,Head of e-commerce,Trading team,2026-11-12 09:00
Weekly trading pack,Finance lead,Leadership team,2026-11-16 10:00
Retention dashboard,CRM lead,CRM team,2026-11-13
Payments reconciliation,Finance lead,Finance team,2026-11-11 10:00
```

### 6. Notes (typed by the data team lead)

```
Run by: Data team lead. Team time zone: Pacific time.
Prepared at: 2026-11-11 08:15 Pacific time.
Last known good: the same check passed at 06:10 on 10 November for
  9 November, with 1,934 rows.
orders_clean takes its rows from orders_raw: one row per order, less test
  and cancelled orders.
Upstream event, on payments_feed: Payment provider P's status page said,
  on the evening of 10 November, that settlement files for that day could
  arrive in two parts. Copied into the incident channel by the on-call
  engineer.
Already done: nothing rerun or changed since the alert.
Data owner for the orders and payments tables: not named.
```

No settings were supplied, so the defaults apply.

## The output

```
DATA-QUALITY ALERT TRACE: orders_clean daily row count, fired 11 November 2026 06:10 Pacific time

For: Data team lead. Prepared 11 November 2026 08:15 Pacific time from: the alert; lineage notes, 10 rows; change log, 6 entries; run log, 6 runs; report users list, 4 reports; notes.
Window: last known good 10 November 2026 06:10 (the same check passed, per the notes). First bad 11 November 2026 06:10 (the alert). Considered from 3 November 2026 06:10 (7-day lookback).
Settings: lookback 7 days, row change 20%, late start 60 minutes (defaults).
Notes on the inputs: Times read in the alert's zone: last known good in the notes (06:10 on 10 November) and the next_use values in the report users list. Times placed at the latest they could mean: the upstream event, "the evening of 10 November", placed at 23:59 on 10 November.

1. The alert
Check: volume on orders_clean. Expected at least 1,800 rows for the previous day. Observed 1,212 rows for 10 November 2026. Difference -588 against the 1,800 minimum (-32.7% of expected).
Raised by scheduled check in the monitoring tool. Severity high.

2. Affected reports and users
Downstream of orders_clean: 3 reports.
Daily sales report. Owner Head of e-commerce. Used by Trading team. Next use 12 November 09:00. Refresh: by schedule, refreshed at 06:00 on 11 November after the bad build; not confirmed by the run log. Path: orders_clean → daily_sales_model → Daily sales report.
Retention dashboard. Owner CRM lead. Used by CRM team. Next use 13 November (time not stated). Refresh: by schedule, refreshed at 06:30 on 11 November after the bad build; not confirmed by the run log. Path: orders_clean → customer_model → Retention dashboard.
Weekly trading pack. Owner Finance lead. Used by Leadership team. Next use 16 November 10:00. Refresh: not due since the bad build; next Monday 16 November. Path: orders_clean → daily_sales_model → Weekly trading pack.
End points not in the report users list: none.
May also be affected if a Strong candidate is confirmed: Payments reconciliation, via candidates 1 and 2. Owner Finance lead. Used by Finance team. Next use 11 November 10:00. Refresh: by schedule, refreshed at 07:00 on 11 November, after candidate 1 (finished 03:41) and candidate 2 (placed 23:59 on 10 November); not confirmed by the run log. Path: payments_raw → Payments reconciliation.

3. The path the data takes
Upstream: shop_platform_export → (load_orders, daily 02:00, Data engineering) → orders_raw → (build_orders_clean, daily 04:00, Analytics engineering) → orders_clean
Upstream: payments_feed → (load_payments, daily 02:30, Data engineering) → payments_raw → (build_orders_clean, daily 04:00, Analytics engineering) → orders_clean
Downstream: orders_clean → (build_daily_sales, daily 05:00, Analytics engineering) → daily_sales_model → (refresh_daily_sales, daily 06:00, BI team) → Daily sales report
Downstream: orders_clean → (build_daily_sales, daily 05:00, Analytics engineering) → daily_sales_model → (manual, weekly Monday, Finance) → Weekly trading pack
Downstream: orders_clean → (build_customers, daily 05:00, owner not stated) → customer_model → (refresh_retention, daily 06:30, BI team) → Retention dashboard
Row flow: load_orders: 1,951 (10 November 02:00) → 1,948 (11 November 02:00): -3 (-0.2%).
Row flow: load_payments: 1,890 (10 November 02:30) → 1,236 (11 November 02:30, partial): -654 (-34.6%). Beyond the threshold.
Row flow: build_orders_clean: 1,934 (10 November 04:00) → 1,212 (11 November 04:00): -722 (-37.3%). Beyond the threshold. Writes the alerted object: this is the symptom.
Rows into and out of build_orders_clean, from orders_raw: last good 1,951 in, 1,934 out, 17 dropped (0.9%); bad run 1,948 in, 1,212 out, 736 dropped (37.8%).
Gaps in the lineage: build_customers (orders_clean → customer_model) has no owner. No run-log rows for build_daily_sales, build_customers, refresh_daily_sales, refresh_retention, the manual step into the Weekly trading pack, or build_recon.

4. Candidate causes, ranked by the evidence supplied
1. Strong. Run of load_payments, partial, on load_payments (writes payments_raw), 11 November 02:30. 1,236 rows against 1,890 in the previous successful run (-654, -34.6%); note: "provider file arrived in two parts; second part not loaded". Hops from the alerted object: 1. Timing: inside the window. Fits a volume check: yes, partial run and row change. Who to ask: Data engineering. Linked with candidates 2, 3 and 4.
2. Strong. Note, on payments_feed, 10 November 23:59 (placed; "the evening of 10 November"). Payment provider P's status page said settlement files for that day could arrive in two parts. Hops from the alerted object: 2. Timing: inside the window. Fits a volume check: yes, source. Who to ask: Data engineering, owner of load_payments, which reads payments_feed. Linked with candidate 1.
3. Strong. Change DATA-320, logic, on build_orders_clean, 10 November 11:30. Changed the payments join from a left join to an inner join so unpaid orders drop out. Hops from the alerted object: 0. Timing: inside the window. Fits a volume check: yes, logic. Who to ask: Analytics engineering. Linked with candidates 1 and 4.
4. Weak. Change DATA-318, schema, on payments_raw, 9 November 16:45. Settlement file adds a payment_ref column; order_id now arrives as text. Hops from the alerted object: 1. Timing: before last known good. Fits a volume check: yes, schema. Stays because an earlier change can combine with a later one; it was already in place for the runs of load_payments (10 November 02:30) and build_orders_clean (10 November 04:00, 1,934 rows) before last known good. Who to ask: Data engineering. Linked with candidates 1 and 3.
Set aside: DATA-322, check, on orders_clean, 11 November 07:05 (reviewed the alert threshold after it fired; no change made): after the first bad data.
Off the path, not ranked: DATA-311, logic, on daily_sales_model, 3 November 15:20: downstream of orders_clean. DATA-321, access, on Retention dashboard, 10 November 14:00: downstream of orders_clean.
Older than the lookback, not considered: 1 (DATA-305, 29 October).

5. What to check next
1. Candidate 1, ask Data engineering: compare the number of settlements in both parts of Payment provider P's file for 10 November with the 1,236 rows load_payments wrote to payments_raw on 11 November (1,890 the day before). Confirms it if the second part holds settlements that are not in payments_raw. Rules it out if payments_raw already holds every settlement in both parts.
2. Candidate 2, ask Data engineering: find whether and when the second part of the 10 November settlement file reached payments_feed. Confirms it if the second part reached payments_feed after load_payments started at 02:30 on 11 November. Rules it out if it was there before 02:30.
3. Candidate 3, ask Analytics engineering: count the 10 November orders in orders_raw that have no matching order_id in payments_raw. Confirms it if that count, with the 17 rows the build dropped in the last good run, comes close to the 736 rows dropped in the bad run. Rules it out if few orders lack a match.
4. Candidate 4, ask Data engineering: compare how order_id is stored in payments_raw and in orders_raw for 10 November, since DATA-318 says it now arrives as text. Confirms it if the two differ and orders fail to match on order_id because of it. Rules it out if they are stored the same way. Note that the last good build ran on 10 November at 04:00, after DATA-318, and still produced 1,934 rows.
Gaps to close: build_customers has no owner, ask Analytics engineering, owner of build_orders_clean, the hop just upstream. Whether the steps with no run-log rows ran at their scheduled times on 11 November: ask Analytics engineering for build_daily_sales and build_customers, BI team for refresh_daily_sales and refresh_retention, Finance for the manual step into the Weekly trading pack and for build_recon.

6. Decisions for the Data team lead
1. Whether and when to tell the owners and users of the three affected reports. By schedule, the Daily sales report (06:00) and the Retention dashboard (06:30) have already refreshed with the data in question. The soonest next use is the Daily sales report at 09:00 on 12 November (Head of e-commerce; Trading team). The Weekly trading pack is next used at 10:00 on 16 November (Finance lead; Leadership team).
2. Whether to tell the Finance lead before the Payments reconciliation is used at 10:00 today, 11 November. It may also be affected if candidate 1 or 2 is confirmed, and by schedule it refreshed at 07:00, after the partial load.
3. Who confirms the cause and, with the owner of the step concerned, authorizes any fix or rerun? The notes name no data owner for the orders and payments tables, and say nothing has been rerun or changed since the alert.

Draft for the Data team lead. No query has been run; nothing has been changed, rerun, muted or sent; no candidate is confirmed as the cause.
```

Every figure traces to the alert, the lineage notes, the change log, the run log, the report users list and the notes above. The workflow template ran no query, changed nothing and told no one; the data team lead decides who checks what and who is told.
