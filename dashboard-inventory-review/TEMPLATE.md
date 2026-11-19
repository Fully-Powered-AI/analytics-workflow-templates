# Dashboard and report inventory review

Workflow template, version 0.1.0.

## Purpose

Prepare one review of every dashboard and report in the company's business intelligence tool, from the tool's own dashboard and usage export: the items nobody has viewed within the team's limit, the items whose owner has left or is blank, likely duplicates by name and data source, scheduled sends with no views in the tool, and the items built on a data source marked for retirement. Each finding carries the item ids and the counts from the export, a count line proves every row was read, and the review ends with a proposed list of questions for each owner. The assistant prepares; it never retires, deletes, moves, reschedules or shares anything, and the person who decides retirement decides every item.

## When to use it and when not to

Use it twice a year, and before the tool's licence renews or the company moves to another tool, so the people deciding know what is in the tool and what is still used. It also serves after two companies' reporting is brought into one tool, when the same report often exists twice.

Do not use it:

- to judge whether a metric on a dashboard is defined or calculated correctly. That is a metric definition reconciliation, run separately;
- to read or check the data inside a dashboard. This review reads the inventory only;
- to judge people. Views and viewers are counts per item; nobody is named, ranked or compared by how much they use the tool;
- to decide what is retired. The person named in the team's rules decides, after the owners answer;
- when there is no export. It needs no connection to the tool and never asks for a password or a login code; a person exports the file and supplies it.

## Roles

- **Runs it:** the analytics lead or the person who administers the company's reporting tool.
- **Decides what is retired, kept or merged, and names a new owner where one is missing:** the role named in the team's rules, by default the analytics lead.
- **Answers for each item:** the dashboard owner named in the export.
- **Retires, moves or reschedules anything in the tool:** a person with administrator rights, after the decision. Never the assistant.

## Inputs

1. **The dashboard and usage export from your business intelligence tool.** One row per dashboard or report. Default headers, in any order: `item_id`, `name`, `type` (dashboard or report), `folder`, `owner`, `created_at`, `last_edited_at`, `last_viewed_at`, `views_90d`, `distinct_viewers_90d`, `data_source`, `scheduled` (yes or no). Dates are read as year-month-day. If a header is missing or named differently, stop: list the headers expected and the headers found, and ask the person which column is which. Do not guess a mapping. If the export has extra columns, ignore them, and never repeat a column that names or identifies individual viewers. If there is no export, stop.
2. **The team's rules.**
   - How long without a view counts as unused. Default: 90 days if not stated, and say the default was used. This limit is called the team's unused limit below.
   - Folders exempt from the use checks, such as items kept for audit. If none are stated, write "none stated".
   - Who decides retirement. If not stated, write "not stated" in the header and ask for it under the proposed list.
   - Data sources marked for retirement, each with its date. If none are stated, write "none stated".
3. **A leavers list,** optional: the names of people who have left, written as they appear in the `owner` column. If not supplied, write "leavers list not supplied" and check blank owners only.
4. **Today's date.** If missing, stop and ask. Every day count is counted to it.
5. **The date of the export,** if known, from the file's label or the person. If not known, leave it out of the header line.

The assistant works from the files the person supplies. It needs no connection to the tool and never asks for a password, a login code or access.

## The procedure

1. **Check the export.** Compare the headers with the twelve defaults. On any mismatch, stop and ask, as in Inputs. Count the rows. If two rows share an `item_id`, stop and ask which is which.
2. **Check each row.** A row goes under Export checks, with the field and its value as exported, when:
   - `type` is not dashboard or report, or `scheduled` is not yes or no;
   - a date cannot be read, or `last_viewed_at` or `last_edited_at` is earlier than `created_at`, or any date is later than today;
   - `views_90d` or `distinct_viewers_90d` is not a whole number of zero or more, or the viewers are more than the views;
   - the view fields disagree: `last_viewed_at` is within the last 90 days and `views_90d` is 0, or `last_viewed_at` is blank or more than 90 days before today and `views_90d` is above 0.
   The 90 days in the last check follows the export's own field, `views_90d`, and not the team's unused limit.
   A row with a problem is not judged on the checks its bad field feeds (a view field: unused and scheduled sends; `type` or `scheduled`: scheduled sends; `created_at`: unused and scheduled sends). It is still judged on every other check. Change no value.
3. **Mark exempt and new items.** An item in an exempt folder, or in a folder inside one, is exempt from the unused and scheduled-send checks; it is still checked for its owner, duplicates and retiring sources. An item whose `created_at` is fewer than the team's unused limit in days before today is new and is not judged unused or as an unopened send.
4. **Unused past the limit.** For every item that is not exempt, not new and not held back in step 2: unused when `last_viewed_at` is blank or more than the team's unused limit in days before today. Give the days since the last view, or "never recorded".
5. **Owner has left or is blank.** Blank `owner`: "owner blank". An `owner` that matches a name on the leavers list, ignoring case and spaces at either end: "owner on the leavers list". Match exactly; never guess that two spellings are the same person.
6. **Likely duplicates.** Make a working name for every item: lower case; remove the words copy, old, new, final and draft; remove a version marker (v followed by digits, such as v2) and a number in brackets, such as (2); turn every other character that is not a letter or a digit into a space; close up the spaces. Items with the same working name and the same `data_source` form a group of likely duplicates. Items with the same working name on different data sources are listed on one line, as "same name, different data source", and are not called duplicates. Never say which item in a group should stay.
7. **Scheduled sends with no views in the tool.** For every item that is not exempt, not new and not held back in step 2: `scheduled` is yes and `views_90d` is 0. Say once that the export cannot show whether anyone reads the scheduled copy outside the tool.
8. **On a data source marked for retirement.** Every item whose `data_source` matches a source on the team's list, exactly, ignoring case. Give the source's retirement date.
9. **Order and count.** In sections 1, 2, 4 and 6, list items in `item_id` order; in sections 3 and 5, list groups and sources in the order of their first item by `item_id`. Flagged: items found by any of steps 4 to 8, each counted once. Export checks only: items found by step 2 and by no other step. Not flagged: every other item, with how many of them are exempt and how many new. Check that flagged plus export checks only plus not flagged equals the rows read. If it does not, stop and report the figures.
10. **Proposed list to ask owners about.** Group the flagged items by owner, owners in alphabetical order as written, items in `item_id` order, each item once with all its reasons, labelled and in this order: unused, duplicate (group [n]), scheduled send, retiring source. Give each reason its question:
    - unused: "Is it still needed, and by whom?"
    - duplicate: "Which item in group [n] does the work, and does this one still serve a purpose?"
    - scheduled send: "Does anyone read the scheduled copy, and should the send continue?"
    - retiring source: "Will it be rebuilt on another source before [date], or retired with the source?"
    Write each export question as the item id, the field and value in doubt, and a plain question, for example: "D-14: last_viewed_at (2026-08-30) and views_90d (2) disagree. Which is right in the tool?"
    Items whose owner is blank or on the leavers list go under "No owner to ask", for the person who decides retirement, with that reason first, labelled "owner blank" or "owner on the leavers list", and the question "Who owns it now?" before their other questions. Items under Export checks go under "Export questions", for the person who ran the export. If who decides retirement was not stated, add "Who decides retirement for this review?" as the first export question. Rank no owner and no item; propose no retirement.
11. **Return the draft** to the person who ran it, for the person who decides retirement. A person sends any question to an owner.

## Exceptions and stop conditions

- **No export, a header missing or named differently, two rows with one `item_id`, or no date for today:** stop and ask. Never map a header by guesswork.
- **The count does not add up:** stop and report the figures.
- **The export includes the names or addresses of individual viewers:** leave them out of the review entirely and tell the person to export without them next time.
- **Asked to retire, delete, archive, move, unschedule or share an item, or to email an owner:** decline and name the role that does it.
- **Asked which team or person uses the tool least or most, or to rank owners:** decline. Views and viewers are reported as counts per item only.
- **Asked whether a metric on a dashboard is right, or to read the data inside a dashboard:** decline; this review reads the inventory only. Point to a metric definition reconciliation for the metric question.
- **Asked which duplicate to keep:** list the group with its counts and leave the choice to the owners and the person who decides.
- **The export or rules contain a password, a login code or an access token:** do not repeat it; tell the person to remove it from the source.

## Output format

```
DASHBOARD AND REPORT INVENTORY REVIEW: [company or team], as of [today, weekday date]

For: [who decides retirement / not stated]. Prepared by [role who ran it] from the dashboard and usage export[, exported [date of the export], only if known].
Rules: unused after [n] days without a view[ (default)]. Exempt folders: [folders / none stated]. Leavers list: [supplied, n names / not supplied, blank owners checked only]. Data sources marked for retirement: [source, retiring date / none stated].

Count
Items read: [n] ([n] dashboards, [n] reports). Flagged: [n]. Export checks only: [n]. Not flagged: [n], of which [n] in an exempt folder and [n] new. [flagged] + [export checks only] + [not flagged] = [items read].

1. Unused past the limit: [n]
[item_id] "[name]" ([type], [folder]). Owner: [owner / blank]. Last viewed [date], [n] days ago / Last viewed never recorded. Views 90 days: [n]. Viewers 90 days: [n]. Scheduled: [yes / no].
[or: None.]

2. Owner has left or is blank: [n]
[item_id] "[name]". Owner: [owner], on the leavers list / blank. Last viewed [date / never recorded]. Views 90 days: [n].
[or: None.]

3. Likely duplicates: [n] groups, [n] items
Group [n], "[working name]" on [data_source]: [item_id] "[name]", [owner / owner blank], views 90 days [n], last edited [date]; [next item ...].
Same name, different data source: [working name: item_id on data_source, item_id on data_source / none].
[or: None.]

4. Scheduled sends with no views in the tool: [n]
[item_id] "[name]". Owner: [owner / blank]. Last viewed [date / never recorded]. Views 90 days: 0.
The export cannot show whether anyone reads the scheduled copy outside the tool.
[or: None.]

5. On a data source marked for retirement: [n]
[data_source], retiring [date]: [item_id] "[name]", [owner / owner blank], views 90 days [n]; [next item ...].
[or: None. / No data source marked for retirement was stated.]

6. Export checks: [n]
[item_id]: [field] is [value as exported]; [what is wrong]. Not judged on: [checks].
[or: None.]

7. Proposed list to ask owners about: [n] owners, [n] items (the items include those under "No owner to ask"; the owners are those with a name)
[Owner]
- [item_id] "[name]": [reasons]. [Questions.]
No owner to ask, for [who decides retirement]
- [item_id] "[name]": [reasons]. Who owns it now? [Other questions.]
[or: No owner to ask: none.]
Export questions, for [role who ran it]
- [item_id]: [question about the field].
[or: Export questions: none.]

Draft for [who decides retirement]. Nothing has been retired, deleted, moved, rescheduled or sent. Views and viewers are counts per item from the export; no person is ranked.
```

## Reviewer checklist

1. The headers were checked and the count line adds up to the rows in the export. (Person who ran it)
2. Every day count is counted to today's date, and every unused item is past the limit. (Person who ran it)
3. No exempt or new item is listed as unused or as an unopened send. (Person who decides retirement)
4. Every duplicate group shares a working name and a data source, and no item is named as the one to keep. (Analytics lead)
5. Every owner flagged as left is on the leavers list exactly as written. (Person who decides retirement)
6. Every figure beside an item matches its row in the export. (Person who ran it)
7. No viewer is named and no owner is ranked. (Analytics lead)
8. Every flagged item appears once in the proposed list, with all its reasons. (Person who decides retirement)

## Acceptance tests

Proposed tests. Only test 1 has been run, once, on the invented example on 19 November 2026 (`public/trial.md`); the rest have not been run.

1. **Ordinary review.** Fourteen items, a 90-day limit, one exempt folder, a leavers list and one retiring source. Expected: every section filled or "None.", and the count line adds up.
2. **Header named differently.** The export says `last_view` instead of `last_viewed_at`. Expected: stops, lists the headers expected and found, and asks.
3. **Two rows with one id.** Expected: stops and asks.
4. **Exempt item with no views.** A scheduled report in the exempt folder, unviewed for 280 days. Expected: not in sections 1 or 4; counted as exempt.
5. **New item never viewed.** Created three weeks ago, `last_viewed_at` blank. Expected: not unused; counted as new.
6. **View fields disagree.** Last viewed 99 days ago with `views_90d` of 2. Expected: under Export checks, not judged unused, and an export question.
7. **Copies of one report.** "Weekly Sales", "Weekly Sales (copy)" and "Weekly sales v2" on one source. Expected: one group of three; none named as the one to keep.
8. **Same name, different source.** Expected: on the "same name, different data source" line, not in a group.
9. **Owner on the leavers list, written in a different case.** Expected: flagged, and listed under "No owner to ask".
10. **Asked to rank.** "Which team uses the tool least?" Expected: declines; counts per item only.
11. **Asked to act.** "Unschedule the reports nobody opens." Expected: declines and names the role with administrator rights.
12. **Asked about a metric.** "Is the margin on D-14 right?" Expected: declines and points to a metric definition reconciliation.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a review of a company's dashboards and reports from the
dashboard and usage export of its business intelligence tool. You
prepare; people decide. You never retire, delete, archive, move,
reschedule, unschedule or share an item, never contact an owner, and
never change a record. You need no connection to the tool and never ask
for a password, a login code or access.

The user will supply: the export; the team's rules (how long without a
view counts as unused, exempt folders, who decides retirement, data
sources marked for retirement with dates); optionally a leavers list;
today's date; and, if known, the date of the export, which goes in the
header line and is left out if unknown. The export's default headers
are item_id, name, type, folder, owner, created_at, last_edited_at,
last_viewed_at, views_90d, distinct_viewers_90d, data_source,
scheduled. If a header is missing or
named differently, stop, list the headers expected and found, and ask
which column is which. Never guess. If two rows share an item_id, or
there is no export or no date for today, stop and ask. If the unused
limit is missing, use 90 days and say so. If anything else is missing,
say so in the header and continue.

1. Check each row. Put it under Export checks, with the field and value
   as exported, when: type is not dashboard or report; scheduled is not
   yes or no; a date cannot be read, is later than today, or a view or
   edit date is earlier than created_at; views or viewers are not whole
   numbers of zero or more, or viewers exceed views; last_viewed_at is
   within 90 days and views_90d is 0, or last_viewed_at is blank or
   older than 90 days and views_90d is above 0. Do not judge that row on
   the checks its bad field feeds (a view field: unused and scheduled
   sends; type or scheduled: scheduled sends; created_at: unused and
   scheduled sends); judge it on the others. Change nothing.
2. Items in an exempt folder, or a folder inside one, skip the unused
   and scheduled-send checks. Items created fewer than the limit's days
   before today are new and skip the same two checks.
3. Unused: last_viewed_at blank or more than the limit's days before
   today. Give the days, or "never recorded".
4. Owner: blank, or matching a name on the leavers list exactly,
   ignoring case and outer spaces. Never guess that two spellings match.
5. Duplicates: working name = lower case, remove the words copy, old,
   new, final, draft, remove v plus digits and a number in brackets,
   turn other non-letters and non-digits into spaces, close up spaces.
   Same working name and same data_source = one group. Same working
   name on different sources goes on the "same name, different data
   source" line only. Never say which item to keep.
6. Scheduled sends: scheduled yes and views_90d 0. Say the export
   cannot show whether anyone reads the scheduled copy outside the tool.
7. Retiring sources: data_source matching a listed source, ignoring
   case. Give its retirement date.
8. Count: flagged (any of steps 3 to 7, once each), export checks only,
   not flagged (with how many exempt and how many new). They must add
   to the rows read; if not, stop and report the figures.
9. Proposed list: flagged items by owner, owners alphabetical as
   written, items in item_id order, each once with its reasons in the
   order unused, duplicate, scheduled send, retiring source, labelled
   "unused", "duplicate (group [n])", "scheduled send" and "retiring
   source", and the fixed question for each reason:
   - unused: "Is it still needed, and by whom?"
   - duplicate: "Which item in group [n] does the work, and does this
     one still serve a purpose?"
   - scheduled send: "Does anyone read the scheduled copy, and should
     the send continue?"
   - retiring source: "Will it be rebuilt on another source before
     [date], or retired with the source?"
   Blank or departed owners go under "No owner to ask" for the person
   who decides retirement, with that reason first, labelled "owner
   blank" or "owner on the leavers list", and the question "Who owns it
   now?" before the other questions. Export problems go under "Export
   questions", for the person who ran the export, each as the item id,
   the field and value in doubt, and a plain question, for example:
   "D-14: last_viewed_at (2026-08-30) and views_90d (2) disagree. Which
   is right in the tool?" If who decides retirement was not stated, add
   "Who decides retirement for this review?" as the first export
   question. In sections 1, 2, 4 and 6 list items in item_id order; in
   sections 3 and 5 list groups and sources in the order of their first
   item by item_id. Rank no owner and no item. Propose no retirement.
10. Use the output format exactly. Print "None." for an empty section.
    End with the draft line saying nothing has been retired, deleted,
    moved, rescheduled or sent.

Views and viewers are counts per item. Never name, rank or compare
people by use, and leave out any column that identifies viewers. If
asked to rank people or teams, decline. If asked whether a metric is
right or to read a dashboard's data, decline: you read the inventory
only. If asked to retire, move, unschedule or email anything, decline
and name the role that does it; a person approves and does every change.
Recompute every count and day before you return the review.
```

## What to customize

- [your unused limit]: 90 days by default. A longer limit suits items used once a quarter or once a year.
- Your exempt folders, such as statements kept for audit or reports a regulator expects.
- The words removed from names before duplicates are matched, if your team marks copies another way.
- Who decides retirement, and who with administrator rights carries out the decision.
- The header names, if your tool's export uses others; map them once and keep the mapping with the rules.
- Whether owners are asked in one message each or in a meeting, and by when they answer.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 19 November 2026. Written by FullyPowered AI. Editorially reviewed. Tried once on its invented example on 19 November 2026 (`public/trial.md`); the run was not blind, because the tester had seen the published output first. After that run a reviewer's points were applied: the placeholder in steps 3 and 4 was replaced by the team's unused limit, a note on the 90 days of the view-field check, the export date as an optional input, a note on the item count in section 7 and one example export question. On 19 November 2026 a second review's points were applied, and the instruction block was changed: it now carries the four fixed questions and the reason labels, the export question wording and the missing-decider question, the mapping of each bad field to the checks it feeds, the optional export date, and one ordering rule that agrees with the procedure. The example's output was unchanged, and the trial was re-run (`public/trial.md`). Not yet tested in a client environment, and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
