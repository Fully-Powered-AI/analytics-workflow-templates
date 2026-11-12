---
name: "dashboard-brief"
description: "Settle a dashboard before it is built. From the requester's notes, a sheet of decisions, a list of metrics and a description of each export, prepare one brief: the decisions the dashboard serves, what is shown, every metric's definition in the exact columns of its export, the filters and where each applies, notes on each source, and the refresh owner. The brief is checked for gaps, which are written as numbered questions for the requester. The requester approves what is shown and the definitions. The assistant prepares; it builds no dashboard and no live connection, invents no figure, sample value or column, decides nothing the brief lists, sends nothing and changes no file or record."
license: "MIT"
metadata:
  version: "0.1.0"
  publisher: "Fully Powered AI"
  template: "Dashboard brief"
---

# Dashboard brief

This is the technical file for a Fully Powered workflow template. It carries the instructions an AI product follows. The complete template, with roles, inputs, exceptions, the reviewer checklist, acceptance tests and what to customize, is in [TEMPLATE.md](TEMPLATE.md). A worked example with invented data is in [EXAMPLE.md](EXAMPLE.md).

## Instructions

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

## Before relying on it

Decide every item under "What to customize" in TEMPLATE.md and set the limits the instructions in this file leave open, written in square brackets such as [N], to your own. Then run the acceptance tests in TEMPLATE.md on past work. A person starts this work, supplies the inputs and decides what happens with the result.
