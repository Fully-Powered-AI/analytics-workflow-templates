# Dashboard and report inventory review: an example

*Illustrative example with sample data.* Company X is an illustrative online homeware retailer with about 120 people. Its business intelligence tool's licence renews on 1 February 2027, and its old orders database is being switched off on 31 January. The reporting administrator runs the review for the analytics lead, who decides what is retired. The owners appear as letters, and every item, folder, date and count below is illustrative.

The inputs come first, in full, so the workflow template can be run on them. The review follows.

## The inputs

### 1. The team's rules and today's date (typed by the reporting administrator)

```
Company: Company X
Today: Monday 7 December 2026
Prepared by: Reporting administrator
Who decides retirement: Analytics lead
Unused after: 90 days without a view
Exempt folders: Finance/Statutory (kept for the auditors)
Data sources marked for retirement: legacy_orders_db, retiring 31 January 2027
```

### 2. The leavers list

```
Owner D
Owner G
```

### 3. The dashboard and usage export from your business intelligence tool (exported Monday 7 December 2026)

```
item_id,name,type,folder,owner,created_at,last_edited_at,last_viewed_at,views_90d,distinct_viewers_90d,data_source,scheduled
D-01,Weekly Sales,dashboard,Sales,Owner A,2024-03-04,2026-11-30,2026-12-04,412,23,warehouse.sales,yes
D-02,Weekly Sales (copy),dashboard,Sales,Owner B,2025-06-10,2025-06-12,2026-05-20,0,0,warehouse.sales,no
D-03,Weekly sales v2,dashboard,Sales/Archive,Owner A,2025-09-01,2025-09-03,2026-10-02,3,1,warehouse.sales,no
D-04,Campaign Performance,dashboard,Marketing,Owner C,2025-01-15,2026-10-20,2026-12-03,158,9,warehouse.marketing,yes
R-05,Monthly Returns,report,Operations,Owner D,2023-11-02,2025-02-10,2026-11-28,41,4,legacy_orders_db,yes
R-06,Supplier Lead Times,report,Operations,,2024-05-20,2024-05-20,,0,0,legacy_orders_db,yes
D-07,Budget vs Actual,dashboard,Finance/Statutory,Owner E,2023-01-09,2026-01-12,2026-03-02,0,0,sheet_budget,yes
R-08,Daily Stock Alert,report,Operations,Owner C,2024-08-11,2025-12-01,2026-06-30,0,0,warehouse.sales,yes
D-09,Holiday Trading 2026,dashboard,Sales,Owner B,2026-10-26,2026-11-02,2026-12-01,37,6,warehouse.sales,no
D-10,Customer Cohorts,dashboard,Marketing,Owner D,2025-04-14,2025-04-30,2026-07-15,0,0,warehouse.marketing,no
R-11,Returns by Reason,report,Operations,Owner F,2024-02-02,2026-09-14,2026-12-02,18,3,warehouse.sales,no
D-12,New Product Launch,dashboard,Marketing,Owner C,2026-11-16,2026-11-16,,0,0,warehouse.marketing,no
R-13,Monthly returns,report,Finance,Owner E,2025-03-03,2025-03-03,2026-09-01,0,0,legacy_orders_db,no
D-14,Margin Tracker,dashboard,Finance,Owner A,2024-07-07,2025-08-19,2026-08-30,2,1,warehouse.sales,no
```

## The output

```
DASHBOARD AND REPORT INVENTORY REVIEW: Company X, as of Monday 7 December 2026

For: Analytics lead. Prepared by Reporting administrator from the dashboard and usage export, exported 7 December 2026.
Rules: unused after 90 days without a view. Exempt folders: Finance/Statutory. Leavers list: supplied, 2 names. Data sources marked for retirement: legacy_orders_db, retiring 31 January 2027.

Count
Items read: 14 (9 dashboards, 5 reports). Flagged: 8. Export checks only: 1. Not flagged: 5, of which 1 in an exempt folder and 2 new. 8 + 1 + 5 = 14.

1. Unused past the limit: 5
D-02 "Weekly Sales (copy)" (dashboard, Sales). Owner: Owner B. Last viewed 2026-05-20, 201 days ago. Views 90 days: 0. Viewers 90 days: 0. Scheduled: no.
D-10 "Customer Cohorts" (dashboard, Marketing). Owner: Owner D. Last viewed 2026-07-15, 145 days ago. Views 90 days: 0. Viewers 90 days: 0. Scheduled: no.
R-06 "Supplier Lead Times" (report, Operations). Owner: blank. Last viewed never recorded. Views 90 days: 0. Viewers 90 days: 0. Scheduled: yes.
R-08 "Daily Stock Alert" (report, Operations). Owner: Owner C. Last viewed 2026-06-30, 160 days ago. Views 90 days: 0. Viewers 90 days: 0. Scheduled: yes.
R-13 "Monthly returns" (report, Finance). Owner: Owner E. Last viewed 2026-09-01, 97 days ago. Views 90 days: 0. Viewers 90 days: 0. Scheduled: no.

2. Owner has left or is blank: 3
D-10 "Customer Cohorts". Owner: Owner D, on the leavers list. Last viewed 2026-07-15. Views 90 days: 0.
R-05 "Monthly Returns". Owner: Owner D, on the leavers list. Last viewed 2026-11-28. Views 90 days: 41.
R-06 "Supplier Lead Times". Owner: blank. Last viewed never recorded. Views 90 days: 0.

3. Likely duplicates: 2 groups, 5 items
Group 1, "weekly sales" on warehouse.sales: D-01 "Weekly Sales", Owner A, views 90 days 412, last edited 2026-11-30; D-02 "Weekly Sales (copy)", Owner B, views 90 days 0, last edited 2025-06-12; D-03 "Weekly sales v2", Owner A, views 90 days 3, last edited 2025-09-03.
Group 2, "monthly returns" on legacy_orders_db: R-05 "Monthly Returns", Owner D, views 90 days 41, last edited 2025-02-10; R-13 "Monthly returns", Owner E, views 90 days 0, last edited 2025-03-03.
Same name, different data source: none.

4. Scheduled sends with no views in the tool: 2
R-06 "Supplier Lead Times". Owner: blank. Last viewed never recorded. Views 90 days: 0.
R-08 "Daily Stock Alert". Owner: Owner C. Last viewed 2026-06-30. Views 90 days: 0.
The export cannot show whether anyone reads the scheduled copy outside the tool.

5. On a data source marked for retirement: 3
legacy_orders_db, retiring 31 January 2027: R-05 "Monthly Returns", Owner D, views 90 days 41; R-06 "Supplier Lead Times", owner blank, views 90 days 0; R-13 "Monthly returns", Owner E, views 90 days 0.

6. Export checks: 1
D-14: last_viewed_at is 2026-08-30 and views_90d is 2; a last view 99 days ago means no views in the last 90 days, so the two fields disagree. Not judged on: unused, scheduled sends.

7. Proposed list to ask owners about: 4 owners, 8 items
Owner A
- D-01 "Weekly Sales": duplicate (group 1). Which item in group 1 does the work, and does this one still serve a purpose?
- D-03 "Weekly sales v2": duplicate (group 1). Which item in group 1 does the work, and does this one still serve a purpose?
Owner B
- D-02 "Weekly Sales (copy)": unused, duplicate (group 1). Is it still needed, and by whom? Which item in group 1 does the work, and does this one still serve a purpose?
Owner C
- R-08 "Daily Stock Alert": unused, scheduled send. Is it still needed, and by whom? Does anyone read the scheduled copy, and should the send continue?
Owner E
- R-13 "Monthly returns": unused, duplicate (group 2), retiring source. Is it still needed, and by whom? Which item in group 2 does the work, and does this one still serve a purpose? Will it be rebuilt on another source before 31 January 2027, or retired with the source?
No owner to ask, for Analytics lead
- D-10 "Customer Cohorts": owner on the leavers list, unused. Who owns it now? Is it still needed, and by whom?
- R-05 "Monthly Returns": owner on the leavers list, duplicate (group 2), retiring source. Who owns it now? Which item in group 2 does the work, and does this one still serve a purpose? Will it be rebuilt on another source before 31 January 2027, or retired with the source?
- R-06 "Supplier Lead Times": owner blank, unused, scheduled send, retiring source. Who owns it now? Is it still needed, and by whom? Does anyone read the scheduled copy, and should the send continue? Will it be rebuilt on another source before 31 January 2027, or retired with the source?
Export questions, for Reporting administrator
- D-14: last_viewed_at (2026-08-30) and views_90d (2) disagree. Which is right in the tool?

Draft for Analytics lead. Nothing has been retired, deleted, moved, rescheduled or sent. Views and viewers are counts per item from the export; no person is ranked.
```

Three items are left out of the use checks on purpose: D-07 sits in the exempt folder, and D-09 and D-12 were created within the last 90 days. Every figure traces to the export and the rules above. The review retires, deletes, moves and reschedules nothing, and the analytics lead decides each item after the owners answer.
