# Source guide for a data domain: tried twice on its own example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-12

This record covers two runs of the workflow template on its own invented example, both on 12 November 2026. The inputs are the invented ones in [example.md](example.md): the scope note, the table list, the interview notes and the counts, all invented. No client data was used.

## First run, and what it found

The first run was done by a model that did not write the template. It read the template and the example's four inputs first, followed the fenced instruction block and the output format, produced the full guide, and only then read the example's own output to compare. Its guide had 21 open questions and two joins fewer than the example's: it wrote two joins, listed three pairs under "possible joins by matching names only" and left refunds.order_id without a meaning. The example had 16 questions. Its guide is not reproduced here, because the template and the example were changed in answer to it. What it observed is recorded below as it was written.

### Observations of the first run

- **Every required part was produced, and nothing told me to stop.** The inputs were complete and well formed, so none of the stop conditions applied. The login line at the end of the notes was left out and named under Scope, as the template says.

**Where the instructions left me to guess or choose**

1. **Join columns the analyst did not name.** The notes say "customer_id joins to customers" and "joining orders to order_lines", but do not name the column on the far side. I wrote customers.customer_id and order_lines.order_id because the table list has exactly one candidate. That is close to reading a meaning from a shared name, which the template forbids. It should say whether to write the far-side column, or ask.
2. **Refunds and orders.** The notes say a refund covers one line or a whole order, and one order can have several refunds, but no join is described. I kept refunds out of Joins, listed three name-only pairs, and raised one question. The template does not say whether such a question is required.
3. **Columns used only in a definition.** quantity and unit_price are in the line value formula but have no stated meaning. The template exempts only columns in a key or a join, so I listed them as having no meaning recorded. A reader might see that as too strict.
4. **Traps with "Instead: not stated".** The template does not say whether these need a question. I raised one each (Q18 to Q21) because the Purpose says every gap becomes a question. The question order rule (tables, joins, definitions) has no place for them, so they came last.
5. **Currency trap.** The analyst described a fact (three currencies, rates elsewhere) and not what goes wrong. I recorded it as a trap in the analyst's words and added no consequence.
6. **Shorthand table names.** The analyst said "orders", "customers" and so on. I took them to mean the sales.* tables. The template does not cover this.
7. **Format of the proposed checks.** Step 11 says "the same CSV columns" (four columns) but the output format shows `table,check`. I followed the output format.
8. **The test-customer rule.** It was said under customers but is about orders. I put it under both tables' "rows usually left out" and in definition 1.
9. **Date format.** The format is silent on how to write dates. I used the ISO form of the counts' `run_on` column, and the scope note's wording for "Prepared".
10. **Which date is "Today".** The scope note says 6 November 2026; I used that, not the date of this trial.

**Differences from the published example**

- The example writes two more joins, refunds.order_id to orders.order_id (many-to-one) and refunds order_id + line_no to order_lines (proportion not stated, with the condition "only when line_no is not blank"). The notes describe neither join. I listed those pairs as name-only possibilities.
- Because of that, the example's "possible joins by matching names only" reads "none", and mine lists three pairs.
- The example gives refunds.order_id a meaning ("the refunded order"), which the notes do not state. I put order_id among the columns with no meaning recorded.
- The example has a trap for is_test (test orders are marked on the customer, not the order), which I did not write as a trap; I put the rule under rows usually left out and in definition 1. The example has no trap for the 2-row refund key (it is a conflict only); I added it as trap 6 because the template says to add every trap a check revealed.
- The example has 16 questions and mine has 21. Its Q16 (can one line have more than one refund) and Q14 are different from mine; my extra questions are Q14 (email), Q17 and Q18 to Q21.
- The example asks one question about marketing operations for segment (Q14); I wrote the same question as Q15, after adding email.
- The example proposes a fifth check (refunds unmatched order_id in orders) that depends on its join 3; I proposed four.
- The example's check dates are written "5 November 2026"; mine "2026-11-05". Counts are written with thousands separators in the example and without in mine.
- Wording of individual fields differs in small ways; the content of the six fields for orders, order_lines and customers, the key checks, the conflict and the do-not-use table agree.

**Facts in either output that are not in the inputs**

- In the example's output: refunds.order_id "the refunded order"; joins 3 and 4, including the condition "only when line_no is not blank" (the template's own text gives that phrase as an example of a condition, not the analyst's statement); the question about several refunds per line; the proposed refunds unmatched check. Also the closing paragraph says it ran no query, which is true.
- In mine: customers.customer_id and order_lines.order_id as the far-side join columns (inferred from identical names, see point 1 above), and "order total in the order's currency" for order_total, which is in the list note.

**Against the reviewer checklist.** Items 1, 2, 3, 5, 6 and 7 hold for my output. Item 4 (no shared name written as a join) is only partly met, because of point 1 above. Item 8 (owners read their lines) cannot be checked from a single run.

**Shortcomings (first run).** This was one run by one model on one invented example. It shows the template can be followed to a complete guide; it does not show that every acceptance test passes, and the template is not tested in a client environment. The example and the first run disagreed on three points (the refund joins, the meaning of refunds.order_id and the extra questions), which means the template left room for different readings.

## Edits made after the first run

- **What counts as a join.** Step 7 and the instruction block now say a join is described when the analyst says in substance how rows of one table relate to rows of another; a column need not be named. The refund statement ("a refund covers one line or the whole order", "one order can have several refunds") is therefore a described join.
- **How an unnamed column is written.** The column the analyst named is used. Otherwise a column is written only when the other table has exactly one column of that name, taken from a key the analyst stated for one of the two tables (first wording; see the review edit below), and it is marked "(matched by name)". Where that cannot be done the join says "column not stated" and raises a question. The output format shows the mark.
- **Meaning from a join.** A column used in a join takes no meaning from it. The example no longer says refunds.order_id is "the refunded order". Because the join line shows how such a column is used, it is not listed as having no meaning.
- **Conditions.** A condition is given only in the analyst's words. Join 4 no longer says "only when line_no is not blank", which was the template's own illustration; it says none was stated and quotes what the analyst said about a blank line_no. Q16 now also asks how refunds with a blank line_no are joined. The template's illustration was changed to a generic one.
- **Checks to confirm** are written as rows of the two-column CSV `table,check`, as the format shows.
- **Questions.** The claim that every gap becomes a question was narrowed in the template, the profile and the facts: unanswered fields, doubts, conflicts and unstated join proportions get questions; a trap whose remedy was not stated says "Instead: not stated" and needs none. Checklist item 5 says so.
- **Traps from checks.** A key that fails its check is a conflict only. An unmatched count above 0 that conflicts with no statement is a trap. Step 6, step 9 and the instruction block now agree.
- **Shorthand table names** ("orders", "customers") are matched when exactly one listed table has that name after its schema prefix; otherwise a question comes first in the numbering.
- **Dates and numbers** are written as in the scope note and with thousands separators.
- Two acceptance tests were added: relationship without column names (now test 13) and shorthand table name (now test 15; test 14 was added later, in review).
- The profile and the FAQ now say the template was tried on its invented example, and the example says "not in the table list" for finance.fx_rates.

## Second run

The second run was done on the edited template by the assistant that made the edits, so it is not an independent run. It followed the edited instruction block and output format on the same four inputs. The guide it produced is the one now published in the example; I wrote the example's output from that run, so they agreed because they were the same text, not because a second reader confirmed them. Two later edits changed the example without a re-run; they are listed under the review edits below.

### What came out

```
SOURCE GUIDE: Orders data domain

For: Head of data. Draft for the Senior analyst to verify. Prepared 6 November 2026 from: table list (5 tables, 29 columns); interview with the Senior analyst on 4 November 2026; 7 checks supplied, run on 5 November 2026.
Purpose: A guide for the analysts who work with order data, starting with the two who join in January.
Marks: [list] from the table list · [said] stated by the Senior analyst · [said, not sure] stated with doubt · [checked date] shown by a count the analyst ran · Qn open question n.

Scope
In the guide: sales.orders, sales.order_lines, sales.refunds, sales.customers, sales.orders_2019
In the table list, not covered in the interview: none
Named in the interview, not in the table list: finance.fx_rates (currency rates)
Do not use, as stated: sales.orders_2019
Checks supplied and not used: sales.orders median basket: not one of the three check forms
Left out of the guide: a warehouse login (a user name and where its password is kept), at the end of the interview notes; the Head of data should remove it from the notes

Tables

sales.orders: in use
One row is: one order [said]
Key: order_id [said] [checked 5 November 2026: 48,210 rows, 48,210 distinct]
Dates: placed_at: when the order was placed, stored in UTC; finance reports by Pacific time [said]. updated_at: the time of the last change to the row [said], time zone not stated. Q1
Changes after loading: rows are updated in place when the status changes; no history is kept [said]
Rows usually left out: cancelled orders, for any sales figure; orders of test customers (sales.customers.is_test = true) [said]
Owner: shop platform team [said]
Other columns with a recorded meaning: customer_id: the order's one customer [said]; status: pending, paid, shipped or cancelled [said]; channel: web, app or marketplace [said]; order_total: Order total in the order's currency [list], including shipping and excluding sales tax [said]; currency: the three-letter code of the order's currency [said]
Columns with no meaning recorded: none
Personal data: none marked

sales.order_lines: in use
One row is: one line of an order [said]
Key: order_id + line_no [said] [checked 5 November 2026: 131,877 rows, 131,877 distinct]
Dates: no date column in the table list
Changes after loading: not stated. Q2
Rows usually left out: not stated. Q3
Owner: shop platform team [said]
Other columns with a recorded meaning: sku: Product code [list]; discount: an amount for the whole line, in the order's currency, not per unit [said, not sure] Q5
Columns with no meaning recorded: quantity, unit_price. Q4
Personal data: none marked

sales.refunds: in use
One row is: one refund [said]
Key: refund_id [said]. The check does not hold; see conflict 1.
Dates: refunded_at: meaning not stated, time zone not stated. Q7
Changes after loading: not stated. Q8
Rows usually left out: not stated. Q9
Owner: shop platform team [said]
Other columns with a recorded meaning: line_no: the line the refund covers, blank when the refund covers the whole order [said]
Columns with no meaning recorded: amount, reason_code. Q10
Personal data: none marked

sales.customers: in use
One row is: one customer [said]
Key: not stated. Q11
Dates: first_order_at: meaning not stated, time zone not stated. Q12
Changes after loading: not stated. Q13
Rows usually left out: test customers (is_test = true); their orders are always left out [said]
Owner: CRM team [said]
Other columns with a recorded meaning: email: Customer email address [list]; is_test: true for test customers [said]; segment: set by marketing, by rules marketing operations owns [said] Q14
Columns with no meaning recorded: none
Personal data: email

sales.orders_2019: Do not use, as stated. Old system, before 2020; figures before 2020 come from finance's archive [said]. Q15

Joins
1. sales.orders.customer_id to sales.customers.customer_id (matched by name): many-to-one. Condition: none stated. [said]
2. sales.orders.order_id to sales.order_lines.order_id (matched by name): one-to-many. Condition: none stated. [said]
3. sales.refunds.order_id (matched by name) to sales.orders.order_id: many-to-one. Condition: none stated. [said]
4. sales.refunds.order_id (matched by name) + sales.refunds.line_no to sales.order_lines.order_id + sales.order_lines.line_no: proportion not stated. Q16. Condition: none stated; the analyst said line_no is blank when a refund covers the whole order. [said]
Possible joins by matching names only: none

Definitions
1. Line value: quantity x unit_price - discount, from sales.order_lines. [said] Q5
2. Orders counted in a sales figure: rows of sales.orders whose status is not cancelled and whose customer in sales.customers is not marked is_test = true. [said]

Known traps
1. sales.orders.order_total: joining sales.orders to sales.order_lines repeats order_total on every line, so a sum of order_total after the join counts each order once per line. Instead: never sum order_total after that join; use line value (definition 1). [said]
2. sales.orders.placed_at: stored in UTC while finance reports by Pacific time, so grouping by the UTC date gives different month totals from finance. Instead: not stated. [said]
3. sales.orders.status: rows are updated in place and no history is kept, so the status on a past date cannot be rebuilt. Instead: not stated. [said]
4. sales.orders.channel: marketplace orders load once a day at 06:00 UTC, so yesterday is incomplete until then. Instead: not stated. [said]
5. sales.orders.order_total: in the order's own currency, and the business sells in three; the rates are in finance.fx_rates, which is not in the table list. Instead: not stated. [said]
6. sales.customers.is_test: the orders of test customers must always be left out. Instead: join sales.orders to sales.customers and filter on is_test. [said]

Conflicts
1. "refund_id is the key" [said] against 2,390 rows and 2,388 distinct refund_id [checked 5 November 2026]: 2 more rows than distinct values. Q6

Open questions: 16
Q1. For the Senior analyst: In which time zone is sales.orders.updated_at stored?
Q2. For the Senior analyst: Are rows in sales.order_lines changed, deleted or replaced after they first appear?
Q3. For the Senior analyst: Which rows of sales.order_lines should normally be left out of a figure?
Q4. For the Senior analyst: What do sales.order_lines.quantity and sales.order_lines.unit_price hold?
Q5. For the shop platform team: Is sales.order_lines.discount an amount for the whole line, in the order's currency, as the Senior analyst believes?
Q6. For the Senior analyst and the shop platform team: On 5 November 2026 sales.refunds had 2,390 rows and 2,388 distinct refund_id values. Is refund_id the key, and what do the repeated rows stand for?
Q7. For the Senior analyst: What does sales.refunds.refunded_at record, and in which time zone?
Q8. For the Senior analyst: Are rows in sales.refunds changed, deleted or replaced after they first appear?
Q9. For the Senior analyst: Which rows of sales.refunds should normally be left out of a figure?
Q10. For the Senior analyst: What do sales.refunds.amount and sales.refunds.reason_code hold?
Q11. For the Senior analyst: Which columns make a row of sales.customers unique?
Q12. For the Senior analyst: What does sales.customers.first_order_at record, and in which time zone?
Q13. For the Senior analyst: Are rows in sales.customers changed, deleted or replaced after they first appear?
Q14. For marketing operations: What rules set sales.customers.segment?
Q15. For the Head of data: Does anyone still read sales.orders_2019?
Q16. For the Senior analyst: Can one line in sales.order_lines have more than one refund in sales.refunds, and how are refunds with a blank line_no joined to lines, if at all?

Checks to confirm (for an analyst to run; none has been run)
table,check
sales.customers,rows
sales.customers,distinct customer_id
sales.orders,unmatched customer_id in sales.customers.customer_id
sales.order_lines,unmatched order_id in sales.orders.order_id
sales.refunds,unmatched order_id in sales.orders.order_id

Draft for the Senior analyst to verify and the Head of data to approve. Built only from the table list, the interview notes and the counts supplied; nothing was connected to, queried, filed or published.
```

### What was observed

- Every required part was produced. The login line was left out and named under Scope. The 16 questions come in the order the template gives, with no question for the shorthand names, because each shorthand name matched exactly one listed table.
- All four joins the analyst described in substance are written. Joins 1 and 2 and the far side of 3 and 4 use the "(matched by name)" rule (join 1 by the name of the column the analyst named, the others from a stated key), and in each case the table list has exactly one column of that name. refunds.order_id appears in joins 3 and 4 and has no meaning recorded; nothing was invented for it.
- The facts in the guide that are not stated outright in the notes are now only these: the columns marked "(matched by name)"; the proportion "many-to-one" for joins 1 and 3, which follows from "each order has one customer" with one row per customer, and from "one order can have several refunds"; and the proposed checks. The first two are judgements that the domain analyst should confirm, and the guide shows them by their marks.
- The guide has no trap for the 2-row difference on refunds, because the template now sends that to Conflicts only.

### Where the instructions still need a judgement

- Whether "each order has one customer" with "one row per customer" fixes many-to-one, or leaves one-to-one possible. I took it as many-to-one, as the example does.
- Whether quantity and unit_price, used in a stated formula but never described, are "no meaning recorded". I listed them so.
- Whether the is_test statement is a trap. I recorded it as one, in the analyst's words, and also under rows usually left out.
- The matching rule for a column the analyst did not name has been tried on one example, where each of its four uses was unambiguous. Acceptance tests 13 to 15 have not been run.

### Shortcomings

Two runs of one template on one invented example, the second by the assistant that made the changes. It shows the template can be followed to a complete guide and that the two defects of the first run are closed on this example; it does not show that every acceptance test passes, and the template is not tested in a client environment.

## Edits after independent review (12 November 2026)

- **Join columns.** A reviewer found that join 1 (analyst names only orders.customer_id; no key stated for customers) did not follow the rule as written. Step 7 and the instruction block now give two cases: (a) a column named on one side only, where the other column is written only if exactly one column in that table has the same name as the named column; (b) no column named, where the columns come from a stated key as before. Both are marked "(matched by name)". This edit left the example output and the run above unchanged, because join 1 is case (a) and joins 2 to 4 are case (b) (for join 4, the analyst named refunds.line_no). The template was not re-run after this edit; the recorded output above is the earlier run's, unaltered. A new acceptance test (14) covers case (a); tests 13 to 15 have not been run.
- **Smaller changes.** The instruction block now also says what a date column is, that a check naming an unlisted table or column is not used, that a table not to be used is left out of possible joins and proposed checks, and writes the date form as "such as 5 November 2026". Step 7 says which grains fix a proportion. The example's customers line now says orders of test customers are left out, as the analyst said, and its closing paragraph says definition 2 is assembled from two statements. The profile and facts say the template guesses "no meaning" from a column name.
- **Second-round review edits (12 November 2026).** Step 7 now says which table's stated key to take when both have one (the key all of whose columns have exactly one same-named column in the other table), and that only the matched column is marked; step 8 and the instruction block now allow a definition put together from separate statements of the analyst. In the example, orders.customer_id no longer has a meaning line (it appears in join 1 and a join column takes none), trap 1 no longer adds the consequence "so a sum of order_total after the join counts each order once per line", and the closing paragraph explains join 4's marks and says the test-customer rule under customers is a judgement. The recorded output in the second run above still shows the earlier text on these points, unaltered; the template was not re-run after these edits, so the example now differs from that record on the customer_id line, trap 1 and the customers' rows-left-out line.
