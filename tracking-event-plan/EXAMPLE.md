# Tracking event plan: an invented example

*Illustrative example with invented data.* The company, the tools and the people below are all invented. Studio L is an invented 12-person workshop that makes furniture to order and takes quote requests through its website. Its two tools are called Tool A (analytics) and Tool B (email service). The founder is about to have a contractor add tracking to the site. First come the inputs the founder supplied, in full, then the plan the workflow template returned.

## The inputs

### 1. Settings (typed by the founder)

```
Business: Studio L
Today: Tuesday 10 November 2026
Workflow: the Studio L website
Runner: Founder
Approver: Founder
Event owner (who says what an event means): Founder
Builder: Web developer (contractor)
Naming rule: default
Never collect: names, email addresses, phone numbers, anything typed into the message box
```

### 2. Questions (typed by the founder)

```
id,question,decision it informs,asked by
Q1,"What share of people who look at a piece go on to ask for a quote?","Whether the autumn budget goes to the product pages or to advertising",Founder
Q2,"Which kinds of project do quote requests ask about?","Which three pieces to photograph for the spring catalogue",Founder
Q3,"Which quote requests become orders?","Whether to follow up every request within a day",Founder
Q4,"How many people join the newsletter, and from which kind of page?","Whether to keep the sign-up box in the footer",Founder
Q5,"Do people like the new homepage?",,Founder
Q6,"How many people ask for a quote more than once?","Whether to merge repeat requests in the office",Founder
```

### 3. The journey (typed by the founder)

```
step,where,what the visitor does,what the site does
1,"Home page and range pages","Arrives and browses the ranges","Shows the three ranges: dining tables, desks, shelving"
2,"Product page","Opens a piece","Shows photos, sizes and a from-price"
3,"Quote form page","Presses Ask for a quote, then fills in name, email, project type (dining table, desk, shelving or other), budget range and a message, and presses Send","Shows Thank you, we reply in two working days, and emails the form to the office"
4,"Footer of every page","Types an email address and presses Subscribe","Shows You are subscribed once Tool B has accepted the address"
```

### 4. Events already collected

```
event_name,description,destination
page_view,"Any page opens",Tool A
quote_submit,"Quote form sent",Tool A
signup,"A visitor joined something",Tool A
```

### 5. Destinations

```
destination,used for,owner
Tool A,"Counting visits and actions on the website",Founder
Tool B,"Sending the newsletter",Office manager
```

## The plan

**TRACKING EVENT PLAN: the Studio L website**

**For:** Founder. Prepared Tuesday 10 November 2026, from 6 questions, 4 journey steps, 3 existing events and 2 destinations. Naming rule: default (object, then action in the past tense, lowercase, words joined by underscores). Destinations: Tool A, Tool B.
**Counts:** Questions 6 (answered 3, not answerable 1, need rewording 1, held 1). Events 3 (1 new, 2 existing reused with a change, 0 existing reused unchanged). Properties 2, each counted once (page_type on 2 events, project_type on 1). Decisions 8.

**Questions**

- **Q1.** What share of people who look at a piece go on to ask for a quote? Decision it informs: whether the autumn budget goes to the product pages or to advertising. Measure: visitors, as Tool A counts them, who sent at least one quote request, out of visitors, as Tool A counts them, who opened at least one product page, in the same period. Answered by: page_view with page_type product; quote_submit. The plan adds no way to recognise a visitor and relies on Tool A's own count. See decision 7.
- **Q2.** Which kinds of project do quote requests ask about? Decision it informs: which three pieces to photograph for the spring catalogue. Measure: quote requests sent, counted by project type. Answered by: quote_submit with project_type.
- **Q3.** Which quote requests become orders? Decision it informs: whether to follow up every request within a day. Not answerable from this plan: the sale happens outside the website. The plan can count requests but cannot show which became orders; that needs a link between a request and the order book. See decision 5.
- **Q4.** How many people join the newsletter, and from which kind of page? Decision it informs: whether to keep the sign-up box in the footer. Measure: subscriptions completed, counted by the kind of page the visitor was on. Answered by: newsletter_subscribed with page_type.
- **Q5.** Do people like the new homepage? Decision it informs: no decision named. Needs rewording: "like" is not something a site can count, and no decision depends on the answer. No event is planned for it. See decision 6.
- **Q6.** How many people ask for a quote more than once? Decision it informs: whether to merge repeat requests in the office. Held: the decision is to merge repeat requests in the office, which needs individual requests tied to one person, not a count of visitors from Tool A, and the only candidates on the form are on the never-collect list. The plan proposes none. See decision 8.

**Events**

**page_view** (existing, reused; change: add one property)
- Moment: step 1 and step 2, and every other page.
- Fires when: any page opens, as it does now. Does not fire when: not stated for this existing event; the builder confirms it fires once per page opened and says how a reload is handled today.
- Answers: Q1.
- Properties: page_type, the kind of page opened. Values: home, range, product, quote, other (other added by the plan). Required: yes. Needed by Q1.
- Goes to: Tool A. Owner: Founder. Built by: Web developer.
- Check once built: open a product page; Tool A shows one page_view with page_type product. Open the home page; one page_view with page_type home.

**quote_submit** (existing, reused; change: add one property)
- Moment: step 3.
- Fires when: the trigger is unchanged; the builder confirms it fires once per quote form sent. Does not fire when: not stated for this existing event; the builder confirms that an attempt that shows an error, a second press of Send on the same form and a reload of the Thank you message add nothing.
- Answers: Q1, Q2.
- Properties: project_type, the project type the visitor chose on the form. Values: dining_table, desk, shelving, other. Required: yes. Needed by Q2.
- Goes to: Tool A. Owner: Founder. Built by: Web developer.
- Check once built: send a test request choosing desk; Tool A shows one quote_submit with project_type desk. Make the form show an error, in a way the builder describes; no event appears. Reload the Thank you page; nothing more appears.

**newsletter_subscribed** (new)
- Moment: step 4.
- Fires when: the You are subscribed message appears. Does not fire when: Subscribe is pressed but Tool B does not accept the address, Subscribe is pressed a second time on the same message, or the message is shown again on reload.
- Answers: Q4.
- Properties: page_type, the kind of page the visitor was on, with the same values as on page_view. Required: yes. Needed by Q4.
- Goes to: Tool A. Owner: Founder. Built by: Web developer.
- Check once built: subscribe from a product page with a test address of your own; Tool A shows one newsletter_subscribed with page_type product. Reload the page; nothing more appears. Press Subscribe with an address Tool B will not accept, which the builder can tell you how to supply; nothing appears.

**Similar names and existing events not reused**

- **signup** (Tool A): not reused. Its description, "A visitor joined something", could cover the newsletter or something else, so the plan cannot tell whether it is the same action as newsletter_subscribed. See decision 4.

**Existing names that break the rule**

- **page_view** (Tool A): the rule would give page_viewed. Kept, not renamed. See decision 2.
- **quote_submit** (Tool A): the rule would give quote_submitted. Kept, not renamed. See decision 3.

Existing events left as they are: signup, which is listed above as not reused. They are left as they are.

**Held for the owner**

- A way to tie individual requests to one person, for Q6: none proposed. See decision 8.

**Not collected**

- Name, email address, message (quote form): on the never-collect list.
- Budget range (quote form): no question needs it.
- Email address (newsletter box): on the never-collect list.

**Coverage:** every event serves at least one question. Questions with an answer in this plan: Q1, Q2, Q4. Questions without: Q3 (not answerable), Q5 (needs rewording), Q6 (held).

**Destinations:** Tool A receives page_view, quote_submit and newsletter_subscribed; owner Founder. Tool B receives no event from this plan; what Tool B stores is outside it.

**Decisions for the Founder: 8**

1. Approve what is collected: three events (page_view, quote_submit, newsletter_subscribed) and two properties (page_type, project_type), including the added property on each of the two existing events, and the page_type value other, which the plan added because the journey names only four kinds of page. Nothing else is collected.
2. page_view does not follow the naming rule; the rule would give page_viewed. It is kept and not renamed. The plan does not know how Tool A treats a renamed event or whether history is joined. Say whether it stays as it is.
3. quote_submit does not follow the naming rule; the rule would give quote_submitted. It is kept and not renamed, with the same unknown about Tool A. Say whether it stays as it is.
4. signup is not reused. Say what fires it today. The plan does not change it.
5. Q3 is not answerable from this plan. Say whether the answer is to be found elsewhere, such as in the order book. Not planned here.
6. Q5 needs rewording and names no decision. Reword it as something a site can count, with the decision it informs, or drop it.
7. Q1 relies on Tool A's own count of visitors, which the plan neither adds to nor changes. Say whether that count is good enough for the budget decision. The builder can say how Tool A counts the same visitor across a product page and a later quote request.
8. Q6 is held. Say whether any way of tying individual requests to one person is to be considered. None is proposed.

**Not supplied:** nothing missing. The plan has not seen how Tool A counts visitors, which Q1 depends on; that is a setting in Tool A. No list of page kinds was supplied, so the page_type values come from the journey, plus other.

Draft for the Founder's approval. Nothing has been built, switched on or sent.
