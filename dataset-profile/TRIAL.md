# Dataset profile: tried twice on its own example

- **Product:** Claude, run in Claude Code
- **Model:** Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

This record covers two runs of the capability template on its own invented example, both on 10 November 2026. The inputs are the invented ones in [the example](example.md): the settings, the schema notes and the extract `order_lines_oct2026.csv` for the invented shop called Shop M. No client data was used. A short script recomputed the counts, medians and line numbers from the extract in both runs, as the template tells the assistant to recompute every figure.

## First run, and what it found

The first run was done by an assistant that did not write the template. It followed the instruction block and the output format. Its profile agreed with the example in every count and line number but one. The example had reported line 18 (order 5012, shipped 2026-10-08 before it was ordered on 2026-10-10) as a failed rule. The first run did not, because the template tests a date pair only when the analyst lists the rule or the notes say one date comes first, and neither did. So the instruction block and the example disagreed, and a person following the block would have missed a plain error. The first run also listed nine places where the instructions were ambiguous: no Analyst setting although the format prints one; an "identifier" column the settings never name; which numeric columns get a spread; whether a stand-in counts as a distinct value; the allowed-values check placed in step 6 in the procedure and in section 7 in the format; whether allowed lists are case-sensitive; how an unreadable date is treated in a date-pair rule; whether decision options that do not fit may be dropped; and the defaults (the far-out rule, the cap of ten line numbers, candidate keys of up to three columns) missing from the pasted instruction block. Its output is not reproduced here, because the template and the example were changed in answer to it.

## Edits made after the first run

- The example now follows the template. The analyst's settings list the rule "ship_date on or after order_date" and name order_id as the identifier column, so line 18 is tested because a rule was given. The template still does not test a date order that nobody stated; test 11 and 12 were added for both cases.
- The template gained an Analyst setting and an Identifier column setting, both optional with defaults; the allowed-values check moved into step 7 to match the output format; spreads are given for every number column except the identifier; allowed lists are compared exactly as written; a row with a blank or unread date is left out of a date-order test and listed; options that do not fit a decision may be left out; a stand-in counts as a distinct value and a blank does not.
- The instruction block now carries the defaults it lacked.
- In the example, the profile's section 8 no longer says a returns row would be matched twice as a fact about the returns table, and no longer says which sku a returns row would match; it states what the join key does and that the file does not show the returns table. Section 7 uses "tested / pass / Left out", section 6 gives the after-today result for every date column, the outside-the-list and seen-once results for every category column and the far-out threshold for every number column, and the order_date line of section 6 states its after-today result.

## Second run

The second run was done on the edited template by the assistant that made the edits, so it is not an independent run. It followed the revised instruction block and output format on the inputs now in the example (the same extract, with the two new settings). The profile it produced is the one published in the example.

### Inputs used

The three inputs in the example, by reference: (1) the settings, now including the identifier column and the consistency rule, (2) the ten-column schema notes, (3) the 24-row extract with its header as line 1. No stand-in values were added beyond the defaults.

### What came out

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

### What was observed

Every required part was produced: all eleven sections, with the trace line. Nothing triggered a stop: the headers matched in name and order, every row had ten fields, the schema notes and expected key were supplied, and no column was marked as personal data. The script recheck gave the same counts, medians and line numbers as the first run, and the date-order rule tested 22 lines, with line 8 (unreadable order_date) and line 11 (blank ship_date) left out, and failed line 18. Line 18 now appears in section 7, in question 9 and in decision 4 because the analyst supplied the rule, not because the template assumed it.

The second run has a limit that the first did not: the assistant that ran it also wrote the changes, and it knew the output it was aiming for. It shows that the revised block can be followed to this profile, not that a stranger would reach the same one. It was not run again by an independent reader. The wording of some resolved ambiguities (for example, that a stand-in counts as a distinct value) was settled by the editing assistant's choice, and the template now states those choices rather than leaving them open.

Facts in the output that are not in the inputs: none. Section 8 states what the join key does with the rows and says the file does not show the returns table. No outside source was named.

### Where the instructions still needed a guess

1. Which date is the "order date" for a row whose order_date is a slash date that could be read two ways: the rule treats it as unread and leaves the row out, and says so, but the template does not say whether to also test it under each reading. It was left out only.
2. Whether the "Identifier column" may be a key column. Here it is order_id, which is part of the expected key; the template does not say that is unusual.
3. How to group decisions. The template says one numbered line per open choice, and this run grouped related lines into four choices; the grouping is a judgment.

After this record was written, the template was edited to settle guesses 2 and 3 (an identifier column may also be a key column and still gets its own line; findings that call for the same options may share a decision line). The template was not run again after those edits, and they change no figure in the profile above. Questions 7 and 9 in the profile above were also reworded by hand after the run, in the example and here alike. The run produced "and what are the correct codes?" at the end of question 7 and "Which date is recorded wrongly?" as question 9; both were made neutral. Nothing else in the record was altered.

One run on one invented file shows that the revised template can be followed and produces a complete profile. It does not show that the template works on a real extract, on a larger or messier file, or in any other product.
