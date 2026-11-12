# Metric definition reconciliation: an invented example

*Illustrative example with invented data.* The shop, the people, the orders and the amounts below are all invented. The business is an invented online shop selling garden tools, with a finance lead, a marketing lead and one analyst. October's "Net sales" is 695.00 in the monthly management report and 692.00 on the marketing dashboard. The analyst runs the workflow template. First come the inputs, in full, then the page it returned.

## The inputs

### 1. The question

```
Metric: Net sales. Period: October 2026. Run date: 10 November 2026.
Used for: Report 1 feeds the monthly statements. Report 2 is used by
marketing to judge campaign weeks.
```

### 2. Definition sheet, Report 1

```
Report name: Monthly management report
Report owner: Finance lead
Metric label: Net sales
Formula in words: Sum of the item value of each order, less any refund paid on that order. Shipping and sales tax are not part of item value.
Source: Shop orders table, exported 2 November 2026
One row is: one order
Included: orders with status paid, shipped, delivered or part-refunded
Excluded: cancelled orders and test orders
Date field and time zone: time the order was placed, in Pacific time
Period: calendar month in Pacific time
Refunds and adjustments: refunds deducted from the order's value
Unit and currency: US dollars
Refreshed: 2 November 2026
Notes: none
```

### 3. Definition sheet, Report 2

```
Report name: Campaign dashboard
Report owner: Marketing lead
Metric label: Net sales
Formula in words: Sum of the order total, which includes shipping and excludes sales tax. Refunds are not deducted.
Source: Shop orders feed, read through the dashboard tool
One row is: one order
Included: all orders that are not cancelled
Excluded: cancelled orders
Date field and time zone: time the order was placed, in UTC
Period: calendar month in UTC
Refunds and adjustments: not deducted
Unit and currency: US dollars
Refreshed: nightly; read 9 November 2026
Notes: none
```

### 4. Reported values

```
Report 1: 695.00, read 2 November 2026
Report 2: 692.00, read 9 November 2026
```

### 5. Extract, Report 1 (the orders it counts)

```
record_id,record_date,amount,status
1001,2026-10-03T09:12:00-07:00,120.00,paid
1002,2026-10-07T14:40:00-07:00,60.00,shipped
1003,2026-10-12T11:05:00-07:00,200.00,delivered
1004,2026-10-15T16:20:00-07:00,75.00,part-refunded
1005,2026-10-21T08:30:00-07:00,90.00,paid
1006,2026-10-31T17:45:00-07:00,150.00,paid
```

### 6. Extract, Report 2 (the orders it counts)

```
record_id,record_date,amount,status,shipping
1001,2026-10-03T16:12:00Z,128.00,paid,8.00
1002,2026-10-07T21:40:00Z,66.00,shipped,6.00
1003,2026-10-12T18:05:00Z,208.00,delivered,8.00
1004,2026-10-15T23:20:00Z,108.00,part-refunded,8.00
1005,2026-10-21T15:30:00Z,97.00,paid,7.00
1007,2026-10-01T02:10:00Z,55.00,paid,5.00
1008,2026-10-18T12:00:00Z,30.00,test,0.00
```

### 7. Owner notes (typed by the analyst)

```
The metric owner is the finance lead. The statements close on Pacific time.
```

## The output

```
METRIC DEFINITION RECONCILIATION: Net sales, October 2026

For: Finance lead (metric owner). Prepared 10 November 2026 from 2 definition sheets, two extracts, owner notes.
Purpose of the figure: Report 1 feeds the monthly statements; Report 2 is used by marketing to judge campaign weeks.

Reported values
Report 1: Monthly management report, owner Finance lead: 695.00, read 2 November 2026.
Report 2: Campaign dashboard, owner Marketing lead: 692.00, read 9 November 2026.
Gap: 3.00, Report 1 minus Report 2. Differences found total 297.00 in size and, taken as effects on the gap, net to it.

Side by side
Source: Report 1 "Shop orders table, exported 2 November 2026". Report 2 "Shop orders feed, read through the dashboard tool". Differs
What one row is: Report 1 "one order". Report 2 "one order". Same
Population included: Report 1 "orders with status paid, shipped, delivered or part-refunded". Report 2 "all orders that are not cancelled". Differs
Exclusions: Report 1 "cancelled orders and test orders". Report 2 "cancelled orders". Differs
Date used and time zone: Report 1 "time the order was placed, in Pacific time". Report 2 "time the order was placed, in UTC". Differs
Period boundaries: Report 1 "calendar month in Pacific time". Report 2 "calendar month in UTC". Differs
What is summed: Report 1 "Sum of the item value of each order, less any refund paid on that order. Shipping and sales tax are not part of item value." Report 2 "Sum of the order total, which includes shipping and excludes sales tax. Refunds are not deducted." Differs
Refunds and adjustments: Report 1 "refunds deducted from the order's value". Report 2 "not deducted". Differs
Unit and currency: Report 1 "US dollars". Report 2 "US dollars". Same
Refreshed: Report 1 "2 November 2026". Report 2 "nightly; read 9 November 2026". Differs

Row comparison
Extract check: Report 1 6 rows sum to 695.00 (ties). Report 2 7 rows sum to 692.00 (ties).
Duplicate record ids: none.
In both, same amount: 0 records, 0.00.
In both, different amount: 5 records (1001, 1002, 1003, 1004, 1005). Report 1 545.00, Report 2 607.00, difference 62.00.
Only in Report 1: 1 record (1006), 150.00.
Only in Report 2: 2 records (1007, 1008), 85.00.

Bridge from Report 1 to Report 2
Report 1 reported: 695.00
Only in Report 1, order 1006: -150.00 (1006) = 545.00
Only in Report 2, order 1007: +55.00 (1007) = 600.00
Only in Report 2, test order: +30.00 (1008) = 630.00
Different amount, shipping: +37.00 (1001, 1002, 1003, 1004, 1005) = 667.00
Different amount, not split: +25.00 (1004) = 692.00
Report 2 reported: 692.00. Unexplained remainder: 0.00.

Likely causes
Shown by the records: 3.
1. Date basis. Order 1006 (150.00) was placed 2026-10-31T17:45-07:00, which is 1 November 00:45 UTC: in October for Report 1, November for Report 2. Order 1007 (55.00) was placed 2026-09-30T19:10-07:00, which is 1 October 02:10 UTC: in October for Report 2 and, by Report 1's Pacific-time rule, in September. Net effect on the gap: +95.00 (+150.00 for 1006, -55.00 for 1007).
2. Population. Order 1008 (30.00) has status test. Report 2 excludes only cancelled orders; Report 1 excludes test orders. Effect on the gap: -30.00.
3. Shipping. Report 2 sums the order total including shipping; Report 1 excludes it. The shipping column on 1001 to 1005 totals 37.00 and equals the whole amount difference on 1001, 1002, 1003 and 1005 and 8.00 of the 33.00 difference on 1004. Effect on the gap: -37.00.
Consistent with the definitions, not shown by the records: 1. Refund on order 1004, 25.00: the 33.00 difference on 1004 less 8.00 shipping. Effect on the gap if confirmed: -25.00. Order 1004 has status part-refunded, Report 1 deducts refunds and Report 2 does not. The refund amount was not supplied; the refund paid on order 1004 would confirm it.
Not explained: none. The bridge closes. The two reports were read on different dates (2 and 9 November); both extracts tie to their reports. The Source and Refreshed differences are marked Differs, but no record in the extracts shows an amount for either, and the bridge closes without one; no amount is attributed to them.

What may be right in both
Report 2 is arithmetically consistent with its own definition (its rows sum to its reported value). A measure of order value that includes shipping, does not deduct refunds and, as the feed stands, counts test orders, by UTC day, could serve campaign tracking if it were kept apart under a label of its own, such as "Order value before refunds, including shipping". The Finance lead and the Marketing lead would decide whether test orders belong in it.

Proposed common measure
Net sales. Basis: the reports state different purposes (statements; campaign weeks). Report 1 is owned by the Finance lead, who is the metric owner, and feeds the monthly statements, which close on Pacific time, so the proposal follows that purpose; the Finance lead is asked to confirm it governs. The campaign purpose is kept apart as above.
Population: orders with status paid, shipped, delivered or part-refunded; cancelled and test orders excluded. Today: Report 1. Effect: -30.00 on the gap (Report 2 counts order 1008).
Date and period: time the order was placed, calendar month in Pacific time. Today: Report 1. Effect: +95.00 on the gap (orders 1006, 150.00, and 1007, 55.00, move months).
What is summed: item value without shipping, less refunds. Today: Report 1. Effect: -37.00 on the gap for shipping on the five shared orders; -25.00 for the refund on 1004, not confirmed.
Under the proposal the sum of Report 1's records is 695.00. This is not confirmed as correct: the owner has not yet chosen the definition.

Questions before the metric owner decides: 4
1. For Finance lead: do the monthly statements govern the purpose of "Net sales", and should it mean item value without shipping, less refunds, by Pacific order time, excluding cancelled and test orders?
2. For Finance lead and Marketing lead: should the dashboard keep a separate measure of order value including shipping for campaign weeks, and what should it be called?
3. For Marketing lead: can test orders be excluded in the dashboard's feed, so that order 1008 is not counted?
4. For Finance lead, as owner of Report 1, which deducts refunds: what refund was paid on order 1004? If it is 25.00 the refund cause is confirmed.

Draft for the Finance lead's decision. Nothing has been changed, sent or published, and no figure is declared correct.
```

Every figure traces to the two definition sheets and the two extracts supplied above. The workflow template changes no report and names no figure as correct.
