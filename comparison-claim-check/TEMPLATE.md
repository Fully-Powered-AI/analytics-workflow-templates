# Comparison claim check

Workflow template, version 0.1.0.

## Purpose

Take one claim that a group did better than another, together with the numbers for the two groups, and return a plain page that names the method, gives the size of the difference with a range, checks the assumptions the comparison depends on, and states in ordinary words what the data supports and what it does not. The assistant prepares the reading. It never says a change caused a result unless the groups were assigned at random, never turns a thin result into a confident one, and never decides whether anything should change.

## When to use it and when not to

Use it when two groups are compared on one outcome and someone is about to believe or act on the difference: a page or offer test, a pilot in one branch against another, a before-and-after in separate groups, a process change.

Do not use it for the following.

- Comparing more than two groups at once, or the same people measured twice (before and after). This version compares two separate groups.
- Reviewing why deals were won or lost, which is win-loss review.
- Grouping what customers say, which is customer feedback themes.
- Planning how large a test should be, forecasting, or choosing what to test.
- Claims where the outcome is a health or safety result, or where the answer will be used for a legal or hiring decision. Say so and decline.

## Roles

- **Starts it and supplies the inputs:** the analyst, manager or owner who holds the claim.
- **Checks the figures:** an analyst, who recomputes the result and the checks.
- **Decides what to do:** the business owner. The assistant never does.

## Inputs

1. **The claim,** in the words it was made, naming which group is said to be better and on which outcome. If it does not name both, stop and ask.
2. **The data,** in one of two forms.
   - A summary per group. For a yes-or-no outcome, default headers `group`, `n`, `successes`. For a numeric outcome, default headers `group`, `n`, `mean`, `sd`, and `median` if available.
   - One row per record. Default headers `group`, `outcome`. Optional: `unit_id`, `date`, `segment`.
   If a header does not match these, stop and ask which column is which. Do not guess. There must be exactly two distinct group labels; if there are more or fewer, stop.
3. **How the groups were formed:** assigned at random by a system, chosen by people, or different periods or places. If not supplied, treat as unknown, which counts as not random.
4. **The outcome definition:** what counts as success or what the number measures, the period, and what one row stands for (a person, a visit, an order). If the unit is not supplied, ask once; if still unknown, note it under "Each unit counted once".
5. **Comparisons and stopping:** how many comparisons were looked at on this outcome (the claim included), and whether anyone watched the results and stopped when they looked good. If the number of comparisons is not supplied it is unknown: flag it under check 5 and the support level cannot be higher than "Points the same way but is not strong enough to rely on".
6. **The planned split between groups,** if there was one. Default: equal.
7. **The smallest difference that would matter** to the business, if known. Optional.

## The procedure

1. **Check the claim can be answered.** Two groups, one outcome, and an outcome in the data that matches the claim. If not, stop and say what is missing.
2. **Check the records.** For record rows, count rows per group and rows with no outcome. For summaries, check successes are not more than n. If any group has fewer than 10 records, do not run a test; give the plain figures, set the support level to "Cannot be assessed from this data" and explain.
3. **Choose the method.**
   - Yes-or-no outcome: the difference between two rates. If either group has fewer than 10 yes or fewer than 10 no, use an exact test (Fisher's) and name the routine used for the interval.
   - Numeric outcome: Welch's comparison of two means. Report each group's mean, spread and median. If either group has fewer than 30 records, or its mean and median differ by more than half a standard deviation, also report the difference in medians with a rank-based test or a bootstrap interval, and base the reading on the more cautious of the two. If the numeric outcome was supplied only as a summary (group, n, mean, sd), the rank-based test and the bootstrap cannot be calculated: report the medians if they were supplied, say that the second test cannot be run from a summary, and read the result cautiously.
   Say in one sentence why the method fits.
4. **Calculate.** Use code or a spreadsheet's functions; never estimate by eye. If the assistant cannot calculate, stop and say so. Report: each group's rate or mean; the difference, claimed-better group minus the other; the relative difference; a two-sided p-value to three decimals; an effect size (Cohen's h for rates, which is 2 times the arcsine of the square root of one rate minus 2 times the arcsine of the square root of the other, reported as a positive number when the claimed-better group is higher; Cohen's d with the pooled standard deviation for numbers) with the conventional labels (0.2 small, 0.5 medium, 0.8 large; below 0.2 is "below the conventional small"). For rates use the difference plus or minus 1.96 times the square root of each rate times its complement over its n, summed, and a z-test on the pooled rate.
5. **Allow for repeated comparisons.** Let k be the number of comparisons looked at on this outcome. Compare the p-value with 0.05 divided by k, and give the interval at a level of 100 times (1 minus 0.05 over k) per cent. For k of 1 this is the usual 95%. For k above 1, the multiplier 1.96 becomes the matching normal quantile, the z value that leaves 0.025 divided by k in each tail. If k is not supplied, treat it as unknown: show the figures for k of 1, say that k was not supplied, flag it under check 5, and cap the support level in step 7.
6. **Run the assumption checks,** and mark each Pass, Flag or Cannot check, with one line of reason.
   1. *Groups formed:* Pass only for random assignment by a system. Otherwise Flag: the result is an association and no cause is claimed.
   2. *Split against plan:* test the group sizes against the planned split with a chi-square on the counts. Flag if p is under 0.01: the assignment may be faulty and the result should not be relied on.
   3. *Size and shape:* the checks in step 3.
   4. *Each unit counted once:* Flag if the same person, browser or account can appear more than once, or if `unit_id` repeats; give how many repeats if known. Do not remove them silently. An overlap between the groups that is possible but not known is a Flag here; an overlap that is known is a stop condition.
   5. *Early looking and repeated comparisons:* Flag if results were watched and the test stopped early, or the length was not fixed in advance, or the number of comparisons (k) was not supplied.
   6. *Same conditions:* Flag if the groups ran over different periods, places or populations, or if anything other than the change differs between them that the person has mentioned.
   7. *Missing or extreme values:* report missing outcomes by group; with summary data, missing outcomes cannot be seen, so mark Cannot check, or Pass only when the person has said none are missing, giving that statement as the reason; Flag if over 5% in either group. For numbers in record rows, name any value more than 5 standard deviations from its group's mean, and show the result with and without it. Never remove it from the main result. With summary data the 5-standard-deviation check is Cannot check.
7. **Choose the support level.** Exactly one of four phrases.
   - **Supports the claim, within the limits below:** the p-value is under 0.05 over k, the interval at that level excludes zero in the direction claimed, k was supplied, and checks 1 (groups formed), 2 (split against plan), 5 (early looking and repeated comparisons) and 6 (same conditions) have no Flag.
   - **Points the same way but is not strong enough to rely on:** the observed difference is in the direction claimed, but the interval includes zero, or the p-value is not under 0.05 over k, or k was not supplied, or one of checks 1, 2, 5 or 6 is flagged.
   - **Does not support the claim:** the observed difference is zero or in the opposite direction.
   - **Cannot be assessed from this data:** a stop condition applies.
   Flags on checks 4 and 7 do not lower the level; name them in the limits.
8. **Say what it means in business terms.** Give the difference per 1,000 units for rates, or in the outcome's own units for numbers, with the interval. If the smallest meaningful difference was supplied, say whether the whole interval is above it, straddles it or is below it. If not, write "smallest meaningful difference not supplied" and leave that judgement to the person.
9. **Write what the data supports,** in two to four plain sentences using the figures. If the lower end of the interval is under a tenth of the observed difference, say the margin is narrow. Use "was higher", "is consistent with" and "was associated with". Use "because of" or "caused" only for random assignment, and still not for why. Never write "proves", "significant" without the number beside it, or "confirms".
10. **Write what it does not support.** Always include: other periods and groups, the reason for the difference, and any forecast. Add whatever the flags and the unsupplied inputs rule out.
11. **List questions for the person,** at most five, each one something whose answer could change the reading. If the person asked whether to roll out, buy or stop something, the first question says that the decision is theirs and this check does not make it. Then write one sentence of report wording that stays inside the data.
12. **Return it to the person who asked,** with the trace line.

## Exceptions and stop conditions

- **Header does not match the defaults, or more or fewer than two groups:** stop and ask.
- **The outcome in the data is not the outcome in the claim:** stop and say which differs.
- **A group has fewer than 10 records:** no test; plain figures only.
- **The same people are known to appear in both groups, such as a before-and-after on the same customers:** stop and say this version compares separate groups. (If an overlap is only possible, flag it under check 4.)
- **The assistant cannot calculate:** stop; never estimate.
- **Asked to leave out records, change the groups or choose a different test until the result becomes significant:** decline. A change of method after seeing the result is written in the output as a limit, and the original reading stays.
- **Asked whether to roll out, buy or stop something:** decline; set out the support level and the questions, with the decline as the first question, and leave the decision to the person.
- **The claim is a health or safety result, or feeds a legal or hiring decision:** decline.
- **A flag on check 2:** state that the result should not be relied on, whatever the numbers show.

## Output format

```
COMPARISON CLAIM CHECK: [claim in a short phrase]

Support level: [one of the four phrases].

The claim: [as given; which group is said to be better, on which outcome].

What was compared: Group [A]: [n], [successes or mean]. Group [B]: [n], [successes or mean]. Outcome: [definition, and what one row stands for]. Period: [dates, or "dates not supplied"]. Groups formed by: [how].

Method used: [method, and the one-sentence reason it fits].

Result: [Group A rate or mean] against [Group B]. Difference ([claimed-better] minus [other]): [amount], a relative difference of [%]. [level]% interval: [low] to [high]. p-value [x], compared with [0.05 over k]. Effect size: [h or d], [conventional label]. In business terms: [per 1,000 units or in units], interval [low] to [high]. Smallest meaningful difference: [amount or "not supplied"].

Assumption checks:
- Groups formed: [Pass/Flag/Cannot check]. [reason]
- Split against plan: [Pass/Flag/Cannot check]. [reason, with chi-square and p]
- Size and shape: [Pass/Flag/Cannot check]. [reason]
- Each unit counted once: [Pass/Flag/Cannot check]. [reason]
- Early looking and repeated comparisons: [Pass/Flag/Cannot check]. [reason]
- Same conditions: [Pass/Flag/Cannot check]. [reason]
- Missing or extreme values: [Pass/Flag/Cannot check]. [reason]

What the data supports: [two to four sentences].

What it does not support:
- [item]

Questions for you:
1. [question, or "None."]

Suggested wording for a report: "[one or two sentences]"

Every figure was calculated from the data supplied, using [tool or method]. Nothing has been changed or sent, and whether to act is yours to decide.
```

Print every heading in the format. Where a section has nothing to report, write "None." under it. The method, result and checks lines are never left empty; if they cannot be completed, the support level is "Cannot be assessed from this data" and the lines say why.

## Reviewer checklist

1. Every figure in the result line recomputes from the data supplied. (Analyst)
2. The method fits the outcome, and the reason given is true of this data. (Analyst)
3. The interval and p-value use the adjusted level when more than one comparison was made. (Analyst)
4. Each check is marked from the facts supplied, and unsupplied facts are not marked Pass. (Analyst)
5. The support level follows the rule in step 7 and nothing stronger. (Analyst)
6. No sentence implies cause for groups that were not assigned at random. (Analyst)
7. "What it does not support" names every limit the flags and gaps create. (Business owner)
8. The decision is left with the business owner. (Business owner)

## Acceptance tests

Proposed tests. Test 1 was run on 10 November 2026 and its record is published with the template; the others have not been run. The block was amended after that run in small ways that do not change test 1's expected figures.

1. **Fair test, thin margin.** A 4,020 visitors, 482 orders; B 3,980 and 537; random; one comparison. Expected: B 13.49%, A 11.99%, difference 1.50 points, interval 0.04 to 2.96, p 0.044; the margin called narrow.
2. **No real difference.** A 5,000 and 500 orders; B 5,000 and 510. Expected: "Points the same way but is not strong enough to rely on"; interval includes zero.
3. **Opposite direction.** B below A. Expected: "Does not support the claim".
4. **Split does not match the plan.** Planned half and half; A 5,400, B 4,600. Expected: check 2 flagged, p under 0.01, a warning that the result should not be relied on.
5. **Groups chosen by people.** Branch X against branch Y, chosen by the managers. Expected: check 1 flagged, level at most "Points the same way…", wording says "associated with", never "caused".
6. **Three comparisons tried.** Same data as test 1 with k of 3. Expected: p 0.044 compared with 0.0167, level "Points the same way…".
7. **Small group.** One group of 8 records. Expected: no test, "Cannot be assessed from this data".
8. **Header mismatch.** Columns named "arm" and "converted?". Expected: stops and asks which is which.
9. **Pressure to find a result.** "Drop the first two days and rerun." Expected: declines; says a change made after seeing results is a limit.
10. **Number of comparisons not supplied.** Same data as test 1, k not given. Expected: check 5 flagged, and the level is "Points the same way but is not strong enough to rely on" although p is 0.044.
11. **Asked to decide.** Test 1 data with "Can we switch everyone over?". Expected: the first question says the decision is the person's and the check does not make it.

## Instructions for the AI assistant

```
You check a comparison claim for the person who holds it. You never
change records, send anything, or decide what to do about the result.

The user supplies: the claim; the data for exactly two groups (a summary
with headers group, n, successes, or group, n, mean, sd, median; or rows
with headers group, outcome); how the groups were formed; the outcome
definition and what one row stands for; how many comparisons were
looked at and whether anyone stopped early; the planned split; and
optionally the smallest difference that matters. If a header does not
match, if there are not exactly two groups, if the outcome in the data
is not the outcome in the claim, or if the same people are known to be
in both groups, stop and ask. If the outcome is a health or safety
result, or the answer will feed a legal or hiring decision, decline. If you cannot calculate, stop and say so; never
estimate a figure.

1. Check the claim can be answered with this data. If a group has fewer
   than 10 records, run no test, show plain figures, and set the level
   to "Cannot be assessed from this data".
2. Yes-or-no outcome: difference between two rates (use an exact test if
   any cell is under 10). Numeric outcome: Welch comparison of means; if
   a group is under 30 or its mean and median differ by more than half a
   standard deviation, also report medians and read the more cautious.
   From a summary alone (no rows) the rank-based test and bootstrap
   cannot be run: give the medians if supplied, say the second test
   cannot be run from a summary, and read the result cautiously.
3. Calculate each group's rate or mean, the difference (claimed-better
   minus other), the relative difference, a two-sided p-value to three
   decimals and an effect size (Cohen's h or d) with its conventional
   label (0.2 small, 0.5 medium, 0.8 large; below 0.2 is "below the
   conventional small").
   (Cohen's h is 2 x asin(sqrt(rate 1)) - 2 x asin(sqrt(rate 2)).)
4. Let k be the number of comparisons looked at. Compare p with 0.05/k
   and give the interval at 100 x (1 - 0.05/k) per cent, replacing 1.96
   with the normal quantile that leaves 0.025/k in each tail. If k was
   not supplied, show k of 1, say so, and flag it in check 5.
5. Mark seven checks Pass, Flag or Cannot check: groups formed (Pass only
   for random assignment); split against plan (chi-square, Flag if p is
   under 0.01); size and shape; each unit counted once; early looking;
   same conditions; missing or extreme values (flag over 5% missing in
   either group; for rows, name any value over 5 standard deviations
   from its group's mean and show the result with and without it, never
   removing it from the main result; from a summary that check is Cannot
   check). Unsupplied facts are never
   Pass (a summary cannot show missing values: Cannot check, unless the
   person says none are missing). Possible overlap between the groups is
   a Flag in check 4; known overlap is a stop. Check 5 is named "early
   looking and repeated comparisons" and is flagged if k was not given.
6. Support level, one of four: "Supports the claim, within the limits
   below" (p under 0.05/k, interval excludes zero in the claimed
   direction, k supplied, and the checks groups formed, split against plan,
   early looking and repeated comparisons, and same conditions not
   flagged); "Points the same way but is not strong enough to rely on"
   (also the level when the interval includes zero, p is not under
   0.05/k, or k was not supplied); "Does not support the claim"; "Cannot
   be assessed from this data".
7. Say what the data supports in two to four plain sentences. Call the
   margin narrow if the interval's lower end is under a tenth of the
   difference. Use "was higher", "is consistent with", "was associated
   with". Use "caused" only for random assignment and never for why.
   Never write "proves" or "confirms", and never write "significant"
   without the number beside it.
8. Say what it does not support: other periods and groups, the reason,
   any forecast, and what the flags rule out. Also give the difference
   per 1,000 units for rates, or in the outcome's own units for numbers,
   with the interval, and say whether it clears the smallest difference
   if one was supplied. Add at most five questions
   for the person (if they asked whether to act, the first question says
   that is theirs to decide) and one sentence of report wording.
9. Use the output format exactly. Where a section is empty write "None.".
   End with the trace line.

If asked to drop records, change groups or switch tests until the result
looks better, decline. If asked whether to act, decline and leave the
decision to the person.
```

## What to customize

- Your usual interval and the smallest difference that matters, by area.
- The unit you count by for your main outcomes.
- The wording of the four support levels, if your team prefers its own, while keeping their meanings.
- Who must read the page before a result is quoted outside the team.
- Which exports and calculation tools the assistant may use in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Run twice on its invented example in Claude on 10 November 2026, both by the session that wrote and revised it, so neither run was blind; the record of the second run is published beside it. The instruction block was amended afterwards in small ways (the health, safety, legal and hiring decline, summary-only numeric outcomes, the support-level rule for a p-value not under 0.05 over k, and several rules restated that the block had left out) and not re-run. Not yet tested in a client environment.
