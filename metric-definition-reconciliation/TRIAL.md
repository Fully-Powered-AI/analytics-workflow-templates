# Metric definition reconciliation: one trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs are the invented example in [example.md](example.md): an invented online garden-tools shop, October 2026 "Net sales" of 695.00 in the monthly management report and 692.00 on the campaign dashboard. No client data was used.

This is the second run. An earlier run, the same day, produced the first record; the template's pasted instructions, its output format and the example's page were then edited after an independent review, so that run no longer describes the current text. This record replaces it and describes a fresh run on the edited text.

The model that ran this did not write the template, but it is the model that applied the review's edits, and it had read the example file, inputs and published page together, before it began. It worked every figure from the two definition sheets and the two extracts and checked each sum and the bridge itself, but this is not a blind run, and the match with the published page should be read with that in mind. The published page's wording was edited in the same pass to follow the revised rules (signs on effects, the placement of the duplicate-ids line, the labels and the question roles); the groups, the causes and the bridge figures were not changed.

After this run, three small edits were made and the run was not repeated: the example's question input gained a run date line ("Run date: 10 November 2026"), the pasted instructions gained the rule that a cause moving records in opposite directions is shown as its parts with their net and the sentence that an amount labelled consistent with the definitions may be a bridge step, and the pasted step 2 gained "exactly, in the unit reported". Judgement point 3 below describes the template as it stood during the run; the added sentence now answers it. The recorded output and observations are unchanged.

## Inputs used

All seven inputs in the example, by reference: the question, the two definition sheets, the two reported values, the two extracts (six rows and seven rows), and the owner note that the finance lead owns the metric and that statements close on Pacific time.

## What came out

The page followed the output format section by section. Its substance:

- **Gap:** 3.00, Report 1 minus Report 2. The differences found total 297.00 in size and, taken as effects on the gap, net to it: +95.00 (date basis), -30.00 (test order), -37.00 (shipping), -25.00 (refund on 1004, consistent only).
- **Extract check:** Report 1's six rows sum to 695.00 and Report 2's seven rows sum to 692.00; both tie. Duplicate record ids: none, printed on the line after the extract check.
- **Side by side:** same for what one row is and for unit and currency; different for the other eight elements.
- **Row comparison:** no record is in both with the same amount. Five records (1001 to 1005) are in both with different amounts (Report 1 545.00, Report 2 607.00, difference 62.00). Order 1006 (150.00) is only in Report 1. Orders 1007 (55.00) and 1008 (30.00) are only in Report 2.
- **Bridge, in the direction Report 1 to Report 2:** 695.00, less 150.00 for 1006 = 545.00; plus 55.00 for 1007 = 600.00; plus 30.00 for 1008 = 630.00; plus 37.00 shipping on 1001 to 1005 = 667.00; plus 25.00 on 1004 = 692.00. Unexplained remainder 0.00. Each bridge step has the opposite sign to the cause's effect on the gap.
- **Shown by the records (3):** the date basis (net effect on the gap +95.00); the test order 1008 (-30.00); shipping (-37.00).
- **Consistent with the definitions, not shown (1):** 25.00 on part-refunded order 1004, probably a refund that Report 1 deducts and Report 2 does not (-25.00 on the gap if confirmed). The refund amount was not supplied.
- **Not explained:** none. The Source and Refreshed differences are marked Differs but no record shows an amount for them, so none is attributed.
- **What may be right in both:** Report 2 is consistent with its own definition; a measure of order value including shipping, before refunds and counting test orders as the feed stands, could serve campaign tracking under its own label.
- **Proposed common measure:** Net sales on Report 1's definition. The reports state different purposes; the model followed the purpose of the report owned by the metric owner (the finance lead owns Report 1 and the metric), said so, and asked the finance lead to confirm it. Under the proposal the sum of Report 1's records is 695.00, stated as not confirmed as correct.
- **Questions (4):** two for the finance lead, one for the marketing lead, and one on the order 1004 refund, addressed to the finance lead as owner of Report 1, which deducts refunds.
- The page ended with the required line that nothing was changed, sent or published and no figure was declared correct.

## What was observed

- **Every required part was produced.** Nothing in the instructions made the model stop: the formulas, reported values and headers were all present, the extracts tied, and no id repeated.
- **Figures.** Every sum, group total and bridge step matched the published page. All figures trace to the inputs.
- **Differences from the published example.** None in the groups, causes, labels, signs or bridge. Small wording choices differ.
- **Facts not in the inputs.** The refund of 25.00 on order 1004 is inferred from the gap left after shipping; the template labels it as not shown. The suggested label for the dashboard's measure is a suggestion, not an input.

### Where the instructions still needed judgement

1. **Quote form.** The format shows "Report 1 [text]" without saying whether to quote the whole field. The model quoted the field text.
2. **Which purpose governs.** The new rule for differing purposes is followed by the owner-of-the-report test. It worked here because the finance lead owns both Report 1 and the metric; where the metric owner owns neither report, the rule gives "no proposal", which this run did not exercise.
3. **Records that are not in the extract's own terms.** The refund on 1004 is only inferred from the leftover amount; the template does not say whether the 25.00 may be shown as a bridge step before the refund is confirmed. The model showed it as a step labelled consistent with the definitions, which the bridge rule allows.

### Shortcomings

- The trial is one run, by one model, on one invented example, and not a blind run (see above).
- The template's own acceptance tests, such as a date-only extract, a header mismatch, a unit difference with no rate and a missing formula, were not exercised. Only the main path was. The pasted instructions were checked against the output format by reading, not by a run of those cases.
- Nothing here shows how the template behaves on a real client's extracts, which are larger and messier.
