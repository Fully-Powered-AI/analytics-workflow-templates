# Dashboard brief: an invented example

*Illustrative example with invented data.* Tern Hollow Candles is an invented online shop with four staff. The owner asked the operations lead for a dashboard in a spreadsheet. Everything below, the people, the files and every date and count, is invented. The brief contains no figures, because the work never makes any.

## What the person supplies

**Requester's notes**

The owner wants one spreadsheet called "Monday trading view". The owner and the operations lead will open it on Monday mornings. It will be built in a spreadsheet the shop already uses. Reporting is weekly for ads and orders, by product for stock, and monthly for shipping. Filters wanted: week range, month, ad channel, product, and customer region. Only the owner and the operations lead may see it, and no customer details should appear. The operations lead will refresh it every Monday by 9:30. The brief is being prepared on 3 November 2026.

**Decision sheet** (`decision_code, decision, decider, cadence`)

```
D1,"Raise, hold or cut next week's ad budget",Owner,Weekly (Monday)
D2,"Which products to reorder this week",Operations lead,Weekly (Monday)
D3,"Whether to keep free shipping on all orders",Owner,Monthly (first Monday)
```

**Metric list** (`code, metric, decisions, meaning, formula, source_file, columns_used, unit, grain, better`)

```
M1,Ad spend,D1,"Money spent on ads in the week","sum of spend",ads_export.csv,"ads_export.csv: spend, week_start",USD,week,neither
M2,Orders,D1,"Orders placed in the week, not cancelled",,orders_export.csv,"orders_export.csv: order_id, order_date, status",count,week,higher
M3,Spend per order,D1,"Ad spend for each order placed","M1 / M2","ads_export.csv; orders_export.csv","ads_export.csv: spend, week_start; orders_export.csv: order_id, order_date, status",USD,week,lower
M4,Days of stock left,D2,"How long stock on hand lasts at the recent selling pace","on_hand / (units sold in the last 28 days / 28)","stock_export.csv; orders_export.csv","stock_export.csv: sku, on_hand, snapshot_date; orders_export.csv: product_sku, quantity, order_date, status",days,product,higher
M5,Free-shipping share of orders,D3,"Share of orders where the customer paid no shipping","orders with shipping_charged of 0 / all orders",orders_export.csv,"orders_export.csv: order_id, shipping_charged, order_date, status",percent,month,neither
M6,Daily ad spend,D1,"Ad spend for each day","sum of spend per day",ads_export.csv,"ads_export.csv: spend, week_start",USD,day,neither
M7,Website sessions,,"Visits to the shop's site",,,,count,week,higher
M8,Average order value,D3,"Average amount per order","sum of line_total / number of orders",orders_export.csv,"orders_export.csv: order_id, line_total, order_date, status",USD,month,higher
```

**Source sheet** (`source_file, what_it_holds, one_row_per, date_column, columns, extracted_on, first_date, last_date, rows, owner`)

```
orders_export.csv,"Order lines from the online shop","order line",order_date,"order_id, order_date, status, product_sku, quantity, line_total, shipping_charged, discount",2026-11-02,2026-05-04,2026-11-01,4312,Operations lead
ads_export.csv,"Weekly ad spend by channel","week and channel",week_start,"week_start, channel, spend, clicks",2026-10-26,2026-05-04,2026-10-19,50,Owner
stock_export.csv,"Stock on hand by product","product",snapshot_date,"sku, product_name, on_hand, snapshot_date",2026-11-02,2026-11-02,2026-11-02,38,Operations lead
```

## What comes out

```
DASHBOARD BRIEF: Monday trading view

Prepared 3 November 2026 for the owner. To be built in a spreadsheet the shop already uses. Status: DRAFT, not approved. This brief contains no figures.

1. DECISIONS SERVED
D1. Raise, hold or cut next week's ad budget. Decided by the owner, weekly (Monday). Shown by: M1, M2, M3.
D2. Which products to reorder this week. Decided by the operations lead, weekly (Monday). Shown by: M4.
D3. Whether to keep free shipping on all orders. Decided by the owner, monthly (first Monday). Shown by: M5, M8.
Decisions with no metric: none.

2. WHAT IS SHOWN
Viewers: the owner and the operations lead, opened Monday mornings. Access: only the owner and the operations lead; no customer details to appear.
View 1, Ad budget, serves D1:
- M1 Ad spend: number for [latest full week] with [week before] beside it.
- M2 Orders: number for [latest full week] with [week before] beside it.
- M3 Spend per order: number for [latest full week] with [week before] beside it.
View 2, Reorder, serves D2:
- M4 Days of stock left: table by product, with [sku], [product name] and [days left], lowest [days left] first, then products shown as "no sales in the window".
View 3, Free shipping, serves D3:
- M5 Free-shipping share of orders: number for [latest full month] with [month before] beside it.
- M8 Average order value: number for [latest full month] with [month before] beside it.
Items on the page: 6 of 10.

3. METRIC DEFINITIONS
M1 Ad spend. Status: AS SUPPLIED. Open questions: 1, 7.
- Meaning: Money spent on ads in the week.
- Formula: sum of spend. Read in the columns supplied: spend in ads_export.csv, by week_start.
- Includes and excludes: every row whose week_start is that week, all channels unless the channel filter is set. Which day a week starts is Question 1.
- Unit, rounding and grain: USD; whole dollars; week.
- Better when: neither.
- Source: ads_export.csv; spend, week_start.
- When the data is missing: "no data".

M2 Orders. Status: PROPOSED, for approval. Open questions: 1, 2.
- Meaning: Orders placed in the week, not cancelled.
- Formula: number of different order_id values in orders_export.csv whose order_date is in the week and whose status is not a cancelled status. (Proposed, because no formula was supplied. The export has one row per order line, so each order is counted once.)
- Includes and excludes: leaves out lines whose status means cancelled, as the meaning says; which values of status mean cancelled is Question 2.
- Unit, rounding and grain: count; whole number; week.
- Better when: higher.
- Source: orders_export.csv; order_id, order_date, status.
- When the data is missing: "no orders".

M3 Spend per order. Status: AS SUPPLIED; rests on M2, PROPOSED. Open questions: 1, 2, 7.
- Meaning: Ad spend for each order placed.
- Formula: M1 / M2
- Includes and excludes: M1 and M2 for the same week, so it takes their inclusions and exclusions. The channel filter does not apply, because orders carry no channel.
- Unit, rounding and grain: USD; to two decimals; week.
- Better when: lower.
- Source: ads_export.csv (spend, week_start); orders_export.csv (order_id, order_date, status).
- When the data is missing: "no data" if M1 has no data for the week; "no orders" if M2 has none.

M4 Days of stock left. Status: AS SUPPLIED. Open questions: 2, 3, 8.
- Meaning: How long stock on hand lasts at the recent selling pace.
- Formula: on_hand / (units sold in the last 28 days / 28). Read in the columns supplied: on_hand in stock_export.csv for the sku; units sold is the sum of quantity in orders_export.csv for order lines whose product_sku equals that sku.
- Includes and excludes: on_hand from the latest snapshot_date. The supplied formula does not say which 28 days (Question 3) and does not mention status, although status is among the columns supplied (Question 2).
- Unit, rounding and grain: days; rounded down to whole days; product (one row per product in stock_export.csv, identified by sku).
- Better when: higher.
- Source: stock_export.csv (sku, on_hand, snapshot_date); orders_export.csv (product_sku, quantity, order_date, status).
- When the data is missing: "no sales in the window" where the product sold nothing; "no stock row" for a product_sku that has no row in the stock export.

M5 Free-shipping share of orders. Status: AS SUPPLIED. Open questions: 2, 4.
- Meaning: Share of orders where the customer paid no shipping.
- Formula: orders with shipping_charged of 0 / all orders
- Includes and excludes: orders are read as different order_id values, because the export has one row per order line; in the month of order_date. The supplied formula says "all orders" and does not mention status (Question 2). Whether shipping_charged sits on every line of an order or on one is Question 4.
- Unit, rounding and grain: percent; one decimal; month.
- Better when: neither.
- Source: orders_export.csv; order_id, shipping_charged, order_date, status.
- When the data is missing: "no orders".

M8 Average order value. Status: AS SUPPLIED. Open questions: 2, 5.
- Meaning: Average amount per order.
- Formula: sum of line_total / number of orders
- Includes and excludes: line_total summed over the lines with order_date in the month; orders read as different order_id values. The supplied formula does not mention status (Question 2). Whether line_total is before or after the discount column is Question 5.
- Unit, rounding and grain: USD; to two decimals; month.
- Better when: higher.
- Source: orders_export.csv; order_id, line_total, order_date, status.
- When the data is missing: "no orders".

4. FILTERS
Week range: week_start in ads_export.csv and order_date in orders_export.csv. Applies to M1, M2, M3. Not applied to M4: it uses the latest stock snapshot. Not applied to M5 and M8: they have the month filter. Default: [latest full week] beside [week before].
Month: order_date in orders_export.csv. Applies to M5, M8. Not applied to M1, M2, M3, M4: they are not monthly. Default: [latest full month] beside [month before].
Ad channel: channel in ads_export.csv. Applies to M1. Not applied to M2, M3, M4, M5, M8: orders and stock carry no channel, so for M3 spend for one channel divided by all orders would change what it means, and for the rest there is no channel to filter on. Default: all channels.
Product: sku in stock_export.csv. Applies to M4. Not applied to M1, M3: ad spend is not held by product. Not applied to M2, M5, M8: orders are counted once, not once per product. Default: all products.
Asked for and not possible: customer region, because no export has a region column.

5. SOURCE NOTES
orders_export.csv: holds order lines from the online shop; one row per order line; dates 4 May 2026 to 1 November 2026; extracted 2 November 2026, 1 day before this brief; 4312 rows; owner the operations lead. Columns: order_id, order_date, status, product_sku, quantity, line_total, shipping_charged, discount. Age check: fresh, against 7 days (weekly).
ads_export.csv: holds weekly ad spend by channel; one row per week and channel; dates 4 May 2026 to 19 October 2026 (the last week starts 19 October 2026); extracted 26 October 2026, 8 days before this brief; 50 rows; owner the owner. Columns: week_start, channel, spend, clicks. Age check: stale, against 7 days (weekly).
stock_export.csv: holds stock on hand by product; one row per product; dates 2 November 2026 to 2 November 2026; extracted 2 November 2026, 1 day before this brief; 38 rows; owner the operations lead. Columns: sku, product_name, on_hand, snapshot_date. Age check: fresh, against 7 days (weekly).
Joins: orders_export.csv product_sku to stock_export.csv sku, used by M4; the operations lead confirms that every product_sku sold appears as a sku in the stock export, and what is shown for any that does not (Question 8).

6. REFRESH
Owner: the operations lead. When: every Monday by 9:30. Steps: 1. Get each export again. 2. Replace the old export in the spreadsheet. 3. Compare the dates with the source notes. 4. Tell the owner the view is ready. Check after each refresh: each export's last date is later than the last date in the source notes. Cover: not supplied. No live connection is built; the numbers change only when the exports are replaced.

7. LEFT OFF
M6 Daily ad spend: ads_export.csv holds one row per week and channel, so spend cannot be shown by day.
M7 Website sessions: no decision is attached to it and no source is named.

8. CHECKS ON THE INPUTS
- Which day a week starts is not stated for the ads export or the orders export (Question 1).
- The wording of a cancelled status is not on any sheet, and the supplied meanings and formulas of M4, M5 and M8 do not mention cancelled orders (Question 2).
- M4's formula does not say which 28 days (Question 3).
- M5 reads shipping_charged, and M8 reads line_total, on an export with one row per order line (Questions 4 and 5).
- Customer region has no column in any export (Question 6).
- ads_export.csv is 8 days old against a weekly cadence (Question 7).
- M4 joins on product_sku and sku, which have different names (Question 8).
- No cover is named for the refresh (Question 9).
- M2 had no formula; the one proposed leaves out cancelled lines, whose status wording is not supplied (Question 2).
- M6 and M7 are left off (see section 7).

9. QUESTIONS FOR THE REQUESTER
1. M1 and M2 are matched by week. The first and last week_start dates in ads_export.csv, 4 May 2026 and 19 October 2026, both fall on a Monday. orders_export.csv has only order_date. Which day does a week start, and should orders be grouped into weeks that start on that day?
2. M2's meaning leaves out cancelled orders, and the proposed formula does the same. The supplied meanings and formulas of M4, M5 and M8 do not mention cancelled orders, although each lists status among its columns. Should M4, M5 and M8 leave out cancelled lines too, and which values of status mean cancelled?
3. M4's formula says "units sold in the last 28 days". The orders export runs to 1 November 2026 and the stock snapshot is dated 2 November 2026. Which 28 days are meant?
4. M5 counts orders by shipping_charged, and the export has one row per order line. Does shipping_charged appear on every line of an order, or on one line only?
5. M8 adds line_total. The export also has a discount column. Is line_total before or after the discount?
6. Customer region was asked for and no export holds it. Do you want a region column added to the order export, or should the filter be dropped?
7. ads_export.csv was pulled on 26 October 2026 and does not include the week starting 26 October 2026. Can a fresh extract be supplied before the build?
8. M4 joins orders to stock on product_sku and sku. Does every product_sku sold appear in the stock export, and what should be shown for one that does not? The brief shows "no stock row".
9. No cover is named for the Monday refresh. Who refreshes it when the operations lead is away?
10. M6 Daily ad spend cannot be built from a weekly export. Do you want a daily ad export, or should M6 be dropped?
11. M7 Website sessions has no decision and no source. Which decision does it serve, and from which export, or should it be dropped?

10. APPROVALS
[ ] The owner approves what is shown (section 2) and the definitions (section 3). Name and date: ______
[ ] The operations lead confirms the source notes (section 5) and the calculations against the data for orders_export.csv and stock_export.csv. Name and date: ______
[ ] The owner confirms the source notes (section 5) and the calculations against the data for ads_export.csv. Name and date: ______
[ ] The operations lead accepts the refresh (section 6). Name and date: ______
Nothing is built until the first box is ticked by a person.

This brief was prepared on 3 November 2026 from the inputs supplied. It builds no connection, contains no figures and changes no file or record.
```
