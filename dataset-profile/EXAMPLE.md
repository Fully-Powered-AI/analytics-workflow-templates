# Dataset profile: an invented example

*Illustrative example with invented data.* The company, the file, the people and every row below are invented. The company is an invented online homeware shop, called Shop M here. Its analyst has received a month of order lines from the shop's order system and wants to join them to a returns table. First come the inputs the analyst supplied, in full, then the profile the capability returned.

## The inputs

### 1. Settings (typed by the analyst)

```
File: order_lines_oct2026.csv (the full October export, not a sample)
Today: Tuesday 10 November 2026
Intended use: join to the returns table on order_id and sku, to look at returns by channel
Expected key: order_id + line_no (one row per order line)
Join key: order_id + sku
Expected period: order_date from 1 October 2026 to 31 October 2026
Far-out rule: more than 10 times the column median
Personal-data columns: none
Data owner: Operations lead
Identifier column: order_id
Consistency rules: ship_date on or after order_date
```

### 2. Schema notes (one line per column)

```
column,meaning,type,allowed
order_id,Order number,whole number,
line_no,Position of the line within the order,whole number,1 or more
order_date,Date the order was placed,date YYYY-MM-DD,
sku,Product code,text,
qty,Units ordered,whole number,1 or more
unit_price,Price per unit in USD,number,0 or more
line_total,qty times unit_price in USD,number,
country,Ship-to country,two-letter code,US or CA or GB
channel,Where the order was placed,text,web or market
ship_date,Date the line was shipped,date YYYY-MM-DD,filled for every line
```

### 3. The extract: order_lines_oct2026.csv (header is line 1)

```
order_id,line_no,order_date,sku,qty,unit_price,line_total,country,channel,ship_date
5001,1,2026-10-01,SKU-100,2,12.50,25.00,US,web,2026-10-03
5001,2,2026-10-01,SKU-205,1,40.00,40.00,US,web,2026-10-03
5002,1,2026-10-02,SKU-100,1,12.50,12.50,CA,web,2026-10-05
5003,1,2026-10-02,SKU-310,3,8.00,24.00,US,market,2026-10-04
5004,1,2026-10-03,SKU-205,1,40.00,40.00,US,web,2026-10-06
5004,2,2026-10-03,SKU-100,4,12.50,50.00,US,web,2026-10-06
5005,1,10/04/2026,SKU-310,2,8.00,16.00,US,Web,2026-10-07
5006,1,2026-10-05,SKU-205,1,40.00,40.00,GB,web,2026-10-09
5006,1,2026-10-05,SKU-205,1,40.00,40.00,GB,web,2026-10-09
5007,1,2026-10-06,SKU-410,2,19.00,38.00,US,market,
5008,1,2026-10-06,SKU-100,1,12.50,12.50,US,web,2026-10-08
5008,2,2026-10-06,SKU-310,1,8.00,8.00,US,web,2026-10-08
5009,1,2026-10-07,SKU-205,2,40.00,80.00,CA,web,2026-10-10
5010,1,2026-10-08,SKU-410,1,19.00,19.00,,web,2026-10-11
5011,1,2026-10-09,SKU-100,3,12.50,37.50,US,web,2026-10-12
5011,2,2026-10-09,SKU-310,1,8.00,9.00,US,web,2026-10-12
5012,1,2026-10-10,SKU-205,1,40.00,40.00,US,market,2026-10-08
5013,1,2026-10-12,SKU-100,500,12.50,6250.00,US,web,2026-10-14
5014,1,2026-10-13,SKU-410,1,19.00,19.00,US,web,2026-10-16
5015,1,2026-10-14,SKU-310,2,8.00,16.00,N/A,web,2026-10-17
5016,1,2026-10-15,SKU-205,-1,40.00,-40.00,US,web,2026-10-15
5017,1,2026-09-30,SKU-100,2,12.50,25.00,US,web,2026-10-02
5018,1,2026-10-20,SKU-410,1,19.00,19.00,US,web,2026-10-23
5004,2,2026-10-03,SKU-310,2,8.00,16.00,US,web,2026-10-06
```

## The profile

```
DATASET PROFILE: order_lines_oct2026.csv

For: the analyst. Prepared 10 November 2026 from the settings, schema notes and extract supplied. Intended use: join to the returns table on order_id and sku, to look at returns by channel.

1. THE FILE
Header check: the 10 headers match the 10 columns in the schema notes, in the same order. 24 data rows, 10 columns; every row has 10 fields. Full export, as stated; the figures describe the rows supplied.

2. ROW GRAIN
Expected: one row per order line, key order_id + line_no. 22 distinct keys among 24 rows. The grain does not hold: 2 keys appear more than once (5004 / 2 on lines 7 and 25; 5006 / 1 on lines 9 and 10).
Identifier order_id: 18 distinct values.
Join key order_id + sku: 23 distinct among 24 rows. 1 repeat: 5006 / SKU-205 on lines 9 and 10.

3. DUPLICATES
Identical rows: 1 pair, lines 9 and 10 (order 5006, line 1).
Same key, different values: 5004 / 2 on lines 7 and 25. They differ in sku (SKU-100, SKU-310), qty (4, 2), unit_price (12.50, 8.00) and line_total (50.00, 16.00); they agree in order_id, line_no, order_date, country, channel and ship_date.

4. MISSING AND STAND-IN VALUES
country: 1 blank (line 15); 1 stand-in, "N/A" (line 21). 22 of 24 rows hold a value.
ship_date: 1 blank (line 11). 23 of 24 rows hold a value. The notes say it is filled for every line.
No blank or stand-in values in order_id, line_no, order_date, sku, qty, unit_price, line_total, channel.

5. TYPES AND FORMATS
order_date: 23 of 24 values are YYYY-MM-DD. Line 8 reads 10/04/2026, which is either 4 October 2026 or 10 April 2026; it is left unread.
channel: "Web" on line 8 differs from "web" only in capitalisation.
country: apart from the blank and the "N/A" above, every value is a two-letter code.
order_id, line_no, qty: whole numbers throughout. unit_price, line_total: plain numbers throughout, no symbols. sku: "SKU-" and three digits throughout. ship_date: all 23 filled values are YYYY-MM-DD. No leading or trailing spaces found in any column.

6. VALUES AND SPREADS
line_no: min 1, median 1, max 2. 0 negative; 0 zero. Far-out (above 10): none.
qty: min -1, median 1, max 500. 1 negative (line 22); 0 zero. Far-out (above 10): line 19 (500).
unit_price: min 8.00, median 12.50, max 40.00. 0 negative; 0 zero. Far-out (above 125.00): none.
line_total: min -40.00, median 24.50, max 6250.00. 1 negative (line 22); 0 zero. Far-out (above 245.00): line 19 (6250.00).
order_date (23 readable): earliest 2026-09-30, latest 2026-10-20. Outside 1 to 31 October 2026: line 23 (2026-09-30). After 10 November 2026: none. Line 8 falls inside the period if read as 4 October and outside it if read as 10 April.
ship_date (23 readable): earliest 2026-10-02, latest 2026-10-23. After 10 November 2026: none.
sku (4 distinct): SKU-100 7, SKU-205 7, SKU-310 6, SKU-410 4. Outside the allowed list: no list given. Values seen once: none.
country (4 distinct, counting "N/A" and not the blank): US 18, CA 2, GB 2, N/A 1; plus 1 blank. Outside the allowed list (US, CA, GB): lines 15 and 21. Values seen once: "N/A" (line 21).
channel (3 distinct as written): web 20, market 3, Web 1. Outside the allowed list (web, market): line 8 ("Web"). Values seen once: "Web" (line 8). With capitals ignored: web 21, market 3.

7. CONSISTENCY RULES AND ALLOWED VALUES
ship_date on or after order_date (rule given by the analyst): 22 tested, 21 pass. Fail: line 18 (5012): ship_date 2026-10-08 is before order_date 2026-10-10. Left out: line 8 (order_date unread) and line 11 (no ship_date).
line_total = qty x unit_price (defined in the notes): 24 tested, 23 pass. Fail: line 17 (5011 / 2): 1 x 8.00 = 8.00, but line_total is 9.00. Left out: none.
Allowed values in the notes, one line per column that has a limit or list:
line_no, 1 or more: 24 tested, 24 pass. Not passing: none.
qty, 1 or more: 24 tested, 23 pass. Not passing: line 22 (-1).
unit_price, 0 or more: 24 tested, 24 pass. Not passing: none.
country, US or CA or GB: 24 tested, 22 pass. Not passing: line 15 (blank), line 21 ("N/A").
channel, web or market: 24 tested, 23 pass. Not passing: line 8 ("Web").
ship_date, filled for every line: 24 tested, 23 pass. Not passing: line 11 (blank).

8. WHAT THE FINDINGS TOUCH FOR THE INTENDED USE
The intended use reads order_id, sku and channel for the join and the grouping, and order_date for the period.
Join key order_id + sku: two rows carry the key 5006 / SKU-205 (lines 9 and 10). Any returns row with that key would match both of them; the file does not show whether the returns table holds such a row. Order 5004 has two rows keyed line 2 with different skus (lines 7 and 25); under order_id + sku they are distinct keys (5004 / SKU-100 and 5004 / SKU-310), while under order_id + line_no they collide.
Grouping by channel: line 8 ("Web") would form a separate group from "web" unless the grouping ignores capitals.
Period: line 23 is dated 30 September; line 8's date is unresolved.
Columns the intended use does not read (qty, unit_price, line_total, country, ship_date): the findings on lines 11, 15, 17, 19, 21 and 22 sit on those columns, and line 18 has a ship_date before its order_date.

9. QUESTIONS FOR THE DATA OWNER (Operations lead)
1. Lines 9 and 10 are identical in every field (order 5006, line 1, SKU-205, qty 1, 40.00). Does the export list this order line twice, or were two identical lines recorded?
2. Order 5004 has two rows keyed as line 2: line 7 (SKU-100, qty 4, 50.00) and line 25 (SKU-310, qty 2, 16.00). Which is line 2 of the order, or does one belong to a different line number?
3. Line 8 (order 5005) has order_date 10/04/2026. Which date is meant, and does the export write dates this way anywhere else?
4. Line 8 has channel "Web" where every other web order has "web". Is it the same channel?
5. Line 23 (order 5017) has order_date 2026-09-30 in an export described as October. Why is it included?
6. Line 11 (order 5007, ordered 2026-10-06) has no ship_date, and the notes say it is filled for every line. Has it shipped?
7. Country is blank on line 15 (order 5010) and "N/A" on line 21 (order 5015). What do they mean?
8. Line 17 (order 5011, line 2): line_total is 9.00 where 1 x 8.00 is 8.00. Which figure is the recorded one?
9. Line 18 (order 5012): ship_date 2026-10-08 is two days before order_date 2026-10-10. Are both dates as recorded?
10. Line 19 (order 5013): qty 500 of SKU-100, line_total 6250.00, where the median quantity is 1. What was this order?
11. Line 22 (order 5016): qty -1 and line_total -40.00. What does a negative line stand for?

10. DECISIONS FOR THE ANALYST
1. The repeated keys (lines 7, 9, 10, 25): keep all rows as supplied, hold the affected rows out of the join, correct at source, or wait for answers 1 and 2.
2. The row outside the period (line 23) and the unread date (line 8): keep as supplied, hold out of the period, or wait for answers 3 and 5.
3. The "Web" spelling (line 8): keep as its own group as supplied, or wait for answer 4.
4. Rows that break a rule or the allowed values (lines 17, 18, 19, 22) and the blank and stand-in values (lines 11, 15, 21): keep as supplied, hold out of any figure that uses the field, correct at source, or wait for answers 6 to 11.
Whether the data is usable is the analyst's decision.

11. NOT CHECKED
Whether the values are true to the shop's real orders; whether any order lines are missing from the export; any other table, including the returns table; the meaning of any column beyond the schema notes. No row has been changed, removed or corrected.

Every figure counts the 24 data rows of order_lines_oct2026.csv as supplied on 10 November 2026. This profile changes no data and states no conclusion about the business.
```
