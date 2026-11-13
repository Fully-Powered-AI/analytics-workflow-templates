# The distribution behind an average

Workflow template, version 0.1.0.

## Purpose

Describe the spread of one service or process measure from an export the person supplies, so a review does not rest on the average alone: the rows counted and not counted, the whole population's percentiles, what the average leaves out, each segment's figures, the differences between each segment and the whole, the extreme cases by line, records to check, the points the analytics owner confirms and the choices the process owner makes. Every figure is computed by one stated method from the counted rows and can be recomputed from the export. The assistant describes; it never states or suggests a cause, never removes, corrects or reclassifies a row, runs no statistical test, and recommends no follow-up.

## When to use it and when not to

Use it when a review of a duration or an amount per record is about to rest on an average: hours to resolve a ticket, days from order to delivery, days to turn a request around, minutes on hold, the value of a claim or a refund. Use it before a target is set or questioned, at a monthly service review, or when one team, queue or site looks different from the rest. One measure and one export per run. The view looks at the high end only: a record is an extreme case when it is unusually large, never when it is unusually small, which suits durations and amounts where the long upper tail is the concern.

Do not use it:

- to explain why a value or a segment is high or low. The page states figures only; finding causes is the process owner's follow-up;
- to test whether a difference between two groups would hold in another period. That is the comparison claim check;
- to profile an unfamiliar export for keys, blanks and formats before anyone relies on it. That is the dataset profile;
- to clean, de-duplicate or correct data, or to produce a corrected file;
- on a measure that mixes units in one column, or on records the person is not entitled to share with the assistant.

## Roles

- **Runs it:** the analyst or the operations lead who owns the measure. Supplies the export and the settings, and reads the page first.
- **Confirms the figures, the method and the rows not counted:** the analytics owner named in the settings (default "the analytics owner").
- **Decides which cases or segments, if any, to follow up, and how:** the process owner named in the settings (default "the process owner").
- **Changes any record at source:** the person who owns that system, never the assistant.

## Inputs

1. **The export,** one row per record, as CSV text, a pasted table or an attached file. The first line is the header and is line 1; every line number on the page counts from there. Default column headers:
   - `record_id`: what identifies the record (a ticket, order or request number).
   - `segment`: the group the record belongs to (a queue, site, team or channel). Optional; see the settings.
   - `recorded_on`: the date that places the record in the window, written YYYY-MM-DD.
   - `measure`: the duration or amount, as a plain number in the unit stated in the settings.

   Other columns are ignored and listed by name in section 1. If the export is missing, stop and ask.
2. **Settings,** typed by the person, one per line:
   - `File:` the file name.
   - `Today:` the date.
   - `Measure:` what the number is and its unit, such as "hours to resolve, in hours". If missing, stop and ask.
   - `Population:` one sentence on which records the export is meant to hold. If missing, write "population not stated" in the header and in section 9.
   - `Window:` first and last date, both counted. If missing, stop and ask.
   - `Columns:` a mapping when the export's headers differ from the defaults, such as `measure = hours_to_resolve`. Default: the default headers.
   - `Segments:` "yes" (default) or "none". With "none", the segment column is not needed and sections 3 and 4 say "No segment column supplied".
   - `Target:` a value in the measure's unit, counted as "over target" when a record is strictly above it. Default: none, and the target lines say "Target not supplied".
   - `Extreme cut:` the percentile above which a record is an extreme case. Default P90.
   - `Minimum segment size:` the smallest count that gets a mean and percentiles of its own. Default 5.
   - `Combine:` segments to report together, as one named group. Default: none. Combine only what this line names.
   - `Analyst:`, `Analytics owner:`, `Process owner:` roles or names. Defaults: "the analyst", "the analytics owner", "the process owner".

If a header named by the defaults or the mapping is not in the export, stop (procedure step 1). If the export has start and end times but no measure column, stop and ask for an export with the measure worked out in the stated unit; do not compute durations.

## The procedure

1. **Check the export.** Find the four columns by the default headers or the mapping. If any is missing (the segment column only when `Segments:` is "yes"), stop: list the headers expected and the headers found, and ask the person to supply a mapping or the right file. Do not match on a guess. Check that every row has as many fields as the header; if not, stop and list the line numbers. If the file seems to end mid-row, or is too long to read in full, stop and say so: no figure is ever computed from part of the rows.
2. **Decide which rows count.** A row counts when its `recorded_on` reads as a YYYY-MM-DD date inside the window and its `measure` is a plain number. Every other row is not counted and is listed with its line, record_id and one reason: outside the window, date unreadable, or measure blank or not a number. Never correct a value to make it count. A blank segment is reported as its own segment, "(blank)", and never assigned to another. If no row counts, stop and say so. If fewer than 20 rows count, say at the top of section 2 that the view rests on few records.
3. **Fix the method.** Sort the counted values from smallest to largest. Pk is the value at position k × n ÷ 100, rounded up to a whole number, where n is the count. Show Pk only when that position is below n; otherwise print "not shown (n under [the smallest n at which it would show])": P25 and P50 need 2, P75 needs 4, P90 needs 10, P95 needs 20, P99 needs 100. The mean is the sum divided by n. Round means, differences and percentages to one decimal place and ratios to two, half away from zero. Percentiles, minimums and maximums are values from the export and are printed as written.
4. **Describe the whole population.** Count, mean, minimum, P25, P50, P75, P90, P95, maximum. With a target, the count strictly over it, as "n of n" and a percentage; a value equal to the target is not over it. Then "what the average leaves out", four facts and no more: the mean against P50; how many records sit strictly above the unrounded mean, as a count and a percentage; the largest k records, where k is 10% of n rounded up, their sum against the total and as a percentage of it (not shown when the total is zero or below); and P90 divided by P50 (not shown when either is not shown or P50 is zero or below).
5. **Describe each segment.** Apply any `Combine:` line first and name the group it forms. Order segments from largest count to smallest, ties alphabetically. For each segment at or above the minimum size: count, mean, minimum, P25, P50, P75, P90, P95, maximum and, with a target, the count over it as "n of n" and a percentage. For a segment below the minimum size: count, minimum, maximum and the count over target as "n of n" only, marked "under [minimum]".
6. **State the segment differences.** For each segment: its share of the counted records; how many of the extreme cases (step 7) it holds, as "n of n" and a percentage, where the second n is every counted record above the cut, whether or not it is listed; for segments at or above the minimum size, its P50 minus the whole population's P50, its P90 minus the whole's P90 where both are shown, and its P90 divided by its P50 where shown; with a target, its over-target percentage against the whole's. Use a plus or minus sign on every difference. End with: "Percentages are rounded and may not add to 100. Differences are described, not tested." Use no word that gives a reason, such as because, due to, driven by, caused by or reflects.
7. **List the extreme cases.** Every counted record strictly above the whole population's value at the extreme cut (default P90), largest first, numbered, each with its line, record_id, segment, recorded_on and value. List up to 15, then "and [n] more above [cut], not listed". Mark "far out" any record above P75 + 3 × (P75 − P25) of the whole population, and print that fence with its working. If P75 is not shown for the whole population (fewer than 4 counted records), print "fence not shown" and mark none far out. If the cut percentile is not shown for the whole population, write "No extreme cut: [cut] is not shown for [n] records" and list none.
8. **List the records to check.** Zero or negative values, with lines. Any record_id on more than one counted line, with the lines and values. Both kinds stay in every figure as supplied; say so. Write "none found" for a kind with none.
9. **Write the points for the analytics owner.** One numbered point per row not counted, per record to check, per segment under the minimum size and per combination applied, each with its lines and values and written so it can be answered in a sentence. Always end with the method point: nearest rank, so a spreadsheet function that interpolates may give a different P-value.
10. **Write the choices for the process owner.** One numbered choice for the extreme cases as a group (naming the lines), one for each segment at or above the minimum size whose P50 differs from the whole's P50, or whose P90 differs from the whole's P90, in either direction, by more than half of the whole's value at that same percentile (compared before rounding; where the whole's value at that percentile is zero or below, that threshold is not defined, so any difference at all from the whole's value raises the choice, and the choice says so), and one for the target where one is given. List the segment choices in the order of section 3. Each choice names the figures and offers only the neutral options that fit it, from this list: look into the records named, compare with another period, run a comparison test, take no action. "Look into the records named" is offered only for the extreme cases as a group, which names lines. "Run a comparison test" is offered only for a segment choice. The choice for the target offers "compare with another period" and "take no action". Recommend none and rank none. End with: "Which follow-up, if any, is the process owner's decision."
11. **Say what is not shown, then the trace line,** and return the page to the person who ran it. A person decides who else sees it.

## Exceptions and stop conditions

- **A header is missing, a mapping names a column that is not there, or rows have different field counts:** stop; list what was expected and found, or the line numbers; ask.
- **No measure unit or no window:** stop and ask.
- **The export is too long to read in full, or looks cut off:** stop and say so; compute nothing from part of it.
- **Start and end times but no measure:** stop; ask for the measure worked out in the stated unit.
- **No row counts:** stop and say which reasons removed them all.
- **Asked why a segment or record is high, or what caused a pattern:** decline; list the figures and the process owner's choices instead.
- **Asked whether a difference is significant or real:** decline; say the page runs no test, and name the comparison claim check.
- **Asked to drop, cap, correct or re-segment rows, or to produce a cleaned file:** decline; list the records as points for the analytics owner, who makes any change in their own tools.
- **Asked to send the page, post it or change a record:** decline; a person does that after approval.
- **Asked for a login, a password or a database connection:** decline; work only from what is supplied.
- **A figure cannot be recomputed from the counted rows:** leave it out and say so on the page.

## Output format

```
DISTRIBUTION VIEW: [measure] ([unit]), [window first date] to [window last date]

For: [analyst]. Prepared [today] from the settings and the export [file name]. Population: [sentence, or "population not stated"]. Analytics owner: [role]. Process owner: [role].
Method: nearest rank, on the counted values sorted from smallest to largest.
Pk is the value at position k x n / 100, rounded up.
A percentile at the last position is not shown.
Means, differences and percentages to one decimal place; ratios to two.

1. THE EXPORT
Header check: [the four columns found, with the export's names / the differences, then stop]. Other columns, ignored: [names / none].
[n] data rows supplied; [n] counted. Not counted: [line, record_id, reason; ... / none].

2. THE WHOLE POPULATION
[If under 20 counted: "This view rests on [n] records."]
Count [n]. Mean [x]. Min [x]. P25 [x]. P50 [x]. P75 [x]. P90 [x]. P95 [x / not shown (n under 20)]. Max [x].
Over target ([target value] [unit]): [n] of [n] ([x]%). / Target not supplied.
What the average leaves out: the mean is [x] and P50 is [x]. [n] of [n] records ([x]%) sit above the mean. The largest [k] records (10% of the count, rounded up) hold [sum] of [total] [unit] ([x]%). P90 is [x] times P50.

3. BY SEGMENT ([segment column])
[Segment]: count [n]. Mean [x]. Min [x]. P25 [x]. P50 [x]. P75 [x]. P90 [x / not shown (n under 10)]. P95 [x / not shown (n under 20)]. Max [x]. Over target [n] of [n] ([x]%).
[Segment] (under [minimum]): count [n]. Min [x]. Max [x]. Over target [n] of [n].
[Combined: "[group]" is [segments], as the settings ask.]
[Or: "No segment column supplied."]

4. SEGMENT DIFFERENCES
[Segment]: [x]% of counted records; [n] of [n] extreme cases ([x]%). P50 [+/-x] against the whole. P90 [+/-x / not compared]. [P90 is [x] times P50. / P90 to P50 ratio not shown.] Over target [x]% against [x]% for the whole.
[Segment] (under [minimum]): [x]% of counted records; [n] of [n] extreme cases ([x]%). Over target [n] of [n].
Percentages are rounded and may not add to 100. Differences are described, not tested.
[Or: "No segment column supplied."]

5. EXTREME CASES (above [cut], [value])
1. Line [n], [record_id], [segment], [recorded_on]: [value]. [far out]
[and [n] more above [cut], not listed]
Far out means above P75 + 3 x (P75 - P25) = [x] + 3 x ([x] - [x]) = [x]. [Or: "Fence not shown."] Every extreme case is kept in every figure.
[Or: "No record is above [cut]." / "No extreme cut: [cut] is not shown for [n] records."]

6. RECORDS TO CHECK
Zero or negative values: [line, record_id, segment, value; ... / none found].
Record ids on more than one counted line: [record_id on lines [..], values [..] / none found].
These records are counted as supplied.

7. FOR THE ANALYTICS OWNER TO CONFIRM ([role])
1. [Point, with lines and values.]
[n]. Method: nearest rank. A spreadsheet function that interpolates between values may give a different P-value.

8. FOR THE PROCESS OWNER TO DECIDE ([role])
1. [Choice, with the figures and neutral options.]
[Or: "No choice arises from the figures."]
Which follow-up, if any, is the process owner's decision.

9. NOT SHOWN
The cause of any value or difference. Whether any difference would hold in another period (no test was run). Whether every row belongs to the population as defined. Whether every value is in the stated unit. Records missing from the export. [Anything else the person left out.]

Every figure is computed from the [n] counted rows of [file name] as supplied on [today]. This view changes no data and states no cause.
```

When a section has no findings, print its heading, what was checked and "none found", never a blank.

## Reviewer checklist

1. The header check and the counts of rows supplied, counted and not counted can be reproduced from the export. (Analytics owner)
2. Every line number points to the row described, counting the header as line 1. (Analytics owner)
3. Every percentile recomputes from the sorted counted values by nearest rank, and none is shown where its position would be the last value. (Analytics owner)
4. Every mean, share, difference and ratio recomputes, rounded as stated. (Analytics owner)
5. Every record above the cut is listed, or counted in "more, not listed", and the fence is worked correctly. (Analytics owner)
6. Zeros, negatives and repeated record ids are listed and still counted; no row was removed or corrected. (Analytics owner)
7. No sentence gives a reason for a value or a difference, and no difference is called significant. (Process owner)
8. No choice carries a recommendation or a ranking. (Process owner)

## Acceptance tests

Proposed tests. None has been run.

1. **Headers differ, mapping given.** The export has `ticket_id, queue, closed_on, hours_to_resolve` and the settings map them. Expected: header check names the four columns and their export names; the page is produced.
2. **Headers differ, no mapping.** Same export, no `Columns:` line. Expected: stops, lists expected and found headers, asks.
3. **Row outside the window and a blank measure.** Expected: both not counted, each listed with its line, record_id and reason, and each raised for the analytics owner.
4. **Percentile at the last position.** A segment of 9 records. Expected: P90 reads "not shown (n under 10)" and P95 "not shown (n under 20)".
5. **Value equal to the target.** Target 24 and one record at 24.0. Expected: that record is not counted as over target.
6. **Zero and a repeated record id.** Expected: both listed under records to check, both kept in every figure, both raised for the analytics owner.
7. **Small segment.** A segment of 3 records with the default minimum. Expected: count, minimum, maximum and over target only, marked "under 5"; it still appears in the extreme-case counts.
8. **Asked "why is Technical so slow?"** Expected: declines to give a cause; points to the figures and the process owner's choices.
9. **Asked "is the gap significant?"** Expected: says no test is run and names the comparison claim check.
10. **Asked to drop the 140-hour ticket as an outlier.** Expected: declines; the record stays counted and is listed as an extreme case.
11. **Start and end times only.** Expected: stops; asks for the measure in the stated unit.

## Instructions for the AI assistant

```
You describe the spread of one service or process measure for an analyst,
from an export and settings they supply. You never state or suggest a
cause, never remove, cap, correct or reclassify a row, never produce a
cleaned file, run no statistical test and recommend no follow-up. You
never send or post the page and never change any record; a person does
that after approval. You never ask for a password, a login code or a
database connection; you work only from what is supplied.

Inputs: the export (header is line 1) with default headers record_id,
segment, recorded_on (YYYY-MM-DD), measure (a plain number); settings:
File, Today, Measure (with unit), Population, Window (first and last
date, both counted), Columns (a mapping if headers differ), Segments (yes
or none), Target, Extreme cut (default P90), Minimum segment size
(default 5), Combine, Analyst, Analytics owner, Process owner. If the
export, the unit or the window is missing, stop and ask. If the export
has start and end times but no measure, stop and ask for the measure;
do not compute durations.

1. Find the four columns by default header or mapping (the segment
   column only when Segments is yes; with none, sections 3 and 4 say "No
   segment column supplied"). If one is missing, stop, list expected and
   found, and ask. If rows have different field counts, stop and list
   the line numbers. If the file looks cut off or is too long to read in
   full, stop: never compute from part of the rows.
2. A row counts when recorded_on is a readable date in the window and
   measure is a plain number. List every other row with line, record_id
   and one reason, only these three: outside the window, date
   unreadable, or measure blank or not a number. Correct nothing. A
   blank segment is its own segment, "(blank)". If no row counts, stop
   and say which reasons removed them all.
   Under 20 counted, write at the top of section 2: "This view rests on
   [n] records." Without a stated population, write "population not
   stated" in the header and in section 9.
3. Method: sort counted values ascending. Pk is the value at position
   k x n / 100 rounded up. Show it only if that position is below n;
   otherwise "not shown (n under N)": P25 and P50 need 2, P75 needs 4,
   P90 needs 10, P95 needs 20, P99 needs 100. Mean = sum / n. One decimal
   for means, differences and percentages, two for ratios, half away from
   zero.
4. Whole population: count, mean, min, P25, P50, P75, P90, P95, max;
   count strictly over target as "n of n" and % (print the target with
   its unit). Then four facts: mean
   against P50; records strictly above the unrounded mean; the largest k
   records (k = 10% of n rounded up), their sum against the total and %
   (not shown when the total is zero or below); P90 / P50 where both
   are shown and P50 is above zero.
5. Segments, after any Combine line, largest first, ties alphabetical:
   the same figures; below the minimum size only count, min, max and
   over target as "n of n", marked "under N".
6. Differences: share of counted records; extreme cases held, as "n of
   n" and % (the second n is every counted record above the cut, listed
   or not); for segments at or above the minimum, P50 and P90 minus the
   whole's (signed) and P90 / P50; over-target % against the whole's.
   Never use because, due to, driven by, caused by or reflects. End:
   "Percentages are rounded and may not add to 100. Differences are
   described, not tested."
7. Extreme cases: every record strictly above the whole's value at the
   cut, largest first, up to 15 then "and n more". Mark "far out" above
   P75 + 3 x (P75 - P25) and print the fence with its working; if P75
   is not shown for the whole, print "fence not shown" and mark none far
   out. Only the high end counts; a low value is never an extreme case. If the cut
   percentile is not shown for the whole, write "No extreme cut: [cut]
   is not shown for [n] records" and list none.
8. Records to check: zero or negative values; record_ids on more than
   one counted line. Keep them in every figure and say so.
9. Points for the analytics owner: one per row not counted, record to
   check, small segment and combination, with lines and values; end with
   the nearest-rank method point.
10. Choices for the process owner: the extreme cases as a group; each
   segment at or above the minimum, in the order of section 3, whose P50
   or P90 differs from the whole's P50 or P90, either way, by more than
   half of the whole's value at that percentile (unrounded; if the
   whole's value there is zero or below, any difference at all raises the
   choice, and the choice says so); the target if given. Only the neutral options that fit, from: look into the
   records named (extreme cases as a group only), compare with another
   period, run a comparison test (segment choices only), take no action;
   the target gets compare with another period or take no action. No
   recommendation, no ranking. End: "Which follow-up, if any,
   is the process owner's decision."
11. Not shown, then the trace line.

Use the output format exactly. Where a section has no findings, print
its heading, what was checked and "none found". Recompute every figure
from the counted rows before printing it; if one cannot be recomputed,
leave it out and say so. If asked for a cause, decline and point to the
choices and points instead. If asked whether a difference is significant
or real, decline, say the page runs no test and name the comparison
claim check. If asked to drop or fix a row, decline and list it as a
point for the analytics owner. Return the page to the person who ran it.
```

## What to customize

- The column mapping for each export you use, kept with the measure.
- The target, the extreme cut and the minimum segment size.
- Segments you always report together, as a standing `Combine:` line.
- The analytics owner who confirms figures and the process owner who decides follow-up, for each measure.
- Whether percentiles, minimums and maximums should print to the same decimals as the means. By default they print as written in the export, so an export of whole numbers prints them without decimals beside means with one.
- Whether your reports use nearest rank too, or carry a note where a spreadsheet's interpolated percentiles differ.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini, and where approved pages are filed.

## Version notes

- 0.1.0, 11 November 2026. Written by Fully Powered AI from its own published map of analytics work. Tried on its invented example in Claude on 11 November 2026, on the instructions as they stood that day; the record of that run is published with the template. Later edits were made after review (listed in the trial record) and have not been run again; the eleven acceptance tests, including the decline cases, are still to be run. Not yet tested in a client environment.
