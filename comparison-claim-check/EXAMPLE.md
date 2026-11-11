# Comparison claim check: an invented example

*Illustrative example with invented data.* An invented online shop, "Shop X", has tried a new checkout page. Everything below, including the company, the message and the numbers, is made up to show the shape of the work.

## What the person supplies

**The claim, from a message to the owner:** "The new checkout page (version B) converts better than the old one (version A). Can we switch everyone over?"

**The data, a summary with the default headers `group`, `n`, `successes`:**

- A, 4020, 482
- B, 3980, 537

`n` is visitors who reached the checkout. `successes` is visitors who completed an order.

**Notes from the person:**

- Outcome: a visitor who reached the checkout placed an order in the same visit. Counted per browser, so one person on two devices can count twice.
- Groups were formed by the shop's testing tool, which assigned each new visitor to A or B at random on the first visit. The planned split was half and half.
- The test ran for the same 14 days for both versions, which had been set in advance. Nobody looked at results before the end.
- One comparison was planned: conversion, B against A.
- A sale ran in the second week for everyone.
- Smallest difference that would matter: not supplied.

## What comes out

**COMPARISON CLAIM CHECK: new checkout page (B) converts better than the old (A)**

**Support level:** Supports the claim, within the limits below.

**The claim:** Version B has a higher share of checkout visitors who place an order than version A.

**What was compared:** Group A: 4,020 visitors, 482 orders. Group B: 3,980 visitors, 537 orders. Outcome: an order in the same visit, counted per browser. Period: the same 14 days for both (dates not supplied). Groups formed by: random assignment on first visit by the testing tool.

**Method used:** Difference between two rates, with a 95% interval and a z-test using the pooled rate. It fits because the outcome is yes or no and each group has at least 10 orders and 10 non-orders.

**Result:** Version A 11.99% against version B 13.49%. Difference (B minus A): 1.50 percentage points, a relative difference of 12.5%. 95% interval: 0.04 to 2.96 points. p-value 0.044, compared with 0.05 for one comparison. Effect size: Cohen's h 0.045, below the conventional "small" of 0.2. In business terms: about 15 more orders per 1,000 visitors (interval 0.4 to 29.6). Smallest meaningful difference: not supplied.

**Assumption checks:**

- Groups formed: Pass. Random assignment, so a gap can be read as an effect of the version.
- Split against plan: Pass. 4,020 and 3,980 against a planned half and half; chi-square 0.20, p 0.655.
- Size and shape: Pass. Orders 482 and 537, non-orders 3,538 and 3,443, all at least 10.
- Each unit counted once: Flag. Counting is per browser, so some people may be counted twice, and a person on two devices could be in both groups; how many is not known.
- Early looking and repeated comparisons: Pass. Fixed 14 days, nobody looked before the end, and one comparison was made.
- Same conditions: Pass. Both versions ran over the same days, including the week-two sale.
- Missing or extreme values: Cannot check. A summary cannot show missing outcomes and none were mentioned; there are no numeric values to check. This does not lower the support level.

**What the data supports:** In these 14 days, 13.49% of visitors on version B placed an order against 11.99% on version A, a gap of 1.50 points. Visitors were assigned at random, so the gap can be read as an effect of the page and not of who saw it. The margin is narrow: the lower end of the interval, 0.04 points, is under a tenth of the observed gap, so the true gain could be close to nothing or about 3 points.

**What it does not support:**

- That B will do as well in other weeks, on other traffic or without a sale running.
- Why B does better, or which change on the page is responsible.
- Any forecast of yearly orders or revenue; revenue per order was not compared.
- A gain for any group inside the test, such as mobile visitors; no breakdown was run.
- A precise size: the interval is wide compared with the gap.

**Questions for you:**

1. Whether to switch everyone over is yours to decide; this check does not say. Is a gain that could be as small as 0.4 orders per 1,000 visitors enough to justify the switch, or do you want to run longer to narrow the range?
2. Can the testing tool count by person as well as by browser, so the double-counting flag can be cleared?

**Suggested wording for a report:** "In a 14-day test with visitors assigned at random, the new checkout page had a higher order rate than the old one: 13.49% against 11.99%, a gap of 1.50 points (95% interval 0.04 to 2.96). The gain could be very small; the test does not show why it happened or that it will hold in other periods."

Every figure was calculated from the two rows supplied, using Python's standard library. Nothing has been changed or sent, and whether to act is yours to decide.
