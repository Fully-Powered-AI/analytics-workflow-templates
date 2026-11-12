---
name: "comparison-claim-check"
description: "Take one claim that a group did better than another, together with the numbers for the two groups, and return a plain page that names the method, gives the size of the difference with a range, checks the assumptions the comparison depends on, and states in ordinary words what the data supports and what it does not. The assistant prepares the reading. It never says a change caused a result unless the groups were assigned at random, never turns a thin result into a confident one, and never decides whether anything should change."
license: "MIT"
metadata:
  version: "0.1.0"
  publisher: "Fully Powered AI"
  template: "Comparison claim check"
---

# Comparison claim check

This is the technical file for a Fully Powered workflow template. It carries the instructions an AI product follows. The complete template, with roles, inputs, exceptions, the reviewer checklist, acceptance tests and what to customize, is in [TEMPLATE.md](TEMPLATE.md). A worked example with invented data is in [EXAMPLE.md](EXAMPLE.md).

## Instructions

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

## Before relying on it

Decide every item under "What to customize" in TEMPLATE.md and set the limits the instructions in this file leave open, written in square brackets such as [N], to your own. Then run the acceptance tests in TEMPLATE.md on past work. A person starts this work, supplies the inputs and decides what happens with the result.
