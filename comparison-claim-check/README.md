# Comparison claim check

A manager holding a claim such as "version B converts better" and two groups of numbers gets back the method used, the size of the difference, how uncertain it is, the assumptions checked, and plain wording for what the data does and does not support. The manager decides what to do.

*Capability template · Analytics and reporting · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/comparison-claim-check/)*

## The outcome

Someone says the new page, the new offer or the new process did better, and shows two columns of numbers. Before anyone changes anything, the manager gets one page that answers four questions. How big is the difference? How sure can we be that it is more than luck? Were the groups fair to compare? And what can honestly be said about it in a meeting?

The page names the method used and why it fits, gives the difference in plain units and as a range, and checks the things that quietly break a comparison: how the groups were formed, whether the split matches the plan, whether results were watched and the test stopped when it looked good, and whether several comparisons were tried until one worked (if that number is not given, the result cannot be called strong). It then states one of four support levels and the wording the data allows.

The capability never says a change caused a result unless the groups were assigned at random, and it never turns a thin result into a confident one. The manager decides whether to act.

## Who starts the work, and when

An analyst, a marketing or product manager, or an owner starts it when a claim about a difference is about to be believed or acted on: a test has finished, a pilot has run for a month, or someone has pasted two sets of results into a message. The person who owns the decision reads the result.

## What they supply

- The claim, in the words it was made, and which group is said to be better on which outcome.
- The data: either a short summary per group (how many, and how many succeeded, or the average and spread) or one row per record with the group and the outcome.
- How the groups were formed: assigned at random by a system, chosen by people, or simply different periods or places.
- What counts as success, over what period, and whether each row is a person, a visit or an order.
- How many comparisons were looked at on this outcome, and whether anyone watched the results and stopped early.
- Optionally, the smallest difference that would matter to the business.

## What comes out

One page in a fixed order: the support level, the claim, what was compared, the method, the result with its range, seven assumption checks each marked as passed, flagged or not checkable, what the data supports, what it does not support, questions for the manager, and a sentence that can go into a report. Where a section has nothing to say it says so.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/), where a claim should be checked before it travels.
- [Marketing and content](https://fullypowered.ai/functions/marketing-and-content/), for page, subject-line and offer comparisons.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where checkout, pricing and promotion changes are tried on live visitors.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), for product experiments and release comparisons.
- [Marketing and advertising](https://fullypowered.ai/industries/marketing-and-advertising/), where one campaign variant is said to beat another.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/), when many changes are being tried quickly and each needs an honest reading.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), when a pilot in one branch or team is the basis for a wider change.

It is not a review of why deals were won or lost (see [win-loss review](https://fullypowered.ai/capabilities/win-loss-review/)) or a grouping of what customers say ([customer feedback themes](https://fullypowered.ai/capabilities/customer-feedback-themes/)). It compares two groups on one outcome.

## What has to change for your company

Decide the usual confidence level and keep it for every claim. Write down the smallest difference that would justify the cost of a change in each area you test. Fix the unit of counting for your main outcomes: a person, a visit or an order. Decide who must read the page before a result is quoted outside the team. Name the tool the assistant is allowed to calculate with, so every figure can be rerun.

## What has been checked

Fully Powered AI wrote this capability template. It was editorially reviewed on 10 November 2026. It was run twice on its invented example in Claude on 10 November 2026, both times by the session that wrote and revised it, so neither run was blind; the record of the second run is published beside it. It has not yet been tested in a client environment.

Testing in your environment means running it on comparisons whose answers you already know: a real difference, no difference, a split that does not match the plan, and a result that was peeked at. The analyst should recompute every figure before the page is relied on.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete capability template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the capability drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related capabilities

- [Win-loss review](https://fullypowered.ai/capabilities/win-loss-review/)
- [Customer feedback themes](https://fullypowered.ai/capabilities/customer-feedback-themes/)
- [Operations KPI scorecard](https://fullypowered.ai/capabilities/operations-kpi-scorecard/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
