# Analysis plan: a trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs for this trial are the invented example in [example.md](example.md): five short lists about an invented 40-person online seller of garden furniture. No client data was used. Nothing real was pasted, and the example holds only file descriptions, no rows of data.

I (the model) did not write this capability template. I followed its instructions block and output format on the five inputs from the example (the request note, source list, definitions, known events and settings), and then compared the result with the example's published plan and the template's reviewer checklist.

This is the second run. The first run, the same day, used an earlier wording of the block and raised the points that led to the edits below; this record replaces it. Since the first run the block has gained a rule for a period that falls wholly after a maturing cut-off, and says "one page where possible" in place of "one page". The example's inputs did not change.

One honest caveat on the method: I had read the first run's record and the example's published plan before writing this plan, so the trial is not blind. I wrote the plan from the template's rules.

## What came out

```
ANALYSIS PLAN: Why repeat customers dropped this autumn

Prepared for: Owner. Decision owner: Owner. Date: Monday 9 November 2026. Status: Not ready: 2 blocking questions.

1. Question
As asked: "Repeat customers have dropped this autumn. Find out why."
Restated: What explains the drop in repeat customers this autumn, so that the Owner can decide how to spend the $18,000 retention budget for the first quarter of 2027? Measured: not stated (question 1). For: customers who ordered through the website (orders_export.csv); no narrower group stated. Period: "this autumn", dates not stated (question 2). Compared with: not stated (question 2).

2. Decision
Decision: How to spend the $18,000 retention budget for the first quarter of 2027. Needed by: Friday 20 November 2026. Options: A. Pay for the faster carrier service. B. Fund an email series for new customers, sent in their first 90 days. C. Hold the money for now.

3. Hypotheses
H1 (Operations manager): Deliveries got slower after we changed carrier in June. True if: delivery_days is higher for orders placed after 2026-06-15 than before, and customers whose first order took longer to arrive placed a second order less often. False if: delivery_days did not rise, or second-order rates are similar whatever the delivery time.
H2 (Marketing manager): We send fewer emails to new customers than we used to. True if: the number of emails per first-order customer in the 90 days after that order is lower in recent months than in earlier months. False if: that number is flat or higher.
H3 (proposed by the assistant, owner to keep or strike; it follows from the known event of 2026-08-03, free shipping on orders over $75): Free shipping added first-time customers, so the share of buyers who had bought before fell without fewer people coming back. True if: the monthly count of customers on orders where is_first_order is not Y did not fall after 2026-08-03 while the count on orders where is_first_order = Y rose. False if: the count of returning customers fell too.

4. Fields and periods
H1: orders_export.csv: customer_id; order_date; delivery_days; is_first_order. Availability: unclear (question 3). Periods: whole months. The measure needs 90 days to mature if "second order" is read as in the repeat rate definition; the source ends 2026-10-31, so the cut-off is 2026-08-02 (90 days before), and first orders from August 2026 on are dropped from this measure. Last complete month: July 2026. Compare June and July 2026 with the months just before (January to May 2026) and with June and July 2025 (the source starts 2025-01-01). The carrier change of 2026-06-15 falls inside June (question 4). The period asked about, "this autumn" (question 2), has no dates; if it means August to October 2026 it falls wholly after the cut-off, so the repeat rate cannot be read for it before the decision date of 2026-11-20, and the months above are a substitute named as such. Rule applied: maturing measure, cut-off, prior months, same months a year earlier.
H2: emails_export.csv: customer_id; send_date; orders_export.csv: customer_id; order_date; is_first_order. Availability: available. Periods: whole months of first orders, March 2025 to July 2026. emails_export.csv starts 2025-03-01, so earlier first orders cannot be served; the first period is March 2025. The 90-day email window needs the same cut-off, 2026-08-02. Rule applied: late source, cut-off.
H3: orders_export.csv: customer_id; order_date; is_first_order. Availability: available. Periods: whole months, no maturing needed, January 2025 to October 2026 (the source covers October fully). Compare August to October 2026 with May to July 2026 and with August to October 2025. The free shipping start of 2026-08-03 falls inside August (question 5).
Joins: H2 joins orders_export.csv to emails_export.csv on customer_id. One row in orders_export.csv is one order; one row in emails_export.csv is one email sent. Emails are counted by customer_id before the join; orders are reduced to each customer's first order.
Sources not used: support_tickets.csv: no hypothesis needs it, and it starts 2026-04-01 after a helpdesk change, so earlier tickets are missing.

5. Definitions
repeat customers: no definition supplied under that name; the list holds two nearby terms (question 1). repeat rate: share of the customers whose first order fell in a month who place a second order within 90 days of the first (Owner). repeat share: share of the customers who bought in a month who had bought before (Marketing manager).
first-time customer: a customer on an order where is_first_order = Y (Operations manager).
new customers (option B and H2): no definition supplied (question 6).
delivery_days (H1, option A): no definition supplied (question 3).
this autumn: no definition supplied (question 2).

6. Decision criteria
A: reorder rate of customers whose first order took 6 or more days to arrive, compared with those whose first order took 3 days or less; the number is "under half the rate"; leads to A. The meaning of "reorder rate" is not stated (question 1).
B: reorder rate of new customers who got at least one of our emails, compared with new customers who got none; the number is 5 percentage points or more above; leads to B. What "got" means is not stated (question 7).
C: if neither A nor B is met.
Unchanged if: the Owner's words give C if neither criterion is met; nothing else stated.
Both A and B could be met, and no rule says which wins (question 8).
Smallest group worth reading: not supplied.

7. Checks before reading results
1. Reproduce the drop first under the measure the Owner chooses, because the change reported has not been seen.
2. Drop first orders after 2026-08-02 from the repeat rate and the email window, because the source ends 2026-10-31 and the measure needs 90 days.
3. Show June 2026 whole and note the carrier change of 2026-06-15 in it, because the change falls inside the month.
4. Show August 2026 whole and note the start of free shipping on 2026-08-03, because it falls inside the month.
5. Count emails per customer_id before joining, because emails_export.csv has many rows per customer.
6. Confirm what delivery_days counts with the Operations manager, because the name does not say.
7. Do not compare emailed with not-emailed customers before March 2025, because emails_export.csv starts on 2025-03-01.

8. Open questions
1. BLOCKING Which measure is "repeat customers": repeat rate (Owner) or repeat share (Marketing manager), and does "reorder rate" in options A and B mean the repeat rate? Answered by: Decision owner.
2. not blocking What dates are "this autumn", and what is it compared with? Under the repeat rate, first orders from this autumn cannot be read before 2026-11-20; is a different period acceptable? Answered by: Decision owner.
3. not blocking What does delivery_days count from and to? Answered by: Operations manager (source owner).
4. not blocking How should June 2026 be treated, given the carrier change of 2026-06-15? Answered by: Decision owner with the analytics lead.
5. not blocking How should August 2026 be treated, given free shipping from 2026-08-03? Answered by: Decision owner with the analytics lead.
6. not blocking Are "new customers" the same as "first-time customers"? Answered by: Decision owner.
7. not blocking In option B, does "got at least one of our emails" mean sent or opened, and which campaigns count? Answered by: Marketing manager.
8. BLOCKING If both A's and B's criteria are met, which option wins? Answered by: Decision owner.
9. not blocking Is there a smallest group worth reading for the rate comparisons? Answered by: Decision owner.

This plan runs no analysis and states no finding. The question and the decision criteria belong to the Owner. Agreed by the decision owner and the Operations manager: ________ Date: ________
```

## What was observed

**Every part was produced.** All eight sections came out in the fixed order, with the status line, the closing line and the signature line. The status was "Not ready: 2 blocking questions". Nothing in the inputs triggered a stop condition: the question, decision, owner, options, source list and today's date were present and every header matched.

**No finding was stated.** I wrote no figure and no claim about what the data shows. The true-if and false-if lines name only columns on the source list.

**The new rule worked as written.** The period asked about, "this autumn", has no dates. Reading it as August to October 2026, it falls after the cut-off of 2026-08-02, counted as 90 days before 2026-10-31. The rule had me say so in plain words on the H1 period line and raise it as question 2, and name the months used instead as a substitute.

**Where the plan matches the published example.**
- The same status and the same two blocking questions: which measure "repeat customers" means, and which option wins if both A's and B's criteria are met.
- The same cut-off date, with August to October 2026 dropped from the repeat rate.
- The same three hypotheses, with the free-shipping one marked as proposed by the assistant.
- The same joins rule, the same unused support-ticket source and the same "not stated" for the smallest group worth reading.

**Where the plan differs from the published example.**
- The numbering of the open questions differs, and the example's checks list is shorter. My checks name the June and August events as separate lines; the example folds the carrier change into one check about whole months.
- The example's H2 true-if line also asks whether emailed customers reordered more; mine keeps H2 to the number of emails per new customer.
- I raised the same nine open questions in a different order.

**Facts not in the inputs.** I found none in my plan.

**Where the instructions were still ambiguous, so I had to make a choice.**
1. "Repeat customers" is not on the definitions list, but two nearby terms are. The template does not say how to treat a term that is only close to a listed one. I showed both and asked.
2. The blocking list does not cover a missing period or comparison, or an undefined term inside a criterion such as "new customers" or "reorder rate". I marked these not blocking and was not sure that is what the authors meant. The template lists this as something to customize.
3. "Unchanged if" is hard to fill when a catch-all option already says what happens if the other criteria are not met.
4. "Number the questions in the order the sections raised them" conflicts slightly with step 2, which needs question numbers before the questions are all known. I numbered after drafting the sections and then went back to fill the references in section 1.
5. The template does not say whether a plan with an "unclear" availability can still be tested.
6. The cut-off is N days before covers_to. I took an order on 2026-08-02 as just matured; the template does not say whether the boundary day is in or out.
7. The plan here is longer than one page of ordinary text. With "one page where possible" I kept it as short as the fixed format allowed, and it still runs over; the wording now allows that.

**Shortcomings of the template as observed.** The instructions block is long and I had to hold the full section 4 rules in mind while writing. The template leaves it to the assistant to decide how many separate questions to raise, so two runs will not give the same list. Reviewer checklist item 5 (source owners confirm the columns) cannot be judged from the output alone.

**What this trial does not show.** It is one run, by one model, on an invented example. It says nothing about how the template works with real data, in other AI products or for a real client.
