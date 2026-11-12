# Analysis plan: an invented example

*Illustrative example with invented data.* The business, the people, the files, the dates and the lists below are invented, and no real business is meant. The business is an invented 40-person online seller of garden furniture, with its own warehouse and a contract carrier. Its Owner has a question and a budget decision to make. People appear by role.

On Monday 9 November 2026 the Owner typed the request note and the three lists below, and asked for a plan. No data was opened or pasted: the lists describe the files. The inputs come first, in full, so the template can be run on them. The plan the workflow template returned follows.

## The inputs

### 1. Request note (typed by the Owner)

```
Question as asked: Repeat customers have dropped this autumn. Find out why.
Asked by: Owner
Decision this feeds: How to spend the $18,000 retention budget for the first quarter of 2027
Decision owner: Owner
Decision needed by: 2026-11-20
Options on the table: A. Pay for the faster carrier service. B. Fund an email series for new customers, sent in their first 90 days. C. Hold the money for now.
Criteria: A, if customers whose first order took 6 or more days to arrive reorder at under half the rate of customers whose first order took 3 days or less. B, if new customers who got at least one of our emails reorder at a rate 5 percentage points or more above new customers who got none. C, if neither.
Hunches: Operations manager: deliveries got slower after we changed carrier in June. Marketing manager: we send fewer emails to new customers than we used to.
```

### 2. Source list (typed by the Owner; headers and descriptions only)

```
source,owner,holds,one_row_per,columns,covers_from,covers_to,last_refreshed
orders_export.csv,Operations manager,Every order placed through the website,order,order_id; customer_id; order_date; order_value; delivery_days; is_first_order,2025-01-01,2026-10-31,2026-11-09
emails_export.csv,Marketing manager,Every campaign email sent to a customer,email sent,customer_id; send_date; campaign; opened,2025-03-01,2026-10-31,2026-11-09
support_tickets.csv,Customer service lead,Every support ticket opened,ticket,ticket_id; customer_id; opened_date; category,2026-04-01,2026-10-31,2026-11-09
```

### 3. Definitions (typed by the Owner)

```
term,definition,owner
repeat rate,Share of the customers whose first order fell in a month who place a second order within 90 days of the first,Owner
repeat share,Share of the customers who bought in a month who had bought before,Marketing manager
first-time customer,A customer on an order where is_first_order = Y,Operations manager
```

### 4. Known events (typed by the Owner)

```
date,event
2026-04-01,New helpdesk system started; earlier tickets were not carried over
2026-06-15,Changed delivery carrier
2026-08-03,Free shipping began on orders over $75
```

### 5. Settings (typed by the Owner)

```
Today: Monday 9 November 2026
Plan prepared for: Owner
Analytics lead: Operations manager
Smallest group worth reading: (left blank)
```

## The plan the workflow template returned

```
ANALYSIS PLAN: Why repeat customers fell this autumn

Prepared for: Owner. Decision owner: Owner. Date: Monday 9 November 2026. Status: Not ready: 2 blocking questions.

1. Question
As asked: "Repeat customers have dropped this autumn. Find out why."
Restated: What is behind the fall in repeat customers this autumn, so the Owner can decide how to spend the $18,000 retention budget for the first quarter of 2027? Measured: not stated (question 1). For: customers who ordered through the website (orders_export.csv). Period: this autumn, dates not stated (question 2). Compared with: not stated (question 2).

2. Decision
Decision: How to spend the $18,000 retention budget for the first quarter of 2027. Needed by: Friday 20 November 2026. Options: A. Pay for the faster carrier service. B. Fund an email series for new customers, sent in their first 90 days. C. Hold the money for now.

3. Hypotheses
H1 (Operations manager): Deliveries got slower after the carrier change in June. True if: customers whose first order took longer to arrive reorder less often than customers whose first order arrived faster, and delivery times are longer after 15 June 2026 than before. False if: reorder rates are similar across delivery times, or delivery times did not lengthen.
H2 (Marketing manager): Fewer emails go to new customers than before. True if: new customers received fewer emails in their first 90 days in recent months than in earlier ones. False if: email counts per new customer did not fall.
H3 (proposed by the assistant, owner to keep or strike; it follows from the free shipping that began on 3 August 2026): Free shipping brought in more first-time customers, so the share of buying customers who had bought before fell although no fewer people came back. True if: the number of repeat buyers per month did not fall while the number of first-time customers rose after 3 August 2026. False if: the number of repeat buyers fell as well.

4. Fields and periods
H1: orders_export.csv: customer_id; order_date; delivery_days; is_first_order. Availability: unclear (question 3). Periods: first orders by whole month, January 2025 to July 2026, measuring a second order within 90 days. The last complete month is July 2026: the file ends on 2026-10-31, so only first orders on or before 2026-08-02 have had 90 days, and August to October 2026 are dropped from this measure. Compare June and July 2026 with January to May 2026, and with June and July 2025. The carrier change on 2026-06-15 falls inside June; June is shown whole until question 4 is answered. First orders from this autumn cannot be read under this measure before the decision date: the latest first order with 90 days is 2026-08-02 (question 2).
H2: emails_export.csv: customer_id; send_date (and opened, if the answer to question 7 is "opened"). orders_export.csv: customer_id; order_date; is_first_order. Availability: available. Periods: the same first-order months, but emails_export.csv starts on 2025-03-01, so the first month that can be split into emailed and not emailed is March 2025. Emails are counted in the 90 days after each customer's first order.
H3: orders_export.csv: customer_id; order_date; is_first_order. Availability: available. Periods: whole months, January 2025 to October 2026. Compare August to October 2026 with May to July 2026, and with August to October 2025. The free shipping that began on 2026-08-03 falls inside August 2026 (question 5).
Joins: customer_id links emails_export.csv to orders_export.csv. One row is one email sent in emails_export.csv and one order in orders_export.csv, so emails are counted per customer before joining.
Sources not used: support_tickets.csv: no hypothesis uses it, and it starts on 2026-04-01 after the helpdesk change.

5. Definitions
repeat customers: no definition supplied under that name; the list holds two nearby terms (question 1), shown next.
repeat rate: share of the customers whose first order fell in a month who place a second order within 90 days of the first (Owner).
repeat share: share of the customers who bought in a month who had bought before (Marketing manager).
first-time customer: a customer on an order where is_first_order = Y (Operations manager).
new customers (H2, option B): no definition supplied (question 6).
delivery_days: no definition supplied (question 3).

6. Decision criteria
A: if customers whose first order took 6 or more days to arrive reorder at under half the rate of customers whose first order took 3 days or less (Owner). The measure of "reorder rate" is not stated (question 1).
B: if new customers who got at least one of our emails reorder at a rate 5 percentage points or more above new customers who got none (Owner). The measure of "reorder rate" is not stated (question 1). Whether "got" means sent or opened is not stated (question 7).
C: hold the money for now, if neither A nor B applies (Owner).
Unchanged if: neither A nor B applies (option C).
Both A and B could be met, and no rule says which wins (question 8).
Smallest group worth reading: not supplied (question 9).

7. Checks before reading results
1. The first step of the analysis is to reproduce the fall under the measure chosen at question 1, because the request note reports it and no figure was supplied.
2. Drop first orders after 2026-08-02 from the repeat rate, because orders_export.csv ends on 2026-10-31 and the rate needs 90 days.
3. Do not split January and February 2025 into emailed and not emailed, because emails_export.csv starts on 2025-03-01.
4. Count emails per customer before joining to orders, because emails_export.csv has one row per email sent.
5. Confirm what delivery_days counts before using the 3 and 6 day cut-offs in option A, because no definition of delivery_days is supplied.
6. Read the carrier change on first orders in whole months, June and July 2026, because the carrier changed on 2026-06-15 and the cut-off is 2026-08-02. First orders on 1 and 2 August 2026 also have 90 days but fall outside whole months, and first orders in June before 2026-06-15 precede the change, so June is shown whole until question 4 is answered.

8. Open questions
1. BLOCKING Which measure does "repeat customers" mean: the repeat rate (Owner) or the repeat share (Marketing manager)? And does "reorder rate" in options A and B mean the repeat rate? Answered by: Owner.
2. not blocking Which months does "this autumn" cover, and what was it compared with when the fall was seen? Under the repeat rate, first orders from this autumn cannot be read before the decision date of 2026-11-20, because the latest first order with 90 days is 2026-08-02; is a different period acceptable? Answered by: Owner.
3. not blocking What does delivery_days count, and from which date to which? Answered by: Operations manager.
4. not blocking Is June 2026 split on 2026-06-15 by order date, or left whole? Answered by: Owner.
5. not blocking Is August 2026 split on 2026-08-03 by order date, or left whole? Answered by: Owner.
6. not blocking Are "new customers" the same as first-time customers? Answered by: Owner.
7. not blocking In option B, does "got at least one of our emails" mean sent or opened? Answered by: Marketing manager.
8. BLOCKING If both the condition for A and the condition for B are met, which option is chosen? Answered by: Owner.
9. not blocking What is the smallest group of customers worth reading a rate from? Answered by: Owner.

This plan runs no analysis and states no finding. The question and the decision criteria belong to the Owner. Agreed by the decision owner and the Operations manager: ________ Date: ________
```
