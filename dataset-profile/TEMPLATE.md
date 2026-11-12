# Dataset profile

Workflow template, version 0.1.0.

## Purpose

Profile one supplied extract before anyone joins it, loads it or reports from it: what one row is meant to be and whether the data bears that out, where keys repeat, what is missing, which values look odd, where columns disagree with each other, and what the data owner should be asked. Every finding points to a line in the file. The assistant describes; it never changes, removes or corrects a row, never judges whether the data is good enough, and states no business conclusion.

## When to use it and when not to

Use it when a new extract arrives, when a table is inherited, or when a familiar export changes shape, and before the first join. It suits a single table or file at a time.

Do not use it to check a finished workbook before it is sent (that is the spreadsheet check before sharing), to clean or de-duplicate data, to reconcile two sources, or to explain a movement in a metric. Do not use it on a file the person is not entitled to share with the assistant.

## Roles

- **Runs it:** the analyst, who supplies the file and decides what each finding means for the work.
- **Answers the questions:** the data owner named in the settings, a person or team who knows how the extract was produced.
- **Decides what to clean, exclude or correct at source:** the analyst. The profile only lists what is open.

## Inputs

1. **The extract,** as CSV text, a pasted table or an attached file. The first line is the header and is line 1; every line number in the profile counts from there. If the file is a sample or may be cut off, the analyst says so; if it appears to end mid-row, say so in the profile. If missing, stop.
2. **Schema notes,** one line per column with the default headers `column`, `meaning`, `type`, `allowed`. Types are plain words such as whole number, number, date YYYY-MM-DD, text, two-letter code. If missing, stop and ask; do not guess meanings from column names.
3. **Settings,** typed by the analyst, one per line:
   - `File:` the file name and whether it is the full export or a sample.
   - `Today:` the date.
   - `Intended use:` one sentence. If missing, section 8 reads "Intended use not supplied".
   - `Expected key:` the columns that should make a row unique. If missing, ask once. If the analyst does not know, offer the smallest sets of up to three columns that are unique in the data, labelled "candidate keys, observed, not confirmed".
   - `Join key:` if different from the expected key. Default: same as the expected key.
   - `Expected period:` the dates the date columns should fall in. If missing, do not test it and say so.
   - `Far-out rule:` default more than 10 times the column median; for a column whose median is zero or negative the default rule is not applied, and the profile says so and gives only the minimum, median and maximum for that column.
   - `Personal-data columns:` default none. For these columns, report counts only and print no values.
   - `Data owner:` default "the data owner".
   - `Analyst:` who the profile is for. Default "the analyst".
   - `Identifier column:` optional, a single column that names a thing (an order number, a customer number). It gets a distinct count and no spread, even when it is also a column of the expected key. Default none.
4. **Stand-in values.** Defaults: N/A, NA, n/a, null, none, unknown, TBD, -, ?, and the dates 0000-00-00, 1900-01-01, 1970-01-01 and 9999-12-31. The analyst may add their own.
5. **Consistency rules,** optional, typed by the analyst: any column pair that should agree, such as a total equal to quantity times price, or one date on or after another. Without them, test only the rules in step 7 of the procedure.

If a header in the schema notes does not match a header in the extract, or the reverse, stop (procedure step 1).

## The procedure

1. **Check the file.** Count data rows and columns. Compare the extract's headers with the schema notes' `column` values by name and order. If any header is in one and not the other, or the names differ in any way, stop: list the differences and ask the analyst whether to correct the notes, rename a column or supply the right file. Do not profile on a guessed match. Check that every row has the same number of fields; if not, stop and list the line numbers.
2. **Row grain.** State what one row is meant to be, from the notes and the expected key. Count the distinct values of the key and compare with the row count. The grain holds only if they are equal. If not, list every key that appears more than once with its line numbers (up to ten keys, then the count of the rest). Do the same for the join key. If the settings name an identifier column, give its distinct count; otherwise leave that line out.
3. **Duplicates.** Split the repeats into two kinds. Identical rows: every field the same; list the line numbers. Same key, different values: list the lines, name the columns that differ and show the differing values, and name the columns that agree. Never choose which row is right.
4. **Missing and stand-in values.** For every column, count blanks (empty or only spaces) and stand-in values separately, with line numbers up to ten, and say how many rows hold a real value. A zero is not a blank, and a stand-in value is not converted to a blank. List the columns that have neither. A blank in a column the notes say is always filled is stated as such, in that column's line.
5. **Types and formats.** For each column, compare what the values look like with the type in the notes. Report: numbers stored with symbols or text; dates in a second format; an ambiguous slash date (both parts 12 or under) with both readings, left unread; leading or trailing spaces; values that differ only in capitalisation, spacing or punctuation; codes that break the pattern the rest follow. Do not rewrite any value.
6. **Values and spreads.**
   - Numbers: for every column typed whole number or number, except the identifier column, the minimum, median, maximum, how many are negative and how many zero, and each line beyond the far-out rule (the threshold is printed). The identifier column gets its distinct count only, in step 2.
   - Dates: for every date column, earliest and latest of the readable values, any outside the expected period (if one was given) and any after today, saying "none" where there are none; and any the step 5 left unread, stating how they would fall under each reading.
   - Categories: the distinct count and each value's count; a stand-in value counts as a value and a blank does not. If more than ten distinct values, the ten largest and the number of the rest. Values outside the allowed list (compared exactly as written, so "Web" is outside "web"), values seen once, and the counts with capitalisation ignored when look-alikes exist.
7. **Consistency rules and allowed values.** Test only: the rules the analyst listed; any pair of date columns the notes name as one earlier than the other; any total the notes define as a product or sum of other columns. Do not test a date order, or any other rule, that neither the analyst nor the notes state; say instead that no such rule was given. For each rule give how many rows were tested, how many pass, and the lines that fail with their values. A row where a date in the rule is blank or unread is left out of the test, and listed with the reason. Then, for every column whose `allowed` entry in the notes states a limit or a list, give how many rows pass and the lines that do not.
8. **What the findings touch.** In a few lines, say which findings sit on the columns, rows and keys the intended use reads, and which sit on columns it does not read. State facts only: what a join or grouping would do with the row, not whether the data is fit.
9. **Questions for the data owner.** One numbered question per finding that needs an answer from someone else, in section order, each with its line numbers and values and written so it can be answered in a sentence. Offer no answer.
10. **Decisions for the analyst.** One numbered line per open choice (findings that call for the same options on the same columns may share a line), naming the lines and only those options that fit that choice (keep as supplied, hold out of a figure, correct at source, wait for an answer); an option that does not fit may be left out. Recommend none. Final line: whether the data is usable is the analyst's decision.
11. **Not checked, and trace line.** Say what a profile of a file cannot see: whether values are true, whether rows are missing, other tables, meaning beyond the notes. End with the trace line.

## Exceptions and stop conditions

- **Headers do not match the notes, or rows have different field counts:** stop; list the differences or line numbers; ask.
- **No schema notes:** stop and ask; the profile is only as good as the meanings given.
- **No expected key:** ask once; if unknown, give candidate keys, labelled as observed.
- **The file looks cut off or is a sample:** say so at the top, and say the figures describe the rows supplied only.
- **A column is marked personal data:** counts only; no values in any section, question or decision.
- **Asked to clean, de-duplicate, fill, correct or drop rows, or to produce a corrected file:** decline; the analyst decides and makes the change in their own tools.
- **Asked whether the data is good, or what it shows about the business:** decline; list the findings and the open decisions instead.
- **Asked for a login, a database connection or a password:** decline; work only from the file supplied.
- **A figure cannot be recomputed from the rows supplied:** leave it out and say so.

## Output format

```
DATASET PROFILE: [file name]

For: [Analyst setting, or "the analyst"]. Prepared [Today] from the settings, schema notes and extract supplied. Intended use: [sentence, or "not supplied"].

1. THE FILE
Header check: [matches the notes in name and order / the differences, then stop]. [n] data rows, [n] columns; every row has [n] fields [or the lines that do not]. [Full export / sample / may be cut off], as stated.

2. ROW GRAIN
Expected: [what one row is], key [columns]. [n] distinct keys among [n] rows. [The grain holds / does not hold: n keys appear more than once ([key] on lines [..])].
[If an identifier column is named: Identifier [column]: [n] distinct values.]
Join key [columns]: [n] distinct among [n] rows. [Repeats, with lines / no repeats].

3. DUPLICATES
Identical rows: [n pairs or groups, lines / none found among [n] rows].
Same key, different values: [key] on lines [..]. They differ in [columns and values]; they agree in [columns] / [none found].

4. MISSING AND STAND-IN VALUES
[column]: [n] blank (lines [..]); [n] stand-in, "[value]" (lines [..]). [n] of [n] rows hold a value. [If the notes say the column is always filled: "The notes say it is filled for every line."]
No blank or stand-in values in [columns].

5. TYPES AND FORMATS
[column]: [finding with lines] / [columns whose values all match their type].

6. VALUES AND SPREADS
[numeric column]: min [], median [], max []. [n] negative [lines]; [n] zero. Far-out (above [threshold]): [lines and values / none].
[date column] ([n] readable): earliest [], latest []. [Outside [period]: [lines / none].] After [Today]: [lines / none]. [Unread dates and how each reading falls.]
[category column] ([n] distinct): [value count, ...]. Outside the allowed list: [lines / none]. Values seen once: [.. / none]. [Counts with capitals ignored, if look-alikes.]

7. CONSISTENCY RULES AND ALLOWED VALUES
[rule]: [n] tested, [n] pass. Fail: [line, values / none]. Left out: [lines and why / none].
[Rules not given: say which common rule was not tested because none was stated.]
Allowed values in the notes, one line per column that has a limit or list: [column] [allowed]: [n] tested, [n] pass. Not passing: [line, value / none].

8. WHAT THE FINDINGS TOUCH FOR THE INTENDED USE
[Facts about keys, rows and columns the use reads; columns it does not read and the findings on them.]

9. QUESTIONS FOR THE DATA OWNER ([name or role])
1. [Question with lines and values.]
[If none: "No questions arise from the findings."]

10. DECISIONS FOR THE ANALYST
1. [Open choice, lines, the options that fit.]
[If none: "No decisions are open."] Whether the data is usable is the analyst's decision.

11. NOT CHECKED
[Whether values are true to the real world; missing rows; other tables; meaning beyond the notes; anything the analyst left out.] No row has been changed, removed or corrected.

Every figure counts the [n] data rows of [file name] as supplied on [Today]. This profile changes no data and states no conclusion about the business.
```

When a section has no findings, print its heading, then what was checked and "none found", never a blank.

## Reviewer checklist

1. Row count, distinct-key count and the header check can be reproduced from the file. (Analyst)
2. Every line number points to the row described, counting the header as line 1. (Analyst)
3. Blanks, stand-in values and zeros are counted separately, and no stand-in value was treated as a blank. (Analyst)
4. Every figure in the spreads section recomputes from the rows. (Analyst)
5. Every repeated key lists the columns that differ, and no row was chosen as correct. (Analyst)
6. Every question can be answered in a sentence and offers no answer. (Data owner)
7. No decision carries a recommendation, and no sentence says the data is good or bad. (Analyst)
8. Columns marked personal show counts only. (Analyst)
9. Nothing in the file was changed, and no corrected file was produced. (Analyst)

## Acceptance tests

Proposed tests. None has been run as a test of its own; the run on the invented example touched tests 3, 4, 6 and 12 through its data.

1. **Clean file.** Every key unique, no blanks, every value in range. Expected: each section says what was checked and that none was found; questions and decisions say none.
2. **Header mismatch.** The notes list `qty` and the file has `quantity`. Expected: stops and lists the difference; no profile.
3. **Identical duplicate.** Two rows alike in every field. Expected: reported once as identical rows with both lines; neither removed.
4. **Repeated key, different values.** Same key on two lines with different amounts. Expected: reported under same key, different values, with the differing columns and values; no row chosen.
5. **Stand-in text in a numeric column.** "N/A" among numbers. Expected: counted as a stand-in value, not as a blank and not as zero, and reported under types.
6. **Ambiguous date.** 03/04/2026. Expected: both readings stated; left unread; shown in the period test under each reading.
7. **Personal-data column.** A column marked personal with a repeated value. Expected: counts only; no values anywhere in the profile.
8. **Asked to clean the file.** Expected: declines; lists the decisions for the analyst.
9. **No expected key given.** Expected: asks once; if unknown, candidate keys labelled observed.
10. **Asked "is this data good enough?"** Expected: declines; lists the findings and open decisions.
11. **Date order not stated.** Two date columns, no rule from the analyst and nothing in the notes about which comes first. Expected: no order test; the section says no such rule was given.
12. **Date order stated.** The analyst lists "ship_date on or after order_date"; one row has a blank ship_date and one an unreadable order_date. Expected: both left out and listed with the reason; the rest tested.

## Instructions for the AI assistant

```
You write a dataset profile for an analyst, from one extract they have
supplied. You never change, remove, fill or correct any row, never produce
a corrected file, never decide whether the data is usable, and state no
conclusion about the business. The analyst approves and makes every change
to the data, in their own tools. You never ask for a password, a login
code or a database connection; you work only from what is supplied.

The analyst will supply: the extract (the header is line 1); schema notes
with the columns column, meaning, type, allowed; and settings (file, today,
intended use, expected key, join key, expected period, far-out rule,
personal-data columns, data owner, analyst name, identifier column) and,
optionally, consistency rules and stand-in values of their own. If the
extract or the schema notes are missing, stop and say so. If the expected
key is missing, ask once; if the analyst does not know, give the smallest
sets of up to three columns that are unique in the data, labelled "candidate keys, observed, not
confirmed". Defaults: far-out rule is more than 10 times the column median
(for a column whose median is zero or negative, do not apply it: say so and
give only min, median and max); no personal-data columns; data owner "the data owner"; analyst "the
analyst"; no identifier column; if no period is given, do not test one and
say so. List at most ten line numbers or keys for any one finding, then
give the count of the rest.

1. Check the file. Compare the extract's headers with the notes' column
   names, by name and order. If any differ, or rows have different field
   counts, stop, list the differences or line numbers, and ask. Say
   whether the file is a full export, a sample or may be cut off, as the
   analyst states, and that the figures describe the rows supplied.
2. Row grain: state what one row is meant to be. Count distinct values of
   the expected key and of the join key against the row count. If not
   equal, list the repeated keys with their line numbers. If an identifier
   column is named, give its distinct count on its own line, even if it is
   also a key column.
3. Duplicates: separate identical rows from rows that share a key but
   differ. For the second kind name the columns that differ and show the
   values. Never choose which row is right.
4. Missing and stand-in values: count blanks and stand-in values (N/A, NA,
   n/a, null, none, unknown, TBD, -, ?, and the dates 0000-00-00,
   1900-01-01, 1970-01-01, 9999-12-31, plus the analyst's own) separately,
   per column, with line numbers, and say how many rows hold a value. A
   zero is not a blank. Convert nothing. If the notes say a column is
   always filled, say so beside any blank in it.
5. Types and formats: compare values with the notes' types. Report mixed
   date formats, numbers held as text, stray spaces and values that differ
   only by capitals or punctuation. For an ambiguous slash date give both
   readings and leave it unread.
6. Values and spreads: for every number column except the identifier, min,
   median, max, negatives, zeros and values beyond the far-out rule (print
   the threshold); for every date column, earliest, latest and any outside
   the expected period or after today, saying none where none; for
   categories, counts (a stand-in counts as a value, a blank does not),
   values outside the allowed list (exact spelling and capitals), values
   seen once and, if look-alikes exist, counts with capitals ignored.
   Unread dates: say how each would fall under each reading.
7. Consistency rules and allowed values: test only the rules the analyst
   listed, date pairs the notes name as earlier and later, and totals the
   notes define; never test a date order nobody stated, and say none was
   given. Give rows tested, rows passing, failing lines with values, and
   rows left out (a blank or unreadable date) with the reason. Then give,
   for each column with an allowed limit or list in the notes, rows tested,
   rows passing and the lines that do not.
8. Say which findings touch the columns and keys the intended use reads.
   State facts, not fitness.
9. Write one numbered question per finding that needs the data owner, with
   line numbers and values. Offer no answer.
10. Write one numbered decision line per open choice with the options that
   fit it (keep as supplied, hold out of a figure, correct at source,
   wait). Make no recommendation. Say that whether the data is usable is
   the analyst's decision.
11. Say what was not checked, then end with the trace line.

Use the output format exactly. Where a section has no findings, print its
heading, what was checked, and "none found". For columns marked personal
data, print counts only and no values. Recompute every figure from the rows;
if one cannot be recomputed, leave it out and say so. If asked to clean,
de-duplicate, fill or drop rows, or to say the data is good or bad, decline
and list the decisions instead.
```

## What to customize

- Your schema notes for each source, kept and reused.
- The far-out rule, the stand-in values your systems use, and the expected period.
- Which columns hold personal data and must show counts only.
- The data owner for each source, and how the questions reach them.
- Any consistency rules your data should always obey.
- Where profiles are filed, and which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI from its own published map of the work. It was tried on its invented example in Claude on 10 November 2026; the record is published with it. After that first run the template was edited (a date order is tested only when a rule or the notes state it, and the settings, defaults and wording named in the record were settled), and the edited version has been run once more by the assistant that made the edits, not independently. It has not been tested in a client environment.
