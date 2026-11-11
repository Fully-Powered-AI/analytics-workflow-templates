# Tracking event plan: tried on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (`claude-sonnet-5-5`)
- **Date:** 2026-11-10

The inputs are the invented example in [example.md](example.md) (Studio L, Tool A and Tool B). No client data was used. This is the second recorded run. The first run, earlier the same day by a different model session, led to changes in the template's instruction block and output format and in the example (see "What changed since the first run"), so it no longer describes the published template and is replaced by this record. This run was a single attempt by the same model session that revised the template and the example, with the revised example open. It followed the revised instruction block and output format, but it was not written blind, and its agreement with the example is weak evidence for that reason.

## Inputs used

The "The inputs" section of [example.md](example.md), unchanged since the first run: the settings (Studio L, Tuesday 10 November 2026, Founder as runner, approver and event owner, a contractor web developer as builder, the default naming rule, a never-collect list of names, email addresses, phone numbers and anything typed into the message box), six questions, a four-step journey, three existing events and two destinations.

## What changed since the first run

The first run found these points. Each was dealt with in the template and the example.

1. The first run flagged `page_view` as breaking the naming rule and the example did not. The example now flags both `page_view` and `quote_submit`, in a new section "Existing names that break the rule".
2. Q1 needs the same visitor counted across a page view and a later quote request, while Q6 was held for needing that recognition. The template now says a visitor question is measured with the tool's own visitor counting, flagged as a decision, and that a question needing individual records tied to one person is held.
3. The example gave `quote_submit` a trigger the inputs do not state. It now writes the trigger as unchanged, for the builder to confirm.
4. The `other` value for `page_type` is not in the inputs. The template now says to add it, mark it as added by the plan and put it in the first decision.
5. The format now says what to do with a property on two events, with an existing event not reused that no question needs, and with the groups named in the coverage line.

## What came out

```
TRACKING EVENT PLAN: the Studio L website

For: Founder. Prepared Tuesday 10 November 2026, from 6 questions, 4 journey steps, 3 existing events and 2 destinations. Naming rule: default (object, then action in the past tense, lowercase, words joined by underscores). Destinations: Tool A, Tool B.
Counts: Questions 6 (answered 3, not answerable 1, need rewording 1, held 1). Events 3 (1 new, 2 existing reused with a change, 0 existing reused unchanged). Properties 2, each counted once (page_type on 2 events, project_type on 1). Decisions 8.

Questions
Q1. What share of people who look at a piece go on to ask for a quote? Decision it informs: whether the autumn budget goes to the product pages or to advertising. Measure: visitors, as Tool A counts them, who sent at least one quote request, out of visitors, as Tool A counts them, who opened at least one product page, in the same period. Answered by: page_view with page_type product; quote_submit. The plan adds no way to recognise a visitor and relies on Tool A's own count. See decision 7.
Q2. Which kinds of project do quote requests ask about? Decision it informs: which three pieces to photograph for the spring catalogue. Measure: quote requests sent, counted by project type. Answered by: quote_submit with project_type.
Q3. Which quote requests become orders? Decision it informs: whether to follow up every request within a day. Not answerable from this plan: the sale happens outside the website. The plan can count requests but cannot show which became orders; that needs a link between a request and the order book. See decision 5.
Q4. How many people join the newsletter, and from which kind of page? Decision it informs: whether to keep the sign-up box in the footer. Measure: subscriptions completed, counted by the kind of page the visitor was on. Answered by: newsletter_subscribed with page_type.
Q5. Do people like the new homepage? Decision it informs: no decision named. Needs rewording: "like" is not something a site can count, and no decision depends on the answer. No event is planned for it. See decision 6.
Q6. How many people ask for a quote more than once? Decision it informs: whether to merge repeat requests in the office. Held: the decision is to merge repeat requests in the office, which needs individual requests tied to one person, not a count of visitors from Tool A, and the only candidates on the form are on the never-collect list. The plan proposes none. See decision 8.

Events
page_view (existing, reused; change: add one property)
- Moment: step 1 and step 2, and every other page.
- Fires when: any page opens, as it does now. Does not fire when: not stated for this existing event; the builder confirms it fires once per page opened and says how a reload is handled today.
- Answers: Q1.
- Properties: page_type, the kind of page opened. Values: home, range, product, quote, other (other added by the plan). Required: yes. Needed by Q1.
- Goes to: Tool A. Owner: Founder. Built by: Web developer.
- Check once built: open a product page; Tool A shows one page_view with page_type product. Open the home page; one page_view with page_type home.

quote_submit (existing, reused; change: add one property)
- Moment: step 3.
- Fires when: the trigger is unchanged; the builder confirms it fires once per quote form sent. Does not fire when: not stated for this existing event; the builder confirms that an attempt that shows an error, a second press of Send on the same form and a reload of the Thank you message add nothing.
- Answers: Q1, Q2.
- Properties: project_type, the project type the visitor chose in the drop-down. Values: dining_table, desk, shelving, other. Required: yes. Needed by Q2.
- Goes to: Tool A. Owner: Founder. Built by: Web developer.
- Check once built: send a test request choosing desk; Tool A shows one quote_submit with project_type desk. Press Send with a required field empty; no event appears. Reload the Thank you page; nothing more appears.

newsletter_subscribed (new)
- Moment: step 4.
- Fires when: the You are subscribed message appears. Does not fire when: Subscribe is pressed but Tool B does not accept the address, Subscribe is pressed a second time on the same message, or the message is shown again on reload.
- Answers: Q4.
- Properties: page_type, the kind of page the visitor was on, with the same values as on page_view. Required: yes. Needed by Q4.
- Goes to: Tool A. Owner: Founder. Built by: Web developer.
- Check once built: subscribe from a product page with a test address of your own; Tool A shows one newsletter_subscribed with page_type product. Reload the page; nothing more appears. Press Subscribe with an invalid address; nothing appears.

Similar names and existing events not reused
- signup (Tool A): not reused. Its description, "A visitor joined something", could cover the newsletter or something else, so the plan cannot tell whether it is the same action as newsletter_subscribed. See decision 4.

Existing names that break the rule
- page_view (Tool A): the rule would give page_viewed. Kept, not renamed. See decision 2.
- quote_submit (Tool A): the rule would give quote_submitted. Kept, not renamed. See decision 3.

Existing events left as they are: signup, which is listed above as not reused. They are left as they are.

Held for the owner
- A way to tie individual requests to one person, for Q6: none proposed. See decision 8.

Not collected
- Name, email address, message (quote form): on the never-collect list.
- Budget range (quote form): no question needs it.
- Email address (newsletter box): on the never-collect list.

Coverage: every event serves at least one question. Questions with an answer in this plan: Q1, Q2, Q4. Questions without: Q3 (not answerable), Q5 (needs rewording), Q6 (held).

Destinations: Tool A receives page_view, quote_submit and newsletter_subscribed; owner Founder. Tool B receives no event from this plan; what Tool B stores is outside it.

Decisions for the Founder: 8

1. Approve what is collected: three events (page_view, quote_submit, newsletter_subscribed) and two properties (page_type, project_type), including the added property on each of the two existing events, and the page_type value other, which the plan added because the journey names only four kinds of page. Nothing else is collected.
2. page_view does not follow the naming rule; the rule would give page_viewed. It is kept and not renamed. The plan does not know how Tool A treats a renamed event or whether history is joined. Say whether it stays as it is.
3. quote_submit does not follow the naming rule; the rule would give quote_submitted. It is kept and not renamed, with the same unknown about Tool A. Say whether it stays as it is.
4. signup is not reused. Say what fires it today, so it can be reused, renamed or retired. The plan does not change it.
5. Q3 is not answerable from this plan. Say whether the answer is to be found elsewhere, such as in the order book. Not planned here.
6. Q5 needs rewording and names no decision. Reword it as something a site can count, with the decision it informs, or drop it.
7. Q1 relies on Tool A's own count of visitors, which the plan neither adds to nor changes. Say whether that count is good enough for the budget decision. The builder can say how Tool A counts the same visitor across a product page and a later quote request.
8. Q6 is held. Say whether any way of tying individual requests to one person is to be considered. None is proposed.

Not supplied: nothing missing. The plan has not seen how Tool A counts visitors, which Q1 depends on; that is a setting in Tool A. No list of page kinds was supplied, so the page_type values come from the journey, plus other.

Draft for the Founder's approval. Nothing has been built, switched on or sent.
```

## What was observed

- **Every required part was produced.** Counts, all four question forms, events with moment, both triggers, answers, properties, destinations, owners, builders and checks, the lists, coverage, destinations, decisions, the not-supplied line and the closing line. The counts match the lists. Nothing made the run stop, because every input was complete and its headers matched.
- **Agreement with the example.** The recorded plan is word for word the same as the example's plan as it stood at the time of the run (apart from bold marks). That is expected, because the example was revised in the same pass and was open during the run; it does not show a different run would agree.
- **Where the instructions needed a judgement.**
  - Whether the Q6 reason (the decision needs individual requests tied to one person) is clear enough to separate it from Q1. The new wording gave a way to decide, but another reader could rule Q6 answerable with the tool's own visitor counting.
  - Whether `signup` belongs on "Existing events left as they are". The revised format says it does when not reused, and it was listed there.
  - Whether a second press of Subscribe counts as a repeat. It was treated as one and the builder is asked to confirm.
- **Anything told to stop for.** None.
- **Facts not in the inputs.** The property value `other` for `page_type`; the suggested names `page_viewed` and `quote_submitted`; the remarks about reloads and second presses, which are checks for the builder and not facts about the site; the note that Tool A's treatment of a renamed event is unknown.
- **Reviewer checklist.** Read against this plan, all ten points pass. Point 6 holds because both names that break the rule are listed and flagged. Point 5 holds because nothing was renamed or dropped.
- **Limits of this trial.** One run, one model, one invented example, and the example was in view when the plan was written. It shows the revised template can be followed to a complete plan on a small case. It does not show that a different run would flag the same items.

## Edits made after this run

The record above is unchanged. After a review, small edits were made that this run did not see, and the plan above is not a run of them:

- **Example.** Decision 4 no longer says `signup` could be "reused, renamed or retired", because the template says never to rename an existing event and to recommend nothing. The words "drop-down", "a required field empty" and "an invalid address" in the example were replaced by wording that does not assume facts the inputs never state. The recorded plan above still carries the earlier wording; those phrases were builder checks and one suggestion, not facts from the inputs, and decision 4 went beyond the template's rule.
- **Template.** One sentence in procedure step 3 and in the instruction block says when "how many people" is answered by counting events and when by the tool's visitor counting, and the block now says to count the inputs for the header. These clarify how the Q1, Q4 and Q6 lines were already treated; they were not re-run.
