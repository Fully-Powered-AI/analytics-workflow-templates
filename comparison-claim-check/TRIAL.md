# Comparison claim check: trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs are the invented example in `public/example.md` (the Shop X checkout test): the claim, the two-row summary, and the notes from the person. No client data was used. This is the second run. The first run, on the template as first written, found gaps in it (no home for an unknown number of comparisons, no place for a decline, no rule for missing values in a summary, overlap between groups, no formula for Cohen's h); the template was revised to close them, and this run is on the revised template. It was done by the same session that made the revisions, so it is not an independent run. The session had read the example's output before this run, and the output below starts from the first run's text, changed only where the revised template requires (the check 5 name, the Cannot check for missing values, the Cohen's h formula); the figures were recomputed. Treat it as a check that the revised template still yields a conforming page, not as a blind trial.

## What came out

The assistant followed the instruction block and the output format in `member/template.md`. The figures were recalculated with Python's standard library (no statistics package was installed), using the formulas the template names.

**COMPARISON CLAIM CHECK: new checkout page (B) converts better than the old (A)**

**Support level:** Supports the claim, within the limits below.

**The claim:** Version B has a higher share of checkout visitors who place an order than version A.

**What was compared:** Group A: 4,020 visitors, 482 orders. Group B: 3,980 visitors, 537 orders. Outcome: a visitor who reached the checkout placed an order in the same visit; one row stands for a browser. Period: the same 14 days for both (dates not supplied). Groups formed by: random assignment on first visit by the shop's testing tool.

**Method used:** Difference between two rates, with a 95% interval and a z-test on the pooled rate. It fits because the outcome is yes or no and every cell (orders and non-orders in each group) is at least 10, so no exact test is needed.

**Result:** A 11.99% against B 13.49%. Difference (B minus A): 1.50 percentage points, a relative difference of 12.5%. 95% interval: 0.04 to 2.96 points. p-value 0.044, compared with 0.05 for one comparison. Effect size: Cohen's h 0.045 (2 x asin(sqrt(0.1349)) - 2 x asin(sqrt(0.1199))), below the conventional small. In business terms: about 15 more orders per 1,000 visitors, interval 0.4 to 29.6. Smallest meaningful difference: not supplied.

**Assumption checks:**

- Groups formed: Pass. Random assignment by a system.
- Split against plan: Pass. 4,020 and 3,980 against a planned half and half; chi-square 0.20, p 0.655.
- Size and shape: Pass. Orders 482 and 537, non-orders 3,538 and 3,443, all at least 10.
- Each unit counted once: Flag. Counting is per browser, so a person on two devices can be counted twice, and could even have been given A on one device and B on the other. How many is not known.
- Early looking and repeated comparisons: Pass. The length was fixed in advance, nobody looked before the end, and one comparison was made.
- Same conditions: Pass. Both versions ran over the same 14 days, including the week-two sale for everyone.
- Missing or extreme values: Cannot check. A summary cannot show missing outcomes and the notes do not say none are missing; there are no numeric values to check. This does not lower the support level.

**What the data supports:** In these 14 days, 13.49% of visitors on version B placed an order against 11.99% on version A, a gap of 1.50 points. Visitors were assigned at random, so the gap can be read as an effect of the version shown. The margin is narrow: the lower end of the interval, 0.04 points, is under a tenth of the observed gap, so the true gain could be close to nothing or nearly 3 points.

**What it does not support:**

- That B will do as well in other weeks, on other traffic or without a sale running.
- Why B does better, or which change on the page is responsible.
- Any forecast of orders or revenue; revenue per order was not compared.
- A gain for any group inside the test, such as mobile visitors; no breakdown was run.
- A precise size: the interval is wide compared with the gap.
- A count of people: results are per browser.

**Questions for you:**

1. Whether to switch everyone over is yours to decide; this check does not say. Is a gain that could be as small as 0.4 orders per 1,000 visitors enough for you, or do you want a longer run to narrow the range?
2. Can the testing tool count by person as well as by browser, so the double-counting flag can be cleared?

**Suggested wording for a report:** "In a 14-day test with visitors assigned at random, the new checkout page had a higher order rate than the old one: 13.49% against 11.99%, a gap of 1.50 points (95% interval 0.04 to 2.96). The gain could be very small; the test does not show why it happened or that it will hold in other periods."

Every figure was calculated from the data supplied, using Python's standard library. Nothing has been changed or sent, and whether to act is yours to decide.

## What was observed

- Every required part of the output format was produced and every heading was printed. Nothing in the inputs triggered a stop condition. The figures match the first acceptance test in the template (13.49%, 11.99%, 1.50, 0.04 to 2.96, p 0.044, narrow margin), which this run therefore also serves as.
- The decline of "Can we switch everyone over?" went in question 1, as the revised template now says. Possible overlap between groups was flagged under check 4, as the revised template now says. The unknown-k rule and the other new acceptance tests (10 and 11, and the unknown-k case) were not exercised, because the example supplies k; they have not been run.
- Compared with the published example's output, the figures, the support level, the five passes, the flag and the Cannot check are the same. Remaining small differences are wording only.
- Earlier points that were found in the first run and corrected in the published example rather than here: the suggested wording "a small to moderate gain" sat badly beside an effect size below the conventional small, and the example's "none missing" for a summary was not a supplied fact.

### Shortcomings

- The instruction block was amended after this run in small ways (the health, safety, legal and hiring decline, a rule for numeric outcomes given only as a summary, the support-level rule for a p-value not under 0.05 over k, and restating rules the block had omitted: effect-size labels, the per-1,000 figure, the 5% missing and 5-standard-deviation checks, and "significant" never without its number). None changes this example's inputs, output format or figures, so the run was not repeated and the output above is unchanged; the amended block itself has not been run.
- One run recorded, one model, one invented example, and not independent of the revisions. It says nothing about other data, other products or a client's setting.
- The edge rules added after the first run (unknown number of comparisons, known against possible overlap, numeric outcomes) have not been run.
