# Dashboard brief

Workflow template, version 0.1.0.

## Purpose

Settle a dashboard before it is built. From the requester's notes, a sheet of decisions, a list of metrics and a description of each export, prepare one brief: the decisions the dashboard serves, what is shown, every metric's definition in the exact columns of its export, the filters and where each applies, notes on each source, and the refresh owner. The brief is checked for gaps, which are written as numbered questions for the requester. The requester approves what is shown and the definitions. The assistant prepares; it builds no dashboard and no live connection, invents no figure, sample value or column, decides nothing the brief lists, sends nothing and changes no file or record.

## When to use it and when not to

Use it when someone has been asked to build a dashboard in a spreadsheet or a reporting tool and the work has not yet been settled: before the first chart is made, or when an existing request has grown vague.

Do not use it:

- for a fixed monthly page of ten or fewer measures with targets and red levels. That is the Operations KPI scorecard;
- for the owner's weekly one-page review of the business. That is the Weekly owner business brief;
- to build the dashboard, connect it to a system or fill it with numbers. This workflow template produces the brief a builder works from;
- to analyse why a number moved. That is a separate piece of work;
- when there is no decision to serve. A dashboard with no decision attached has no purpose yet; the first question is what the requester will do differently because of it.

## Roles

- **Starts it and prepares the inputs:** the person asked to build the dashboard.
- **Names the decisions, answers the questions, approves what is shown and the definitions:** the requester, who will use the dashboard to decide.
- **Confirms each source's notes and the calculations against the data:** the owner of the export, who may be the analytics owner.
- **Refreshes the dashboard after it is built:** the person named in the refresh section, one role, not a team.
- **Builds from the approved brief:** the person who builds, usually the person who started the work.

## Inputs

1. **The requester's notes,** free text. They should say: the requester's role; the dashboard's working name; who will look at it and how often; where it will be built (a spreadsheet or a named reporting tool); the reporting grain wanted (day, week or month, and any item such as product); the filters wanted; any limits on who may see which data; and who will refresh it and when. Anything not said is "not supplied". If the notes are missing, stop and ask.
2. **The decision sheet,** one row per decision. Default column headers: `decision_code, decision, decider, cadence`. `decision` is a choice between actions, for example "raise, hold or cut next week's budget". `decider` is one person or role. `cadence` is how often the choice is made. If there is no decision sheet, stop and ask. If a header does not match, stop, show the expected and the found headers, and ask which column is which.
3. **The metric list,** one row per metric. Default column headers: `code, metric, decisions, meaning, formula, source_file, columns_used, unit, grain, better`. `decisions` holds the decision codes the metric serves, separated by semicolons. `formula` may be blank when the requester gives only a meaning; where it names another metric it uses that metric's code. `source_file` names each export, separated by semicolons. `columns_used` lists each file followed by a colon and its columns, exactly as headed in the export. `grain` is day, week or month, or the item that a source's `one_row_per` describes, such as product. `better` is `higher`, `lower` or `neither`. If there is no metric list, stop and ask. If a header does not match, stop and ask, as for the decision sheet.
4. **The source sheet,** one row per export. Default column headers: `source_file, what_it_holds, one_row_per, date_column, columns, extracted_on, first_date, last_date, rows, owner`. `columns` is the export's header row, in full. `extracted_on`, `first_date` and `last_date` are dates written YYYY-MM-DD. If there is no source sheet, stop and ask. If a header does not match, stop and ask. If a metric names a file that is not on the source sheet, or a column that is not in that file's `columns`, stop, show the file, the column expected and the columns found, and ask. Never guess which column was meant.
5. **The date the brief is prepared.** If missing, ask.
6. **The firm's settings,** all optional: maximum decisions, metrics and filters; periods shown in a trend; how old an export may be; rounding; the week start. If missing, use the defaults in the procedure.

Do not ask for, and do not repeat, customers' personal details, bank details, passwords or login codes. If an input contains them, say so and ask the person to remove them.

## The procedure

1. **Check the inputs before anything else.** Each sheet's headers match; codes are unique; every decision code in the metric list exists on the decision sheet; every file and column a metric names is on the source sheet; every date is a real date. Any failure listed in the Inputs section stops the work. Anything else becomes a line under Checks on the inputs, and a question where a person has to answer.
2. **Decisions.** Keep each decision as a choice between actions with one decider and a cadence. A decision worded as watching ("keep an eye on sales") is written down as supplied and raised as a question: what choice does it lead to? A decider that is a team, or a missing cadence, is raised as a question. List the metrics that serve each. A decision no metric serves goes under "Decisions with no metric". Default limit: five decisions. More than that, stop and ask the requester which five this dashboard serves.
3. **Metric fit.** A metric with no decision code, or whose decision is not on the sheet, is Left off with that reason. A metric with no source is Left off with that reason. A metric whose grain is finer than its source holds is Left off: a day grain on an export with one row per week. A grain that names an item (such as product) is kept when at least one of the metric's sources has that item as its `one_row_per`; the definition then names the column the metric lists from that source (such as sku) as the one that identifies the item, and a join with another source under a different name is raised as in step 5. A grain that names an item no source of the metric has as its `one_row_per` is Left off. A metric that reads another metric's code takes both metrics' sources and is checked against both metrics' grains: a grain finer than either is Left off, and if either metric is Left off, so is it.
4. **Definitions.** For each metric that remains, write: its meaning in plain words; its formula in exact column names; what is included and excluded; its unit, rounding and grain; whether higher or lower is better, or neither; its source and columns; and what is shown when the data is missing. Use the supplied formula exactly, word for word: add to it no date window, no exclusion and no condition it does not state. Naming the columns it reads, and saying how a word in it is counted (such as "orders" as different order_id values on an export with one row per order line), are allowed and are written as the brief's reading. Where the meaning or the columns suggest something the formula lacks (a cancelled status, a window that ends on a certain day, a week that starts on a certain day), write what the inputs say under Includes and excludes and raise a question; never fill the gap. Where the formula is blank, propose one from the meaning using only columns on the source sheet, and mark the definition PROPOSED, for approval; the requester may change it. A definition built on a supplied formula is marked AS SUPPLIED. If that formula reads a metric that is PROPOSED, it stays AS SUPPLIED and the Status line adds "rests on [code], PROPOSED", so approving it depends on approving the other. Defaults: amounts in whole currency units except per-order or per-item amounts to two decimals; percentages to one decimal; counts whole; days of stock rounded down to whole days. Missing data, no rows for the period, and a division by zero are shown in words ("no data", "no orders"), never as 0. Two metrics with the same formula on the same source are raised as a question: are they one metric?
5. **Check each definition against the data.** Where a formula uses a column that may repeat on every row of a line-level export (an order-level amount on an export with one row per order line, for example), raise a question: does it repeat on each line or appear once? Where the wording of a status, a flag or a code is needed to include or exclude rows (such as which values of a status column mean cancelled), do not guess the wording; raise a question. Where a formula joins two exports on columns with different names, write the join and raise a question for the owner: does every value on one side appear on the other, and what is shown for those that do not? Where two exports must agree on a period (weeks starting on the same day), raise it.
6. **Filters.** For each filter the requester asked for, find the column. A filter with no column in any export is not offered; it goes under "Asked for and not possible" with a question. For each filter offered, say which metrics it applies to, and which it does not and why: a filter on a column that only some of a metric's sources hold would change the metric's meaning if applied to the rest, so it is not applied to them. Name a default for each. Default limit: five filters.
7. **What is shown.** Group the remaining metrics into views, one per decision. Under each, give each metric a form from this list: number with the prior period beside it; line by period; table by item. Choose table by item for a metric whose grain is an item; choose number with the prior period beside it for any other; add a line by period only where the requester's notes ask for a trend. Describe the layout with placeholders in square brackets only. Never write a sample figure. A trend, where asked for, shows twelve periods unless the settings say otherwise. Default limit: ten metrics on the page; more than that, stop and ask which to keep. The requester may change any form; they decide what is shown.
8. **Source notes.** For each source: what it holds, what one row is, its dates, when it was extracted and how many days before the brief that is, its row count, its owner and its columns, all as supplied. Age check: the cadence used is the shortest among the decisions that the source's metrics serve (daily one day, weekly seven days, monthly thirty-one days, or the setting). An extract older than that is flagged stale, with a question about a fresh one. A source with no owner is raised as a question. Never fill in a date, count or owner.
9. **Refresh.** Name one owner (a person or one role), the cadence and the time, from the notes. Write the steps in plain words: get each export again, replace the old one in the dashboard, check the dates against the source notes, tell the viewers. Write one check the owner makes after each refresh, a single comparison taken from the source notes (for example: each export's last date is later than the one in the source notes). Do not combine two conditions in it, and do not state how far a date must move. A missing owner or cover is raised as a question. State that no live connection is built.
10. **Left off.** List every metric left off and every decision with no metric, each with its reason. If there are none, write "none".
11. **Questions,** numbered, in the order the sections appear. Each states the facts, then asks. Every line under Checks that needs a person's answer names its question; a line about a metric already Left off says "see section 7". Recommend nothing unless the requester asks; if asked for options, list them under the question as "for discussion, not agreed".
12. **Approvals.** Close with approval lines for the requester (what is shown and the definitions), one line for each export owner named on the source sheet (the source notes and the calculations against the data for that owner's exports, which the line names) and the refresh owner. An owner of two exports has one line naming both. An export with no owner gets a line naming the file and "owner not supplied", tied to its question. Leave names and dates blank. Nothing is built until a person ticks the first.
13. Use the output format exactly. Write every date in words, such as 3 November 2026, including the dates in the source notes. Keep the form YYYY-MM-DD only inside a formula or where a value in an export is being quoted for matching. Where a section has nothing in it, print its "none" line.

## Exceptions and stop conditions

- **A header does not match, or a column a metric names is not in its export:** stop; show what was expected and what was found; ask.
- **More decisions, metrics or filters than the limit:** stop and ask which to keep.
- **The requester's notes, the decision sheet, the metric list, the source sheet or the preparation date is missing:** stop and ask.
- **A metric has no decision, no source, or a grain finer than its source holds:** leave it off, say why, and ask.
- **A person asks for sample values, a mock-up with numbers, or "just put in something realistic":** decline. The brief describes the layout with placeholders. Any demonstration values belong in the build, labelled invented, after the brief is approved.
- **A person asks the assistant to build, connect, schedule or share the dashboard, or to send the brief:** decline; a person does that after approval.
- **A person asks for a definition to be changed to make a measure look better:** decline.
- **An input holds customers' personal details, bank details, a password or a login code:** do not repeat it; ask the person to remove it.

## Output format

```
DASHBOARD BRIEF: [dashboard name]

Prepared [date] for [requester role]. To be built in [spreadsheet or tool]. Status: DRAFT, not approved. This brief contains no figures.

1. DECISIONS SERVED
[Code]. [Decision]. Decided by [role], [cadence]. Shown by: [metric codes].
Decisions with no metric: [code and reason], or "none".

2. WHAT IS SHOWN
Viewers: [roles], opened [how often]. Access: [limits as supplied, or "none supplied"].
View [n], [title], serves [decision code]:
- [Metric code] [name]: [form, with placeholders only].
Items on the page: [count] of [limit].

3. METRIC DEFINITIONS
[Code] [name]. Status: [AS SUPPLIED or PROPOSED, for approval][; rests on [code], PROPOSED]. Open questions: [numbers, or "none"].
- Meaning: [plain words]
- Formula: [a supplied formula as supplied, or the proposed one; then the columns it reads]
- Includes and excludes: [rows counted and not counted]
- Unit, rounding and grain: [unit; rounding; grain, naming the identifying column for an item grain]
- Better when: [higher, lower or neither]
- Source: [file and columns]
- When the data is missing: [words shown, never 0]

4. FILTERS
[Name]: [column] in [file]. Applies to [codes]. Not applied to [codes]: [reason]. Default: [value].
Asked for and not possible: [filter and reason], or "none".

5. SOURCE NOTES
[File]: holds [what]; one row per [grain]; dates [first] to [last]; extracted [date], [n] days before this brief; [rows] rows; owner [role]. Columns: [list]. Age check: [fresh or stale, with the cadence used].
Joins: [file and column] to [file and column]; [what the owner confirms], or "none".

6. REFRESH
Owner: [one role]. When: [cadence and time]. Steps: [numbered plain steps]. Check after each refresh: [one comparison]. Cover: [name or role, or "not supplied"]. No live connection is built; the numbers change only when the exports are replaced.

7. LEFT OFF
[Code] [name]: [reason], or "none".

8. CHECKS ON THE INPUTS
[One line per flag, with its question number or "see section 7"], or "All checks passed." Lines that only report a pass are not written.

9. QUESTIONS FOR THE REQUESTER
1. [Facts, then the question.]

10. APPROVALS
[ ] [Requester role] approves what is shown (section 2) and the definitions (section 3). Name and date: ______
[ ] [Export owner role] confirms the source notes (section 5) and the calculations against the data for [files]. Name and date: ______ (one line for each export owner)
[ ] [Refresh owner role] accepts the refresh (section 6). Name and date: ______
Nothing is built until the first box is ticked by a person.

This brief was prepared on [date] from the inputs supplied. It builds no connection, contains no figures and changes no file or record.
```

## Reviewer checklist

1. Every decision is a choice between actions with one decider and a cadence. (Requester)
2. Every metric on the page serves a decision on the sheet, and every decision with a metric is listed. (Requester)
3. Every formula uses only columns on the source sheet, spelled as in the export. (Data owner)
4. Every PROPOSED definition is marked, and a supplied formula that rests on a PROPOSED metric says so. (Requester)
5. No section contains a figure that is not an input: no sample values, no totals, no invented counts. (Requester)
6. Every filter's column exists, and every "not applied" is explained. (Data owner)
7. Every source note matches the source sheet, and stale extracts are flagged. (Data owner)
8. The refresh names one owner and one check, and says no live connection is built. (Refresh owner)
9. Every item under Left off has a reason, and every flag under Checks points to a numbered question or to Left off. (Requester)
10. Every supplied formula is word for word as supplied, with nothing added to it, and every gap in it is a question. (Requester)
11. Every export owner has an approval line. (Export owners)

## Acceptance tests

Proposed tests. None has been run; the two runs so far, on the invented example, are not runs of these.

1. **Normal request.** Three decisions, eight metrics, three exports. Expected: all ten sections complete; supplied formulas unchanged; a blank formula marked PROPOSED.
2. **Renamed header.** The metric list has `metric_name` in place of `metric`. Expected: stops, shows expected and found headers, asks.
3. **Formula column missing.** A formula names `net_sales`, which is not in the export. Expected: stops, shows the column expected and the headers found, asks.
4. **No decision.** A metric has a blank `decisions`. Expected: left off, with the reason and a question.
5. **Grain finer than the source.** A daily metric on an export with one row per week. Expected: left off with the reason; a question about a daily export.
6. **Stale extract.** A weekly dashboard with an export pulled eight days before the brief. Expected: flagged stale under Source notes and in Checks, with a question.
7. **Filter with no column.** A requested filter whose column is in no export. Expected: listed under "Asked for and not possible", with a question.
8. **Filter on only one source.** A filter whose column is in one of two sources a ratio reads. Expected: applied to the first only, with the reason stated for the ratio.
9. **Two deciders.** A decider written as "management team". Expected: raised as a question; nothing assumed.
10. **Asked for sample values.** Expected: declined; the layout stays in placeholders.
11. **Asked to build or share.** Expected: declined; approval lines left blank.
12. **Over the limit.** Seven decisions on the sheet. Expected: stops and asks which five.
13. **Vague window.** A supplied formula says "the last 28 days". Expected: formula unchanged and marked AS SUPPLIED; a question asks which 28 days.
14. **Two export owners.** Exports owned by two different roles. Expected: one confirmation line for each, naming its files.
15. **Item grain.** A metric with grain "product" on an export with one row per product. Expected: kept, with the identifying column named.

## Instructions for the AI assistant

```
You prepare a dashboard brief for the person asked to build the
dashboard. You never build the dashboard, connect it to any system,
invent a figure, a sample value or a column, decide anything the brief
lists, send anything, or change any file or record. The requester
decides what is shown and approves the definitions.

The user will supply: the requester's notes; the decision sheet
(decision_code, decision, decider, cadence); the metric list (code,
metric, decisions, meaning, formula, source_file, columns_used, unit,
grain, better); the source sheet (source_file, what_it_holds,
one_row_per, date_column, columns, extracted_on, first_date, last_date,
rows, owner); the date the brief is prepared; and optional settings. If
the notes, the decision sheet, the metric list, the source sheet or the
date is missing, stop and ask. If a header does not match, or a file or
column a metric names is not on the source sheet, stop, show what was
expected and what was found, and ask. Never guess a column. If there are
more than five decisions, ten metrics on the page or five filters, stop
and ask which to keep.

1. Check the inputs: headers, unique codes, decision codes that exist,
   files and columns that exist, real dates.
2. Decisions: each a choice between actions with one decider and a
   cadence. Raise watching-only decisions, team deciders and missing
   cadences as questions. List the metrics that serve each; list any
   decision with none.
3. Metric fit: leave off, with the reason, any metric with no decision,
   no source, or a grain finer than its source holds. A grain naming an
   item (such as product) is kept if one of the metric's sources has
   that item as its one_row_per; name the column that identifies it. If
   no source does, leave the metric off. A metric built on another
   metric's code takes both metrics' sources, is checked against both
   grains, and is left off if either metric is.
4. Definitions: meaning, formula (as supplied, then the columns it
   reads), includes and excludes, unit, rounding and grain, better
   when, source, and what is shown when data is missing. Use a supplied formula exactly and mark
   it AS SUPPLIED: add no window, exclusion or condition it does not
   state, and raise any gap as a question. Where the formula is blank,
   propose one from the meaning using only listed columns and mark it
   PROPOSED, for approval. A supplied formula that reads a PROPOSED
   metric stays AS SUPPLIED and adds "rests on [code], PROPOSED".
   Rounding: amounts in whole currency units, except per-order or
   per-item amounts to two decimals; percentages to one decimal; counts
   whole; days of stock rounded down. Missing data, no rows and division
   by zero are shown in words, never as 0. Raise a question where two
   metrics have the same formula on the same source: are they one
   metric?
5. Raise a question where a formula uses an order-level or other
   repeating column on a line-level export, where the wording of a
   status or flag is needed, where two exports are joined on columns
   with different names, or where periods must line up.
6. Filters: use only columns that exist. A filter with no column is not
   offered; list it with a question. Say where each applies and where it
   does not, and why. Name a default.
7. What is shown: one view per decision. Forms: number with the prior
   period beside it (the default); table by item (for an item grain);
   line by period, only where the requester asks for a trend, twelve
   periods unless the settings say otherwise. Placeholders in square
   brackets only, never a sample figure.
8. Source notes exactly as supplied, with days between extraction and
   the brief. Flag a stale extract (daily one day, weekly seven,
   monthly thirty-one, or the setting) and a missing owner.
9. Refresh: one owner, cadence, plain steps, one check after each
   refresh (a single comparison, such as each export's last date being
   later than in the source notes), cover. State that no live connection
   is built.
10. Left off: each metric and decision, with its reason, or "none".
11. Questions, numbered in section order: facts, then the question.
    Every flag under Checks names its question or "see section 7".
    Recommend nothing unless asked; options go under the question as
    "for discussion, not agreed".
12. Approvals: a line for the requester, one line for each export owner
    (naming that owner's files), and a line for the refresh owner, with
    names and dates blank.
13. Use the output format exactly. Write every date in words, in the
    source notes too. Where a section has nothing, print its "none"
    line. End with the line saying the brief builds no connection,
    contains no figures and changes no file or record.

If asked for sample or realistic values, to build, connect, schedule or
share the dashboard, or to change a definition so a measure looks
better, decline. If an input contains customers' personal details, bank
details, a password or a login code, do not repeat it; ask the person to
remove it. Check every statement against the inputs before you return the
brief.
```

## What to customize

- Your limits: decisions, metrics and filters on one dashboard, and periods shown in a trend.
- How old an export may be before it is flagged, if not the defaults.
- Your rounding, and the day your weeks start.
- Who counts as the requester, each export owner and the refresh owner, so each approval line has a name.
- The column headers of your sheets, if you keep them differently.
- Where the approved brief is kept and who builds from it.
- The forms offered and the defaults for choosing among them, if your tool shows others.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Editorially reviewed. Tried on its invented example in Claude on 10 November 2026 in two runs; the record is `public/trial.md`. The first run found gaps, which this version closes: supplied formulas are now kept word for word with gaps raised as questions, a grain may name the item a source's rows describe, each export owner has an approval line, the refresh check is one comparison, and dates are all in words. The revised instructions were then run once more, and that second run is the one recorded; it was not fully blind, because the example's earlier output had been read. No edit to the instructions, the output format or the example has been made since. Not yet tested in a client environment, and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
