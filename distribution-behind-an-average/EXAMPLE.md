# The distribution behind an average: an invented example

*Illustrative example with invented data.* The company, the export, the roles and every row below are invented. The company is an invented software company, called Company K here, with a support desk of four queues. Its support analyst is preparing the October service review, where the headline figure has always been the average time to resolve a ticket. First come the inputs the analyst supplied, in full, then the page the workflow template returned.

## The inputs

### 1. Settings (typed by the analyst)

```
File: resolution_times_oct2026.csv
Today: Wednesday 11 November 2026
Measure: hours to resolve, in hours
Population: every support ticket closed in October 2026, one row per ticket
Window: 2026-10-01 to 2026-10-31
Columns: record_id = ticket_id; segment = queue; recorded_on = closed_on; measure = hours_to_resolve
Segments: yes
Target: 24 hours
Extreme cut: P90 (default)
Minimum segment size: 5 (default)
Combine: none
Analyst: support analyst
Analytics owner: head of analytics
Process owner: support operations lead
```

### 2. The export: resolution_times_oct2026.csv (header is line 1)

```
ticket_id,queue,closed_on,hours_to_resolve
4101,Billing,2026-10-01,18.0
4102,Billing,2026-10-01,5.5
4103,Technical,2026-10-02,16.5
4104,Returns,2026-10-03,52.0
4105,Returns,2026-10-03,36.0
4106,Billing,2026-10-04,30.0
4107,Billing,2026-10-05,9.0
4108,Billing,2026-10-05,22.0
4109,Billing,2026-10-06,10.5
4110,Billing,2026-09-30,4.0
4111,Account,2026-10-07,9.0
4112,Account,2026-10-08,12.5
4113,Technical,2026-10-09,22.0
4114,Billing,2026-10-10,7.0
4115,Billing,2026-10-10,2.5
4116,Technical,2026-10-11,8.5
4117,Account,2026-10-12,5.0
4118,Billing,2026-10-12,12.0
4119,Technical,2026-10-13,14.0
4120,Returns,2026-10-14,24.0
4121,Account,2026-10-14,3.5
4122,Technical,2026-10-15,6.0
4123,Technical,2026-10-16,96.0
4124,Technical,2026-10-17,38.0
4125,Billing,2026-10-17,0.0
4126,Technical,2026-10-18,31.0
4127,Billing,2026-10-19,6.5
4128,Technical,2026-10-19,
4129,Technical,2026-10-20,62.0
4130,Technical,2026-10-21,47.0
4131,Technical,2026-10-21,140.0
4132,Billing,2026-10-22,4.0
4133,Billing,2026-10-23,3.0
4134,Billing,2026-10-24,14.0
4135,Account,2026-10-24,20.0
4136,Technical,2026-10-25,19.0
4137,Billing,2026-10-26,6.0
4138,Account,2026-10-26,7.5
4139,Billing,2026-10-27,5.0
4140,Billing,2026-10-28,4.5
4126,Technical,2026-10-28,26.0
4142,Billing,2026-10-29,8.0
4143,Technical,2026-10-30,11.0
```

## The page

```
DISTRIBUTION VIEW: hours to resolve (hours), 2026-10-01 to 2026-10-31

For: support analyst. Prepared Wednesday 11 November 2026 from the settings and the export resolution_times_oct2026.csv. Population: every support ticket closed in October 2026, one row per ticket. Analytics owner: head of analytics. Process owner: support operations lead.
Method: nearest rank, on the counted values sorted from smallest to largest.
Pk is the value at position k x n / 100, rounded up.
A percentile at the last position is not shown.
Means, differences and percentages to one decimal place; ratios to two.

1. THE EXPORT
Header check: all four columns found, as mapped in the settings: record_id is ticket_id, segment is queue, recorded_on is closed_on, measure is hours_to_resolve. Other columns, ignored: none.
43 data rows supplied; 41 counted. Not counted: line 11, 4110, outside the window (closed_on 2026-09-30); line 29, 4128, measure blank.

2. THE WHOLE POPULATION
Count 41. Mean 21.3. Min 0.0. P25 6.0. P50 12.0. P75 24.0. P90 47.0. P95 62.0. Max 140.0.
Over target (24 hours): 10 of 41 (24.4%).
What the average leaves out: the mean is 21.3 and P50 is 12.0. 13 of 41 records (31.7%) sit above the mean. The largest 5 records (10% of the count, rounded up) hold 397.0 of 874.0 hours (45.4%). P90 is 3.92 times P50.

3. BY SEGMENT (queue)
Billing: count 18. Mean 9.3. Min 0.0. P25 4.5. P50 6.5. P75 12.0. P90 22.0. P95 not shown (n under 20). Max 30.0. Over target 1 of 18 (5.6%).
Technical: count 14. Mean 38.4. Min 6.0. P25 14.0. P50 22.0. P75 47.0. P90 96.0. P95 not shown (n under 20). Max 140.0. Over target 7 of 14 (50.0%).
Account: count 6. Mean 9.6. Min 3.5. P25 5.0. P50 7.5. P75 12.5. P90 not shown (n under 10). P95 not shown (n under 20). Max 20.0. Over target 0 of 6 (0.0%).
Returns (under 5): count 3. Min 24.0. Max 52.0. Over target 2 of 3.

4. SEGMENT DIFFERENCES
Billing: 43.9% of counted records; 0 of 4 extreme cases (0.0%). P50 -5.5 against the whole. P90 -25.0. P90 is 3.38 times P50. Over target 5.6% against 24.4% for the whole.
Technical: 34.1% of counted records; 3 of 4 extreme cases (75.0%). P50 +10.0 against the whole. P90 +49.0. P90 is 4.36 times P50. Over target 50.0% against 24.4% for the whole.
Account: 14.6% of counted records; 0 of 4 extreme cases (0.0%). P50 -4.5 against the whole. P90 not compared. P90 to P50 ratio not shown. Over target 0.0% against 24.4% for the whole.
Returns (under 5): 7.3% of counted records; 1 of 4 extreme cases (25.0%). Over target 2 of 3.
Percentages are rounded and may not add to 100. Differences are described, not tested.

5. EXTREME CASES (above P90, 47.0)
1. Line 32, 4131, Technical, 2026-10-21: 140.0. far out
2. Line 24, 4123, Technical, 2026-10-16: 96.0. far out
3. Line 30, 4129, Technical, 2026-10-20: 62.0.
4. Line 5, 4104, Returns, 2026-10-03: 52.0.
Far out means above P75 + 3 x (P75 - P25) = 24.0 + 3 x (24.0 - 6.0) = 78.0. Every extreme case is kept in every figure.

6. RECORDS TO CHECK
Zero or negative values: line 26, 4125, Billing, 0.0.
Record ids on more than one counted line: 4126 on lines 27 and 42, values 31.0 and 26.0.
These records are counted as supplied.

7. FOR THE ANALYTICS OWNER TO CONFIRM (head of analytics)
1. Line 11, ticket 4110 (Billing, 4.0 hours) was closed on 2026-09-30, outside the window, and is not counted. Should it stay out of October?
2. Line 29, ticket 4128 (Technical, closed 2026-10-19) has no hours_to_resolve and is not counted. What is its resolution time?
3. Line 26, ticket 4125 (Billing, closed 2026-10-17) shows 0.0 hours and is counted. Is zero a time the system really records for a resolved ticket?
4. Ticket 4126 (Technical) is on line 27 (closed 2026-10-18, 31.0 hours) and line 42 (closed 2026-10-28, 26.0 hours), and both are counted, while the population is one row per ticket. Is it one ticket listed twice, or a ticket closed twice?
5. Returns has 3 counted records, under the minimum of 5, so it shows count, minimum, maximum and over target only. Report it alone again, or name it in a Combine line next time?
6. Method: nearest rank. A spreadsheet function that interpolates between values may give a different P-value.

8. FOR THE PROCESS OWNER TO DECIDE (support operations lead)
1. The four extreme cases, lines 32, 24, 30 and 5, are above 47.0 hours; two of them (140.0 and 96.0) are far out. Look into the records named, compare with another period, or take no action.
2. Billing: P90 22.0 against 47.0 for the whole, a gap of 25.0, more than half of 47.0; 1 of 18 over target, none of the extreme cases. Compare with another period, run a comparison test, or take no action.
3. Technical: P50 22.0 against 12.0 for the whole, a gap of 10.0, more than half of 12.0; P90 96.0 against 47.0, a gap of 49.0, more than half of 47.0; 7 of 14 over target, 3 of the 4 extreme cases. Compare with another period, run a comparison test, or take no action.
4. The target of 24 hours: 10 of 41 records (24.4%) are over it, while the mean of 21.3 is under it. Compare with another period, or take no action.
Which follow-up, if any, is the process owner's decision.

9. NOT SHOWN
The cause of any value or difference. Whether any difference would hold in another period (no test was run). Whether every row belongs to the population as defined. Whether every value is in the stated unit. Records missing from the export.

Every figure is computed from the 41 counted rows of resolution_times_oct2026.csv as supplied on Wednesday 11 November 2026. This view changes no data and states no cause.
```
