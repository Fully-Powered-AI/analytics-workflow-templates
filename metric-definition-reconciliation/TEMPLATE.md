# Metric definition reconciliation

Workflow template, version 0.1.0.

## Purpose

Prepare one page for the owner of a metric when two reports give different values for the same-named measure: the two definitions side by side, the gap bridged record by record where extracts are supplied, each likely cause marked as shown by the records, consistent with the definitions, or not explained, and a proposed common measure with the questions the owner has to answer. The assistant prepares; it never says which figure is correct, never changes a report, a dashboard, a source or a record, and never sends the page. The metric owner decides the definition.

## When to use it and when not to

Use it when two teams report different values for a metric that carries the same name, or a new tool starts disagreeing with the old one.

Do not use it:

- to find errors inside one workbook. That is spreadsheet check before sharing;
- to track a set of measures month by month. That is the operations KPI scorecard;
- to explain why one measure moved between periods in one report;
- to decide which report is right. The owner decides, from the page.

## Roles

- **Runs it:** an analyst, a finance lead or a report owner.
- **Supplies the definition sheets:** the owner of each report.
- **Decides the common definition:** the named metric owner.
- **Documents the agreed computation:** analytics.
- **Confirms an extract is complete and answers source questions:** the owner of the source system.

## Inputs

1. **The question.** The metric label as each report shows it, the period, and what the figure is used for. If the purpose is missing, continue, and give no proposed measure (step 10).
2. **A definition sheet for each report.** Default field labels, one line each: Report name; Report owner; Metric label; Formula in words; Source; One row is; Included; Excluded; Date field and time zone; Period; Refunds and adjustments; Unit and currency; Refreshed; Notes. If a field is missing, write "not stated" for it and treat it as an open question; never fill it in from a guess. If the formula is missing for either report, stop and ask.
3. **Each report's value for the period,** as shown, with the date it was read. If either is missing, stop.
4. **A record extract for each report, if available.** Default column headers: record_id, record_date, amount, status. One row is one record the report counts, and amount is the amount as the report counts it. Optional extra columns are used when their name matches an element of a definition, such as shipping, tax, refund or currency. If a header does not match the defaults, stop and ask which column is which; never guess. If only one extract is supplied, treat it as no extracts for the row comparison and say so.
5. **Owner notes.** The metric owner's role, earlier decisions, and facts about the business that bear on the choice, such as which time zone the books close in. If missing, write "no owner notes supplied".

The assistant works from the files and notes the person supplies. It needs no connection to any reporting tool and never asks for a password or a login code.

## The procedure

1. **Check the inputs.** Confirm two reports, one period and the same unit and currency. If the reports cover different periods, state it as the first difference and compare rows only after both are pulled for the same period. If the units or currencies differ and no rate is supplied, stop the amount comparison and say why.
2. **Check each extract against its report.** Sum the amount column. It must equal the reported value exactly, in the unit reported. If it does not, say by how much and do not run the row comparison for that pair; still do steps 3, 7, 9, 10 and 11 from the definitions alone. Report only the totals; do not repeat personal names, addresses or contact details that appear in an extract. Refer to records by record_id.
3. **Put the definitions side by side.** Use these ten elements in this order: Source; What one row is; Population included; Exclusions; Date used and time zone; Period boundaries; What is summed; Refunds and adjustments; Unit and currency; Refreshed. Mark each Same, Differs or Not stated in one or both. Quote the text of the sheets; do not paraphrase a definition into a different one. Differs marks a difference in the text; it becomes a cause only when step 6 labels it.
4. **Compare the records.** Match rows by record_id. If a record_id repeats inside one extract, stop the row comparison and ask whether one row is a line rather than a record. Place every record in one of four groups: in both with the same amount; in both with a different amount; only in the first report; only in the second. Total each group. The first report's total, less the group of records only in it, plus the records only in the second, plus the amount differences, must equal the second report's total.
5. **Convert dates when the extracts allow.** If record_date carries a time and an offset or zone, convert it to the other report's zone and check the period boundary. If it carries only a date and the reports use different zones, write "boundary not testable: date only".
6. **Attach a cause to each group and each difference in amount,** using only the causes in this list: date basis or time zone; a status or filter that includes or excludes the record; an amount component (shipping, tax, discount, refund, currency); a repeated record; a different source or refresh date; a different formula, such as a count of records against a count of distinct customers. Label each one:
   - **Shown by the records** when a field in the extract and a stated element of a definition together produce the difference, and the amounts add up;
   - **Consistent with the definitions** when a definition difference could produce it but the records do not show it, for example an amount difference left after the optional columns are used;
   - **Not explained** when neither applies.
   Never label a cause shown because it is likely.
7. **Without extracts,** list the likely causes from the definition differences only, each labelled "from the definitions, not tested on records", with no amounts, and name the extract that would test each.
8. **Build the bridge.** Start at the first report's reported value. Take one step for each group and each cause (an amount labelled consistent with the definitions may be a step, labelled as such): the sign, the amount, the record_ids and the running total. End at the second report's reported value. The steps must add up. Show any remainder as "Unexplained remainder" with its amount, and never adjust a step to make the bridge close. The gap is Report 1 minus Report 2, so a bridge step from Report 1 to Report 2 carries the opposite sign to that cause's effect on the gap; state each cause's effect on the gap with the gap's sign, so the effects net to the gap. One group may be split into steps by cause, and one record's difference may carry two labels, each with its own amount, together equal to the record's difference. A cause that moves records in opposite directions is shown as its parts with their net. When the differences are larger than the net gap, state the total size of the differences beside the gap.
9. **Name what may be right in both.** Where two definitions describe populations or timings that each serve a purpose, say so, and say what each would need to be called to stay apart. Do not retire either. A measure that serves a different purpose is kept apart under its own name, not discarded.
10. **Propose a common measure,** only if the purpose of the figure was supplied. If the reports state different purposes, list each. Propose for the purpose of the report owned by the metric owner when the sheets or owner notes show which that is, say that this is the basis, and ask the metric owner to confirm that this purpose governs; if it cannot be told, write "no proposal: purposes differ and the governing purpose is not stated". For each element where the reports differ, offer the choice that fits the stated purpose, which report uses it today, and the effect on the figure when the records show it. If the purpose was not supplied, give the options for each element and write "no proposal: purpose not stated". Never describe a figure as correct. A figure computed under the proposal is "the sum of the first report's records", not the answer.
11. **Write the questions.** One numbered question for each open item, addressed to a role: the metric owner for each choice of definition, the source owner for each missing fact (when no source owner is named, the owner of the report whose definition uses the fact). Recommend nothing beyond the proposal in step 10.
12. **Return the page** to the person who ran it. The metric owner decides; analytics documents the agreed computation; a person changes any report. The assistant changes none.

## Exceptions and stop conditions

- **Fewer than two reports, or the same report twice:** stop and ask.
- **A formula missing for either report, or either reported value missing:** stop and ask.
- **A header that does not match the defaults:** stop and ask which column is which.
- **An extract that does not sum to its reported value:** no row comparison for that pair; report the difference.
- **A record_id that repeats inside one extract:** stop the row comparison and ask about the grain.
- **A definition that contradicts itself,** such as "excludes cancelled orders" and "all orders": list it as a question for the report owner; do not choose a reading.
- **Asked which number is right, to change a report, a dashboard or a source, to correct a record, or to send the page:** decline and name the role that decides.
- **An extract contains personal details or credentials:** do not repeat them; tell the person to remove them from the file.

## Output format

```
METRIC DEFINITION RECONCILIATION: [metric label], [period]

For: [metric owner role / metric owner not named]. Prepared [date] from [n] definition sheets, [two extracts / no extracts supplied], [owner notes / no owner notes supplied].
Purpose of the figure: [as supplied / not stated].

Reported values
Report 1: [name], owner [role]: [value], read [date].
Report 2: [name], owner [role]: [value], read [date].
Gap: [value], Report 1 minus Report 2. [Differences found total [absolute sum] in size and, taken as effects on the gap, net to it.]

Side by side
Source: Report 1 [text]. Report 2 [text]. [Same / Differs / Not stated in one or both]
What one row is: ...
Population included: ...
Exclusions: ...
Date used and time zone: ...
Period boundaries: ...
What is summed: ...
Refunds and adjustments: ...
Unit and currency: ...
Refreshed: ...

Row comparison [or: Row comparison: not done, [reason].]
Extract check: Report 1 [n] rows sum to [value] ([ties / does not tie: difference]). Report 2 [n] rows sum to [value] ([ties / does not tie: difference]).
Duplicate record ids: none. [If any: the ids, and the row comparison stops here.]
In both, same amount: [n] records, [total].
In both, different amount: [n] records ([ids]). Report 1 [total], Report 2 [total], difference [value].
Only in Report 1: [n] records ([ids]), [total].
Only in Report 2: [n] records ([ids]), [total].

Bridge from Report 1 to Report 2 [or: Bridge: not built, [reason].]
Report 1 reported: [value]
[Step]: [+/- amount] ([ids]) = [running total]
Report 2 reported: [value]. Unexplained remainder: [amount].

Likely causes
Shown by the records: [n]. [Cause, ids, effect on the gap, the field and definition element that show it.] [or: none]
Consistent with the definitions, not shown by the records: [n]. [Cause, ids, effect on the gap, what would confirm it.] [or: none]
Not explained: [n]. [What is left, with the amount.] [or: none]
[Without extracts: Likely causes from the definitions, not tested on records: each cause and the extract that would test it.]

What may be right in both
[Each case, with the separate names it would need.] [or: nothing identified.]

Proposed common measure
[Metric label as proposed.] Basis: [the purpose of the figure / no proposal: purpose not stated.]
[Element]: [choice]. Today: [Report 1 / Report 2 / neither]. Effect: [amount on the records, with the sign of the gap / not computable from the records].
Under the proposal the sum of Report [n]'s records is [value]. This is not confirmed as correct: the owner has not yet chosen the definition.

Questions before the metric owner decides: [n]
[n]. For [role]: [question].

Draft for the [metric owner role]'s decision. Nothing has been changed, sent or published, and no figure is declared correct.
```

## Reviewer checklist

1. Each extract's total equals its reported value, or the page says it does not. (Analyst)
2. The bridge adds up from Report 1's value to Report 2's, and any remainder is shown. (Analyst)
3. Every cause labelled "shown" has a field in the extract and a stated element of a definition behind it, and the amounts add up. (Analyst)
4. The side-by-side quotes the definition sheets and invents no field. (Report owners)
5. No sentence says one figure is correct. (Metric owner)
6. The proposal rests on the stated purpose, and keeps separate any measure that serves a different purpose. (Metric owner)
7. Every open item is a question addressed to a role. (Analyst)
8. No personal detail from an extract appears on the page. (Analyst)

## Acceptance tests

Proposed tests. None has been run.

1. **Offsetting differences.** Two extracts whose net gap is small and whose record differences are large. Expected: the gap line states both, and the bridge closes.
2. **Time-zone boundary.** A record placed late on the last day of the month in one zone. Expected: shown as a date-basis cause, in the right report's month, with the converted time.
3. **Date only.** The same record with a date and no time, and the reports using different zones. Expected: "boundary not testable: date only".
4. **Extract does not tie.** An extract that sums to 40 more than its report. Expected: no row comparison for that pair; the difference reported; the definitions still compared.
5. **Header mismatch.** A column named "total" in place of amount. Expected: stops and asks which column is which.
6. **Amount difference with no optional column.** Expected: labelled consistent with the definitions, not shown, with what would confirm it.
7. **Repeated record id.** Expected: row comparison stops and the grain is asked about.
8. **No extracts.** Expected: causes from the definitions only, labelled not tested, no amounts, and the extract named that would test each.
9. **No purpose stated.** Expected: options for each element and "no proposal: purpose not stated".
10. **Both reports legitimate.** Expected: both kept, with separate names proposed.
11. **Asked which number is right.** Expected: declines and names the metric owner.
12. **Missing formula.** Expected: stops and asks.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a metric definition reconciliation for the owner of a metric,
from two reports that give different values for the same-named measure.
You prepare; people decide. You never say which figure is correct, change
a report, dashboard, source or record, or send anything. The metric owner
decides the definition. You never ask for a password or a login code and
need no access to any system.

The user will supply: the metric and period and what the figure is used
for; a definition sheet for each report (report name, report owner,
metric label, formula in words, source, one row is, included, excluded,
date field and time zone, period, refunds and adjustments, unit and
currency, refreshed, notes); each report's value and the date it was
read; optionally a record extract for each report with the headers
record_id, record_date, amount, status (extra columns such as shipping,
tax or refund are used when they match a definition element); and the
owner's notes. If a formula or a reported value is missing, stop and
ask. If a header does not match, stop and ask which column is which. If
another field is missing, write "not stated" and treat it as a question.
Never guess a missing field.

1. Check one period, one unit and one currency. If the periods differ,
   say so first and compare rows only for the same period. If the units
   or currencies differ and no rate is supplied, stop the amount
   comparison and say why.
2. Sum each extract and compare with its reported value exactly, in the
   unit reported. If they differ,
   report the difference, skip the row comparison for that pair, and
   continue from the definitions. If only one extract is supplied, treat
   it as no extracts for the row comparison and say so. Refer to records
   by record_id; do not repeat personal details. If an extract contains
   personal details or credentials, do not repeat them and tell the
   person to remove them from the file.
3. Side by side, in this order: source; what one row is; population
   included; exclusions; date used and time zone; period boundaries;
   what is summed; refunds and adjustments; unit and currency;
   refreshed. Quote the sheets. Mark each Same, Differs or Not stated in
   one or both. Differs marks a difference in the text; it is a cause
   only when step 6 labels it. If a definition contradicts itself, such
   as "excludes cancelled orders" and "all orders", list it as a question
   for the report owner and do not choose a reading.
4. Match rows by record_id into four groups: in both with the same
   amount, in both with a different amount, only in the first, only in
   the second. Total each. If a record_id repeats within an extract,
   stop the row comparison and ask about the grain.
5. Convert dates to the other report's zone when the extract has a time
   and an offset. If it has a date only and the reports use different
   zones, write "boundary not testable: date only".
6. Attach a cause to each group and each difference in amount, using only
   these causes: date basis or time zone; a status or filter that
   includes or excludes the record; an amount component (shipping, tax,
   discount, refund, currency); a repeated record; a different source or
   refresh date; a different formula, such as a count of records against
   a count of distinct customers. Invent no other category. Label each
   one. Shown by the records: a field in the extract and a stated
   definition element produce it and the amounts add up. Consistent with
   the definitions: a definition difference could produce it but the
   records do not show it. Not explained: neither. Never call a cause
   shown because it is likely.
7. Without extracts, give likely causes from the definitions only, each
   labelled "from the definitions, not tested on records", with no
   amounts, and name the extract that would test each.
8. Build the bridge from Report 1's value to Report 2's, one step per
   group or cause, with ids and running total. A group may be split into
   steps by cause, and one record's difference may carry two labels with
   an amount each. A cause that moves records in opposite directions is
   shown as its parts with their net. An amount labelled consistent with
   the definitions may be a step, labelled as such. Show any remainder
   as "Unexplained remainder". Never adjust a step to make it close. The gap is Report 1 minus Report 2, so
   a bridge step carries the opposite sign to that cause's effect on the
   gap; state each cause's effect on the gap with the gap's sign. State
   the total size of the differences beside the gap when it is larger
   than the gap.
9. Say where both reports may be right, and what each would be called to
   stay apart. Do not retire either.
10. Propose a common measure element by element only if the purpose of
    the figure was supplied. If the reports state different purposes,
    list each, propose for the purpose of the report owned by the metric
    owner when the sheets or notes show which that is, say that this is
    the basis, and ask the owner to confirm it; if that cannot be told,
    write "no proposal: purposes differ and the governing purpose is not
    stated". If no purpose was supplied, give options for each element
    and write "no proposal: purpose not stated". Never call a figure
    correct; a figure under the proposal is "the sum of Report n's
    records", not the answer.
11. End with numbered questions, each for a named role: the metric owner
    for each choice of definition, the source owner for each missing
    fact (when none is named, the owner of the report whose definition
    uses the fact). Recommend nothing beyond the proposal.

Use the output format exactly. Every figure must come from the sheets or
the extracts; check each sum and the bridge before you return the page.
If there are fewer than two reports, or the same report twice, stop and ask. If
asked which number is right, to change a report, dashboard or source, to
correct a record, or to send the page, decline and name the role that
decides.
```

## What to customize

- The fields on your definition sheet, and who fills each one in.
- The default extract headers, and the optional columns you will add for amount components such as shipping, tax, refund and currency.
- Who owns each shared metric, and who documents the agreed computation.
- The cause list in step 6, if your reports have causes of their own, such as a fiscal calendar or a currency rate date.
- Where agreed definitions are kept, and what a separate measure must be called.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Editorially reviewed. Tried on its invented example in Claude on 10 November 2026; the record is published with it. Not yet tested in a client environment, and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
