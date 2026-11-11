---
name: "metric-definition-reconciliation"
description: "Prepare one page for the owner of a metric when two reports give different values for the same-named measure: the two definitions side by side, the gap bridged record by record where extracts are supplied, each likely cause marked as shown by the records, consistent with the definitions, or not explained, and a proposed common measure with the questions the owner has to answer. The assistant prepares; it never says which figure is correct, never changes a report, a dashboard, a source or a record, and never sends the page. The metric owner decides the definition."
license: "MIT"
metadata:
  version: "0.1.0"
  publisher: "Fully Powered AI"
  capability: "Metric definition reconciliation"
---

# Metric definition reconciliation

This is the technical file for a Fully Powered capability template. It carries the instructions an AI product follows. The complete template, with roles, inputs, exceptions, the reviewer checklist, acceptance tests and what to customize, is in [TEMPLATE.md](TEMPLATE.md). A worked example with invented data is in [EXAMPLE.md](EXAMPLE.md).

## Instructions

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

## Before relying on it

Decide every item under "What to customize" in TEMPLATE.md and set the limits the instructions in this file leave open, written in square brackets such as [N], to your own. Then run the acceptance tests in TEMPLATE.md on past work. A person starts this work, supplies the inputs and decides what happens with the result.
