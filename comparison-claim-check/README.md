# Comparison claim check

Hold a claim like version B converts better against two groups of numbers and get the method, the size of the difference and plain wording. You decide.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See Comparison claim check on our website](https://fullypowered.ai/workflows/comparison-claim-check/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the invented ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/comparison-claim-check/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check)*

## The outcome

Someone says the new page, the new offer or the new process did better, and shows two columns of numbers. Before anyone changes anything, the manager gets one page that answers four questions. How big is the difference? How sure can we be that it is more than luck? Were the groups fair to compare? And what can honestly be said about it in a meeting?

The page names the method used and why it fits, gives the difference in plain units and as a range, and checks the things that quietly break a comparison: how the groups were formed, whether the split matches the plan, whether results were watched and the test stopped when it looked good, and whether several comparisons were tried until one worked (if that number is not given, the result cannot be called strong). It then states one of four support levels and the wording the data allows.

The workflow template never says a change caused a result unless the groups were assigned at random, and it never turns a thin result into a confident one. The manager decides whether to act.

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

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check), where a claim should be checked before it travels.
- [Marketing and content](https://fullypowered.ai/functions/marketing-and-content/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check), for page, subject-line and offer comparisons.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check), where checkout, pricing and promotion changes are tried on live visitors.
- [Software and technology](https://fullypowered.ai/industries/software-technology/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check), for product experiments and release comparisons.
- [Marketing and advertising](https://fullypowered.ai/industries/marketing-and-advertising/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check), where one campaign variant is said to beat another.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check), when many changes are being tried quickly and each needs an honest reading.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check), when a pilot in one branch or team is the basis for a wider change.

It is not a review of why deals were won or lost (see [win-loss review](https://fullypowered.ai/workflows/win-loss-review/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check)) or a grouping of what customers say ([customer feedback themes](https://fullypowered.ai/workflows/customer-feedback-themes/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check)). It compares two groups on one outcome.

## What has to change for your company

Decide the usual confidence level and keep it for every claim. Write down the smallest difference that would justify the cost of a change in each area you test. Fix the unit of counting for your main outcomes: a person, a visit or an order. Decide who must read the page before a result is quoted outside the team. Name the tool the assistant is allowed to calculate with, so every figure can be rerun.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was run twice on its invented example in Claude on 10 November 2026, both times by the session that wrote and revised it, so neither run was blind; the record of the second run is published beside it. It has not yet been tested in a client environment.

Testing in your environment means running it on comparisons whose answers you already know: a real difference, no difference, a split that does not match the plan, and a result that was peeked at. The analyst should recompute every figure before the page is relied on.

- Written by FullyPowered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete workflow template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the workflow template drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related workflow templates

- [Win-loss review](https://fullypowered.ai/workflows/win-loss-review/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check)
- [Customer feedback themes](https://fullypowered.ai/workflows/customer-feedback-themes/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check)
- [Operations KPI scorecard](https://fullypowered.ai/workflows/operations-kpi-scorecard/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-comparison-claim-check&from=gh-analytics-comparison-claim-check).
