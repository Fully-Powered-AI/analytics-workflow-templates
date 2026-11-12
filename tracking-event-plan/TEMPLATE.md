# Tracking event plan

Workflow template, version 0.1.0.

## Purpose

Prepare the plan for what a website or app should record, before anyone builds it: the events, the properties each carries, the exact moment each fires, where each goes, what each is called and who owns it, every one tied to a question the business needs answered. The plan also says which questions it cannot answer, which existing events it did not reuse, which fields it holds back for the owner and which it leaves uncollected. The assistant prepares; it writes no tracking code, switches nothing on, changes no tool and decides nothing about what is collected. It gives no advice about privacy rules or consent notices.

## When to use it and when not to

Use it before a site or app is instrumented, when a new feature or step needs measuring, or when an existing set of events has grown names nobody trusts. Run it again when the questions change.

Do not use it:

- to write or review tracking code, tag set-ups or tool configuration. The builder does that from the approved plan;
- to read reports, explain a number that moved or check an analysis. Other workflow templates do that once data exists;
- to say whether collecting something is allowed. That is for the owner and whoever advises them;
- to audit whether search engines can find the pages, which is the website findability audit, or to plan a free resource, which is the lead magnet plan;
- when there are no questions. The owner writes the first list; this workflow template does not invent them.

## Roles

- **Runs it:** the founder, product owner or marketing lead.
- **Approves what is collected:** the approver named in the settings. Always a person.
- **Owns what each event means:** the event owner named in the settings.
- **Builds the events and confirms each trigger can be built as written:** the builder named in the settings.
- **Owns each destination:** the person named against it in the destinations list.

## Inputs

1. **The questions,** one per line. Default headers: `id,question,decision it informs,asked by`. If the headers do not match, stop and ask which column is which. If there are no questions, stop. A question with no decision is kept and flagged. Two questions with the same id: stop and ask.
2. **The journey:** the steps a visitor or user takes. Default headers: `step,where,what the visitor does,what the site does`. If the headers do not match, stop and ask. If there is no journey, stop.
3. **The events already collected,** if any. Default headers: `event_name,description,destination`. If the headers do not match, stop and ask. If none is supplied, write "no existing events supplied". Two rows with the same event_name: stop and ask.
4. **The destinations.** Default headers: `destination,used for,owner`. If the headers do not match, stop and ask. If none is supplied, stop: an event with nowhere to go is not a plan.
5. **The settings:** the business, today's date, the workflow named, who runs it, the approver, the event owner, the builder, the naming rule and the never-collect list. If the approver is missing, stop and ask. If the event owner or builder is missing, write "owner not assigned" or "builder not assigned" where it applies; never choose one. If the naming rule is missing, use the default in step 5 and say so. If the never-collect list is missing, write "never-collect list not supplied" and treat every field in step 7 as held.

The assistant works from the notes and files the person supplies. It needs no connection to any analytics tool or to the site, and it never asks for a password or a login code.

## The procedure

1. **Check the inputs.** Confirm one workflow, the questions, the journey, the destinations and the approver. Count the questions, journey steps, existing events and destinations; these four counts go in the header. Apply the stop conditions in the inputs.
2. **Sort the questions.** Keep each question's id and wording. Set each into one group:
   - **Measurable:** a count, a rate, a time between two moments, or a split of a count, can answer it from moments in the journey.
   - **Needs rewording:** the question names nothing a site or app can count, such as whether people "like" something. Say why. Plan nothing for it.
   - **Not answerable from this plan:** the answer sits outside the journey, such as a sale made offline. Say what is missing. Plan nothing for it.
   - **Held:** answering it would need a detail in step 7's held list, or a link between individual records and one person. Say which and plan nothing for it.
   A question with no decision is flagged "no decision named" whichever group it falls in.
3. **Write each measure.** For a measurable question, state what is counted and out of what, over the same period. Name the journey moments it needs. A rate always names both the top and the bottom. A question about visitors is measured with the analytics tool's own visitor counting, as the tool already provides it: write "visitors, as [tool] counts them", propose no identifier, and flag the dependency for the approver (step 12). Do not claim more than the tool's count can show. A "how many people" question whose thing counted is the action itself, such as subscriptions completed or requests sent, is measured by counting that event, and the measure says so; use the tool's visitor counting only when the question is about visitors, as in a rate out of visitors.
4. **Choose the moments.** A moment in the journey becomes an event only if a measurable question needs it. A moment no question needs is not planned. List every field the journey asks the person for that the plan does not collect, with the reason: on the never-collect list, or no question needs it.
5. **Name the events.** Default rule: object, then the action in the past tense, lowercase, words joined by underscores, for example `newsletter_subscribed`. One name, one action: two places that do the same action share one event and a property that says where. Never give two names to one moment.
6. **Compare with the existing events.** For each event needed:
   - If an existing event describes the same moment, reuse it. Do not create a second event for the moment. If properties must be added, mark it "existing, reused; change: ...". If nothing is added, mark it "existing, kept as is".
   - If an existing name does not follow the naming rule, keep it and list it under "Existing names that break the rule" with the name the rule would give, and flag it for the owner. Never rename an existing event.
   - If an existing event's description is broader or vaguer than the moment, or its name is close to a new one (same words in another order, same object with another action), do not reuse it and do not assume it is the same. List it under "Similar names and existing events not reused" and flag it for the owner.
   - Existing events that no question needs, and existing events not reused, are left alone and listed together as left as they are. Never recommend removing them.
7. **Choose the properties.** A property is a detail added to an event so a question can be split or filtered. Add one only if a measurable question needs it. Name it with the same rule (lowercase nouns joined by underscores). Give its meaning, its values and whether it is required. Values come from the journey (the kinds of page, the choices a form offers) as a fixed list. Where the journey does not name every kind, add "other", mark it "added by the plan" and include it in the first decision for the approver to confirm. A property whose values are typed by the visitor is not proposed. In the header count, a property counts once however many events carry it. The following are held, never proposed, even when a question needs them: anything that identifies a person (name, email address, phone number, postal address, account or customer number, an identifier the plan would add to recognise the same person), anything on the never-collect list, anything a visitor types freely, and payment details. Put them under "Held for the owner" with the question that needs them. Money amounts and counts that belong to the business, such as the value of an order, are not held. Nor is the tool's own visitor counting (step 3), which the plan uses and does not change. A question whose decision needs particular records tied to the same person, such as merging one person's requests, is held.
8. **Write the trigger.** For each event, one plain sentence for when it fires, naming the visible moment (a message appears, a page finishes opening), and one for when it does not fire, covering the attempt that fails, the repeat and the reload. For a reused event whose trigger is unstated, write that the trigger is unchanged and the builder confirms it fires once per occurrence.
9. **Assign destinations and owners.** Each event goes to the destinations from the list that serve its questions. An event with no destination, or one that would go to a destination not on the list, is flagged. Take the event owner and the builder from the settings; where none is given, write "owner not assigned". A destination that receives no event is listed with that fact. The plan says nothing about what a destination stores.
10. **Write a check for each event.** Two or three plain steps a person can follow once it is built, saying what should appear and, for a trigger that must not fire, that nothing appears. Use test details the person owns. Do not write code.
11. **Check coverage.** Every event serves at least one question; every measurable question has at least one event. List the questions with no answer in the plan and the group each fell into.
12. **Write the decisions.** Number them for the approver. The first is always approval of what is collected: the events and properties by name, including every change to an existing event and every value added by the plan. Then one decision for each flagged item, in the order they appear: an existing name that breaks the rule, an existing event not reused, a question not answerable, a question to reword, a measure that relies on the tool's own visitor counting, a held detail, a missing owner or builder, an unlisted destination. State the facts; recommend nothing unless the approver asks.
13. **Return the draft** to the person who ran it, for the approver. The approver settles the decisions; the builder confirms the triggers; a person builds.

## Exceptions and stop conditions

- **No questions, no journey, no destinations or no approver:** stop and ask. Do not supply questions or a standard event list.
- **Headers do not match the defaults:** stop and ask which column is which.
- **Duplicate question ids or duplicate event names:** stop and ask.
- **A question needs a held detail:** plan nothing for it; hold it and say which detail.
- **Asked to add a field to the plan that is held or on the never-collect list:** decline; the approver decides and the plan stays as written until they do.
- **Asked to write tracking code, set up a tool, say whether collecting something is allowed, or switch anything on:** decline and name the role that does it. Record the question as a decision.
- **The notes contain a password, a login code or a key to a tool:** do not repeat it in the plan; tell the person to remove it from the source.
- **Asked to recommend which question matters most, or to make a question answerable by choosing a different measure:** decline; list the options only if the approver asks.

## Output format

```
TRACKING EVENT PLAN: [workflow]

For: [approver role]. Prepared [date], from [n] questions, [n] journey steps, [n] existing events and [n] destinations. Naming rule: [rule / default]. Destinations: [names].
Counts: Questions [n] (answered [n], not answerable [n], need rewording [n], held [n]). Events [n] ([n] new, [n] existing reused with a change, [n] existing reused unchanged). Properties [n], each counted once ([name] on [n] events, ...). Decisions [n].

Questions
[id]. [Question] Decision it informs: [decision / no decision named]. Measure: [what is counted, out of what, same period; "visitors, as [tool] counts them" for visitors]. Answered by: [events and properties]. [Where a visitor count is used: See decision [n].]
[id]. [Question] Decision it informs: [...]. Not answerable from this plan: [what is missing]. See decision [n].
[id]. [Question] Decision it informs: [...]. Needs rewording: [why]. No event is planned for it. See decision [n].
[id]. [Question] Decision it informs: [...]. Held: [which detail and why]. See decision [n].

Events
[event_name] ([new / existing, reused; change: ... / existing, kept as is])
- Moment: [journey steps].
- Fires when: [...]. Does not fire when: [...].
- Answers: [ids].
- Properties: [name, meaning. Values: [list]. Required: [yes / no]. Needed by [id].] / none
- Goes to: [destinations]. Owner: [role / owner not assigned]. Built by: [role / builder not assigned].
- Check once built: [steps and what should appear].
[No events: write "No events planned: no question can be answered from the journey."]

Similar names and existing events not reused
- [event_name] ([destination]): [why not reused]. See decision [n].
[Or: None.]
Existing names that break the rule
- [event_name] ([destination]): the rule would give [name]. Kept, not renamed. See decision [n].
[Or: None.]

Existing events left as they are: [names / none], including any listed above as not reused. They are left as they are.

Held for the owner
- [Detail] for [id]: none proposed. See decision [n].
[Or: None.]

Not collected
- [Field] ([where on the journey]): [on the never-collect list / no question needs it].
[Or: None.]

Coverage: [every event serves at least one question / the events that serve none]. Questions with an answer in this plan: [ids]. Questions without: [ids, each with its group: not answerable / needs rewording / held].

Destinations: [name] receives [events]; owner [role]. [name] receives no event from this plan; what it stores is outside it.

Decisions for the [approver role]: [n]
1. Approve what is collected: [events and properties by name, including each change to an existing event]. Nothing else is collected.
[n]. [The facts and the question, one for each flagged item.]

Not supplied: [what was missing and what it affected / nothing missing; "no existing events supplied" where that applies]. [Anything the plan could not see, including how the tool counts visitors where a measure relies on it.]

Draft for the [approver role]'s approval. Nothing has been built, switched on or sent.
```

## Reviewer checklist

1. Every event serves at least one question that is on the list. (Event owner)
2. Every property is needed by a named question and takes its values from a fixed list. (Event owner)
3. No held detail or never-collect field appears in any event. (Approver)
4. Each trigger names a visible moment and says when it does not fire. (Builder)
5. No existing event was renamed or dropped, and each existing event that was reused or left out is accounted for. (Event owner)
6. Every name follows the naming rule, or is an existing name flagged for the owner. (Event owner)
7. The counts in the header match the lists below them. (Person who ran it)
8. Every destination is on the supplied list and its owner is named. (Approver)
9. Every flagged item has a decision, and the first decision names everything collected. (Approver)
10. The plan contains no code and no statement about whether collecting something is allowed. (Approver)

## Acceptance tests

Proposed tests. None has been run.

1. **Ordinary plan.** Three measurable questions, a four-step journey, three existing events, two destinations. Expected: every event tied to a question, properties from fixed lists, counts that match, decision 1 naming everything.
2. **Question with no decision.** Expected: kept, flagged "no decision named", still measured if measurable.
3. **Vague question.** "Do people like the new page?" Expected: "Needs rewording", no event, a decision.
4. **Question answered elsewhere.** A sale made offline. Expected: "Not answerable from this plan", what is missing, no event.
5. **Question that needs a person's email.** Expected: held, nothing proposed, a decision; the email is not added even when asked to.
6. **Existing event with a vague description.** "A visitor joined something". Expected: not reused, listed with the reason, a decision.
7. **Existing name that breaks the rule.** Expected: kept, flagged, the rule's name shown, never renamed.
8. **Two journey places, one action.** The same sign-up box on every page. Expected: one event with a property for the page kind.
9. **Field no question needs.** A budget drop-down. Expected: under "Not collected", no property.
10. **Headers do not match.** Questions supplied with columns in another order and other names. Expected: stops and asks.
11. **No destinations.** Expected: stops and asks.
12. **Asked to write code or to say if collecting is allowed.** Expected: declines, names the role, records a decision.
13. **Free-text property.** A message box proposed as a property. Expected: held, not proposed.
14. **Question about visitors in a period.** Expected: measured as "visitors, as the tool counts them", no identifier proposed, a decision to confirm the tool's counting.
15. **Existing events with a name that breaks the rule and an unstated trigger.** Expected: listed under "Existing names that break the rule" with the name the rule would give; trigger written as unchanged, builder to confirm.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a tracking event plan for the founder or product owner of a
website or app. You write the plan only. You never write tracking code,
change a tool, switch anything on, send anything, or decide what is
collected: a person approves that. You give no advice about privacy rules
or consent notices, and you never ask for a password or a login code.

The user will supply: the questions (default headers id, question, decision
it informs, asked by); the journey (step, where, what the visitor does,
what the site does); the existing events, if any (event_name, description,
destination); the destinations (destination, used for, owner); and the
settings (business, date, workflow, who runs it, approver, event owner,
builder, naming rule, never-collect list). If a header does not match,
stop and ask. If there are no questions, no journey, no destinations or no
approver, stop and say so. Two questions with one id, or two events with
one name: stop and ask. If no existing events are supplied, write "no
existing events supplied". Count the questions, journey steps, existing
events and destinations for the header. If the naming rule is missing, use the default
below and say so. If the never-collect list is missing, write
"never-collect list not supplied" and treat every field in step 6 as held.

1. Sort each question: measurable, needs rewording (names nothing a site
   can count), not answerable from this plan (the answer is outside the
   journey; say what is missing), or held (needs a held detail, or needs
   individual records tied to one person). A question with no decision is
   flagged "no decision named".
2. For a measurable question, state what is counted and out of what, over
   the same period. A rate names both parts. For visitors, write "visitors,
   as [tool] counts them", propose no identifier, and flag the dependency
   for the approver. A "how many people" question whose thing counted is
   the action itself (subscriptions completed, requests sent) is measured
   by counting that event, and the measure says so; use the tool's visitor
   counting only when the question is about visitors, as in a rate out of
   visitors.
3. A journey moment becomes an event only if a measurable question needs
   it. List the fields the journey asks for that you do not collect, with
   the reason.
4. Name events as object then past-tense action, lowercase with
   underscores, unless the settings give another rule. Two places doing one
   action share one event and a property for where.
5. Reuse an existing event for the same moment; never create a second one.
   Never rename or drop an existing event. If an existing name breaks the
   rule, keep it and list it with the name the rule would give, and flag
   it. If an existing description is vaguer than the moment, or a name is
   close to a new one, do not reuse it; list it and flag it. Existing
   events no question needs, and those not reused, are listed as left as
   they are; never recommend removing them.
6. Add a property only if a measurable question needs it, with a name,
   meaning, fixed list of values taken from the journey and whether it is
   required. Where the journey does not name every kind, add "other", mark
   it as added by you and put it in the first decision. Count each property
   once in the header. Hold, never propose: anything that identifies a
   person or that you would add to recognise the same person, anything on
   the never-collect list, anything typed freely, payment details. The
   tool's own visitor counting is not held. If asked to add a held field,
   decline.
7. For each event write when it fires and when it does not (the attempt
   that fails, the repeat and the reload), naming the visible moment. For
   a reused event whose trigger is unstated, write that the trigger is
   unchanged and the builder confirms it fires once per occurrence. Add its
   destinations from the supplied list; its owner and builder from the
   settings (never choose one; write "owner not assigned" or "builder not
   assigned"); and two or three plain steps to check it once built.
8. Check coverage, then list decisions for the approver: first, approval
   of everything collected by name, including each change to an existing
   event and each value you added; then one for each flagged item. State
   facts. Recommend nothing unless asked.
9. Use the output format exactly. End: "Draft for the [approver role]'s
   approval. Nothing has been built, switched on or sent."

Decline to write code, to set up a tool, to say whether collecting
something is allowed, or to change a figure or a measure so a question
looks answerable. Name the person who does that instead.
```

## What to customize

- Your naming rule, if the business has one.
- The never-collect list, so it is held every time.
- The default roles: approver, event owner and builder.
- The fixed lists of values for common properties, such as the kinds of page.
- Your destinations, what each is for and who owns each.
- Any value lists the business already uses for properties, so the plan uses them instead of adding "other".
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Tried on its invented example by Claude on 10 November 2026 (the second recorded run, which replaced a first; see the trial record in the public folder); not yet tested in a client environment.
