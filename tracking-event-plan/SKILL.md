---
name: "tracking-event-plan"
description: "Prepare the plan for what a website or app should record, before anyone builds it: the events, the properties each carries, the exact moment each fires, where each goes, what each is called and who owns it, every one tied to a question the business needs answered. The plan also says which questions it cannot answer, which existing events it did not reuse, which fields it holds back for the owner and which it leaves uncollected. The assistant prepares; it writes no tracking code, switches nothing on, changes no tool and decides nothing about what is collected. It gives no advice about privacy rules or consent notices."
license: "MIT"
metadata:
  version: "0.1.0"
  publisher: "Fully Powered AI"
  template: "Tracking event plan"
---

# Tracking event plan

This is the technical file for a Fully Powered workflow template. It carries the instructions an AI product follows. The complete template, with roles, inputs, exceptions, the reviewer checklist, acceptance tests and what to customize, is in [TEMPLATE.md](TEMPLATE.md). A worked example with invented data is in [EXAMPLE.md](EXAMPLE.md).

## Instructions

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

## Before relying on it

Decide every item under "What to customize" in TEMPLATE.md and set the limits the instructions in this file leave open, written in square brackets such as [N], to your own. Then run the acceptance tests in TEMPLATE.md on past work. A person starts this work, supplies the inputs and decides what happens with the result.
