# Dashboard brief: a trial on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10
- **Template version:** 0.1.0

This is a record of one run of the capability template on its own invented example. The shop, the people, the files, the dates and the counts are invented, and no client data was used. It shows what the template produced once, on one set of inputs. It is not a test in any company's environment.

This is the second run on the same example, made the same day. The first run showed where the instructions left room to guess; the instructions, the output format and the example's output were revised, and the run recorded here was made on the revised instructions. The example's inputs did not change. What the first run found, and what was changed, is at the end.

The inputs were the invented example for Tern Hollow Candles: the requester's notes, the decision sheet, the metric list and the source sheet, as printed in `public/example.md` under "What the person supplies". The preparation date was 3 November 2026. The pasted instruction block and the output format were followed as written, and nothing else was added. The assistant built nothing and was given no settings, so the defaults applied.

## What came out

The full brief, as produced. It is the output shown in `public/example.md` as first published. After the independent review, three lines of the example were corrected by hand and are not reproduced here as run: the Ad channel and Product filter lines (the run named too few metrics under "Not applied to"), the Checks line for M2 (it pointed to section 3 and no question), and a sentence in the ads export's source note that was an inference. The recorded output below is as the run produced it.

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
Ad channel: channel in ads_export.csv. Applies to M1. Not applied to M3: orders carry no channel, so spend for one channel divided by all orders would change what M3 means. Default: all channels.
Product: sku in stock_export.csv. Applies to M4. Not applied to M2, M5, M8: orders are counted once, not once per product. Default: all products.
Asked for and not possible: customer region, because no export has a region column.

5. SOURCE NOTES
orders_export.csv: holds order lines from the online shop; one row per order line; dates 4 May 2026 to 1 November 2026; extracted 2 November 2026, 1 day before this brief; 4312 rows; owner the operations lead. Columns: order_id, order_date, status, product_sku, quantity, line_total, shipping_charged, discount. Age check: fresh, against 7 days (weekly).
ads_export.csv: holds weekly ad spend by channel; one row per week and channel; dates 4 May 2026 to 19 October 2026 (the last week starts 19 October 2026); extracted 26 October 2026, 8 days before this brief; 50 rows; owner the owner. Columns: week_start, channel, spend, clicks. Age check: stale, against 7 days (weekly). The week starting 26 October 2026 is not in it.
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
- M2 had no formula; one is proposed (section 3).
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

## What was observed

- **Every required part was produced.** All ten sections are present, in the order and wording of the output format, with the closing line. No stop condition applied: the headers matched, every named file and column was on the source sheet, every date was real, and there were three decisions, six metrics on the page and four filters offered, all within the defaults.
- **Nothing in the output is a figure that is not an input.** The numbers are counts and dates from the inputs (4312, 50 and 38 rows, the extract dates), the two day counts worked out from them (1 day and 8 days), the page count (6 of 10) and the calendar fact, stated as such in Question 1, that two week_start dates fall on a Monday. Every layout line uses placeholders in square brackets.
- **Supplied formulas were kept word for word.** M4, M5 and M8 keep their supplied formulas with nothing added. The 28-day window and the cancelled-order exclusion, which the inputs do not state for those three metrics, became Questions 3 and 2. M2, which had no formula, is PROPOSED and leaves out cancelled lines, as its supplied meaning says. M3 is AS SUPPLIED and says it rests on M2, PROPOSED.
- **M4's item grain was kept.** Its grain is product, the stock export has one row per product, and the brief names sku as the identifying column.
- **Left off:** M6 (day grain on a weekly export) and M7 (no decision, no source). The ads export was flagged stale (8 days against 7). The customer region filter is listed as not possible.
- **Approvals:** four lines, one for the requester, one for each of the two export owners (the operations lead for orders and stock, the owner for ads) and one for the refresh owner.
- **Questions** are in section order (11 of them), and every line under Checks names its question or points to Left off, except the line about M2, which pointed to section 3 (corrected in the example afterwards to name Question 2).
- **Where the template still leaves a choice.**
  - Counting "orders" as different order_id values on an export with one row per order line is the brief's reading of a word in the supplied formulas of M5 and M8. The instructions allow it but do not require it; it is stated in the brief and tied to Question 4.
  - The form for each metric came from the default in step 7 (number with the prior period beside it, table by item for an item grain). A requester who wants a trend line has to say so.
  - The missing-data wording for M4 was changed to "no sales in the window", because the window itself is Question 3.
- **Shortcomings of this trial.** One run, by one model, on one invented example. The run was not blind: the same session had read the example's earlier output and the first run's record before it wrote this brief, so agreement with the example is not independent evidence, and this brief is also the published example. The first run was likewise not fully blind, because part of the example's earlier output was shown alongside the inputs. The template's acceptance tests were not run, and the template has not been tried in ChatGPT, Copilot or Gemini.

## What the first run found, and what was changed

The first run, using the instructions as first written, found these. Each led to a change in the instruction block, the output format or the example, listed here; the revised instructions were then run once, which is the run recorded above.

- The example had marked M4, M5 and M8 AS SUPPLIED while adding a fixed 28-day window and a cancelled-order exclusion their supplied formulas did not state, and had stated the ads weeks start on Mondays as a fact. The instructions now require a supplied formula word for word, with gaps raised as questions, and the example follows.
- M4's grain was "product", which is not a column in any export, and the grain rule would have left it off. A grain may now name the item a source's rows describe, with the identifying column named.
- The ads export belongs to the owner but only the operations lead was asked to confirm the sources. There is now one confirmation line for each export owner.
- The refresh check was two checks, with "by a week" that need not hold. It is now one comparison.
- Further edits made from the first run: the choice among the three forms; the status of a supplied formula that rests on a PROPOSED metric; all dates written in words; lines under Checks must name a question or point to Left off; the pasted block now carries the rounding defaults, the item-grain rule, the rule for a metric built on another metric and the question about two metrics with the same formula; "the finer of the two cadences" was replaced by a check against both grains.
