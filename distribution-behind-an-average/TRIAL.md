# Trial: the distribution behind an average

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (claude-sonnet-5-5)
- **Date:** 2026-11-11

The inputs were the invented example in `public/example.md`: its settings and its export of 43 invented support tickets. No client data was used. The run was one attempt, by a model that did not write the template. The model followed the fenced instruction block and the output format, and used a short script only as a calculator to check percentiles, means and counts against the export. It did not read the example's published page until its own page was finished.

## Inputs used

- The settings block under "The inputs" in `public/example.md` (October 2026 resolution times, 24-hour target, default extreme cut and minimum segment size, no combining).
- The export `resolution_times_oct2026.csv` in the same file, header as line 1.

## What came out

```
DISTRIBUTION VIEW: hours to resolve (hours), 2026-10-01 to 2026-10-31

For: support analyst. Prepared Wednesday 11 November 2026 from the settings and the export resolution_times_oct2026.csv. Population: every support ticket closed in October 2026, one row per ticket. Analytics owner: head of analytics. Process owner: support operations lead.
Method: nearest rank, on the counted values sorted from smallest to largest.
Pk is the value at position k x n / 100, rounded up.
A percentile at the last position is not shown.
Means, differences and percentages to one decimal place; ratios to two.

1. THE EXPORT
Header check: the four columns found, with the export's names: record_id = ticket_id, segment = queue, recorded_on = closed_on, measure = hours_to_resolve. Other columns, ignored: none.
43 data rows supplied; 41 counted. Not counted: line 11, 4110, outside window (2026-09-30); line 29, 4128, measure blank.

2. THE WHOLE POPULATION
Count 41. Mean 21.3. Min 0.0. P25 6.0. P50 12.0. P75 24.0. P90 47.0. P95 62.0. Max 140.0.
Over target (24): 10 of 41 (24.4%).
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
1. Line 11, 4110, Billing, closed 2026-09-30, 4.0 hours: outside the window, not counted. Confirm it belongs outside October.
2. Line 29, 4128, Technical, closed 2026-10-19: measure blank, not counted. Confirm the value, or that none exists.
3. Line 26, 4125, Billing, 0.0 hours: a zero value, counted as supplied. Confirm it is a real time in the stated unit.
4. 4126 on line 27 (Technical, 2026-10-18, 31.0) and line 42 (Technical, 2026-10-28, 26.0): both counted. Confirm whether this is one ticket twice or two tickets.
5. Returns has 3 counted records, under the minimum of 5, so it shows count, minimum, maximum and over target only. Confirm it should be reported alone.
6. Method: nearest rank. A spreadsheet function that interpolates between values may give a different P-value.

8. FOR THE PROCESS OWNER TO DECIDE (support operations lead)
1. The extreme cases as a group (lines 32, 24, 30 and 5; 140.0, 96.0, 62.0 and 52.0 hours, all above 47.0): look into the records named, compare with another period, or take no action.
2. Billing: P90 is 25.0 below the whole's, more than the whole's P50 of 12.0 (P50 is 5.5 below): look into the records named, compare with another period, run a comparison test, or take no action.
3. Technical: P90 is 49.0 above the whole's, more than the whole's P50 of 12.0 (P50 is 10.0 above): look into the records named, compare with another period, run a comparison test, or take no action.
4. The target of 24 hours: 10 of 41 records (24.4%) are over it; 5.6% in Billing and 50.0% in Technical: compare with another period, or take no action.
Which follow-up, if any, is the process owner's decision.

9. NOT SHOWN
The cause of any value or difference. Whether any difference would hold in another period (no test was run). Whether every row belongs to the population as defined. Whether every value is in the stated unit. Records missing from the export.

Every figure is computed from the 41 counted rows of resolution_times_oct2026.csv as supplied on Wednesday 11 November 2026. This view changes no data and states no cause.
```

## What was observed

- **Every required part was produced.** All nine numbered sections, the method lines and the trace line came out in the stated order. Nothing in the template made the run stop: the header check passed through the mapping, no row had the wrong number of fields, and 41 of 43 rows counted.
- **The figures match the published example's page exactly.** Counts, percentiles, means, shares, differences, ratios, the fence, the four extreme cases, the records to check and the four process-owner choices all agree. Only the wording differs.
- **The wording differences are small.** The published page writes the date as "11 November 2026" where the setting reads "Wednesday 11 November 2026" and this run kept it as typed. The published page phrases the analytics owner's points as questions and this run phrased them as "Confirm ..." statements. The published page adds figures to the process owner's choices (for example "3 of the 4 extreme cases") and notes which extreme cases are far out; this run kept to the figures the template names. For Billing the published page offers three options and leaves out "look into the records named"; this run offered four. The published closing line of section 9 says "Tickets missing from the export" and this run used the template's "Records missing from the export".
- **No fact outside the inputs.** Every value, line number, ticket number and date in this run comes from the settings or the export. The published page's "Tickets missing from the export" and its question in point 4 do not add a fact. Neither page mentions that ticket 4141 is absent from the numbering; the template does not ask for that, and the inputs do not say it matters.
- **Where the instructions were open and a guess was needed:**
  - Whether to keep the weekday from the `Today:` setting.
  - What the second number in "[n] of [n] extreme cases" counts. This run read it as all extreme cases above the cut.
  - Whether the analytics owner's points are questions or statements; the template only says each can be answered in a sentence.
  - The rule for the process owner's segment choices sets a threshold in the units of P50 and applies it to the P90 gap as well. Billing is raised only because its P90 is 25.0 below the whole's, against a threshold of 12.0. It reads as intended but is an odd yardstick.
  - The order of the segment choices is not stated. This run followed the segment order from section 3.
  - Whether the target line prints the unit: the format shows "Over target ([target])" and the example prints "24 hours" where this run printed "24".
  - Which neutral options "fit" a given choice is left to the assistant, which is why the published page and this run differ for Billing.
- **One slip during the run.** The first copy of the export taken for the check dropped its last two rows, which gave 39 counted rows and different figures. The mismatch with the count of Technical tickets showed it, the copy was redone from the file, and every figure on the page above comes from the full 43 rows.
- **Shortcomings of the template found:**
  - Its version notes still say "Not yet tried on its invented example", and its acceptance tests are marked as not run. This run covered the example only, not those eleven tests, and none of the decline cases (asking for a cause, for significance, or to drop the 140-hour ticket) was tried.
  - The output is long for a reader: nine sections, and the points and choices repeat figures from the sections above.
  - Percentiles that are printed "as written" depend on how the export writes numbers, so an export of whole numbers would print differently from this one.

## Note added after review

The run above was made on the instructions as they stood that day, and its output and observations are unchanged. After review, the template was edited in these places: the threshold for a segment's choice is now half of the whole's value at the same percentile (P50 against P50, P90 against P90); segment choices follow the order of section 3; "look into the records named" is offered only for the extreme cases as a group, and "run a comparison test" only for a segment choice; the target is printed with its unit; the missing-export stop reads "stop and ask"; and the version notes and profile now say the template was tried on its example. The published example page was brought into line (date as typed, "Records missing from the export", choice order and options). The template has not been run again on the changed instructions, so this record covers the earlier wording only. The figures on the example page are unchanged, and the same segments (Billing and Technical) are raised under the new threshold.

A second round of review edits followed. The instruction block now also states the three reasons a row is not counted, the case where the largest-records share is not shown, the "No extreme cut" case, the wording of the few-records sentence, that only the high end counts as extreme, and that the second number in "[n] of [n] extreme cases" is every counted record above the cut, listed or not (the reading this run used). The profile now says plainly that no row is removed or corrected. No example input or figure changed. The template has still not been run again on the edited wording, and the run above is unchanged.

A third round of review edits followed. The template now says what to print when P75 is not shown (the fence reads "fence not shown" and no record is marked far out), says what happens to a segment choice when the whole's P50 or P90 is zero or below (any difference raises it, and the choice says so), and carries in its instruction block the "Segments: none" handling, the line numbers listed when rows have different field counts, the reasons given when no row counts, and the naming of the comparison claim check when asked about significance. A customization note now covers percentiles printed as written in the export. None of these cases arises in the example, so no example input or figure changed, and the template has still not been run again; the run above is unchanged. The wording differences described in the observations (the weekday in the date, "Tickets missing from the export", the options for Billing) are those of the example page before the first round of edits; the published example has since been aligned with the template, so they no longer exist.
