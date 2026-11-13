# Source guide for a data domain: an invented example

*Illustrative example with invented data.* The business, the people, the tables, the counts and the notes below are all invented. The business is an invented online retailer of outdoor gear with a small data team: a head of data and three analysts. One of them, the senior analyst, is the person everyone asks about the order tables. Two new analysts join in January, so the head of data interviews the senior analyst and runs the workflow template. First come the inputs, in full, then the guide it returned.

## The inputs

### 1. Scope note (typed by the head of data)

```
Domain: Orders
Purpose: A guide for the analysts who work with order data, starting with the two who join in January
Domain analyst: Senior analyst
Data lead: Head of data
Today: 6 November 2026
```

### 2. Table list (copied by the senior analyst from the warehouse's column listing)

```
table,column,type,note
sales.orders,order_id,bigint,
sales.orders,customer_id,bigint,
sales.orders,placed_at,timestamp,
sales.orders,status,text,
sales.orders,channel,text,
sales.orders,order_total,decimal,Order total in the order's currency
sales.orders,currency,char(3),
sales.orders,updated_at,timestamp,
sales.order_lines,order_id,bigint,
sales.order_lines,line_no,integer,
sales.order_lines,sku,text,Product code
sales.order_lines,quantity,integer,
sales.order_lines,unit_price,decimal,
sales.order_lines,discount,decimal,
sales.refunds,refund_id,bigint,
sales.refunds,order_id,bigint,
sales.refunds,line_no,integer,
sales.refunds,refunded_at,timestamp,
sales.refunds,amount,decimal,
sales.refunds,reason_code,text,
sales.customers,customer_id,bigint,
sales.customers,email,text,Customer email address. Personal data
sales.customers,first_order_at,timestamp,
sales.customers,segment,text,
sales.customers,is_test,boolean,
sales.orders_2019,order_id,bigint,
sales.orders_2019,customer_id,bigint,
sales.orders_2019,placed_at,timestamp,
sales.orders_2019,total,decimal,
```

### 3. Interview notes (typed by the head of data during the conversation)

```
Interview with the senior analyst, 4 November 2026.

orders
- One row per order. order_id is unique.
- Each order has one customer: customer_id joins to customers.
- placed_at is when the order was placed, stored in UTC. Finance reports by
  Pacific time, so grouping by the UTC date gives different month totals
  from finance.
- status is one of pending, paid, shipped, cancelled. Leave out cancelled
  orders for any sales figure.
- order_total includes shipping and excludes sales tax. currency is the
  three-letter code of the order's currency.
- Rows are updated in place when the status changes; updated_at is the time
  of the last change. No history is kept, so you cannot rebuild what the
  status was on a past date.
- channel is web, app or marketplace. Marketplace orders load once a day at
  06:00 UTC, so yesterday is incomplete until then.
- order_total is in the order's own currency and we sell in three. Rates are
  in finance.fx_rates, which is not in this list.
- Owner: shop platform team.

order_lines
- One row per line of an order; order_id and line_no together are unique.
- Joining orders to order_lines repeats order_total on every line. Never sum
  order_total after that join. For line value use
  quantity x unit_price - discount.
- discount is for the whole line, in the order's currency, not per unit.
  I think. Check with the shop platform team.
- Owner: shop platform team.

refunds
- One row per refund. refund_id is the key.
- A refund covers one line or the whole order; line_no is blank when it
  covers the whole order. One order can have several refunds.
- Owner: shop platform team.

customers
- One row per customer.
- Test customers have is_test = true. Their orders must always be left out:
  join orders to customers and filter on is_test.
- segment is set by marketing. I don't know the rules; marketing operations
  owns them.
- Owner: CRM team.

orders_2019
- Old system, before 2020. Do not use: figures before 2020 come from
  finance's archive. Not sure whether anyone still reads it.

(Warehouse login for the team: user analytics_ro, password on the team sheet.)
```

### 4. Counts the senior analyst ran and pasted in

```
table,check,result,run_on
sales.orders,rows,48210,2026-11-05
sales.orders,distinct order_id,48210,2026-11-05
sales.order_lines,rows,131877,2026-11-05
sales.order_lines,distinct order_id + line_no,131877,2026-11-05
sales.refunds,rows,2390,2026-11-05
sales.refunds,distinct refund_id,2388,2026-11-05
sales.orders,median basket,61.40,2026-11-05
```

## The output

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
Other columns with a recorded meaning: status: pending, paid, shipped or cancelled [said]; channel: web, app or marketplace [said]; order_total: Order total in the order's currency [list], including shipping and excluding sales tax [said]; currency: the three-letter code of the order's currency [said]
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
Rows usually left out: orders of test customers (is_test = true) are always left out [said]
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
1. sales.orders.order_total: joining sales.orders to sales.order_lines repeats order_total on every line. Instead: never sum order_total after that join; use line value (definition 1). [said]
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

Every line of the guide traces to the scope note, the table list, the interview notes or the counts above. Where the analyst described a relationship without naming a column ("customer_id joins to customers", "a refund covers one line or the whole order"), the join is written because the relationship was described; the column the analyst did not name is written only when its table has exactly one column of that name, and is marked "(matched by name)". In join 1 the analyst named orders.customer_id, and the far column is the one customers column of that name; in joins 2 and 3 no column was named, and the far column comes from the stated key of the other table (order_id of orders; order_lines has one order_id, refunds has one). In join 4 the analyst named refunds.line_no, so it carries no mark, and refunds.order_id came from the stated key of order_lines (order_id + line_no). Only the column that was matched is marked. Definition 2 is assembled from two separate statements (cancelled orders; test customers), both traced to the notes. The test-customer rule was said under customers but is about orders; it is recorded under rows usually left out for both tables, a judgement the analyst should confirm. The proportion of join 3 is stated ("one order can have several refunds"); that of join 4 is not. No column takes a meaning from a join. Of the seven counts, six were read: the two on sales.orders and the two on sales.order_lines agree, so those keys held on 5 November; the two on sales.refunds differ by 2,390 − 2,388 = 2, which is recorded as a conflict rather than settled. The workflow template ran no query and logged in to nothing.
