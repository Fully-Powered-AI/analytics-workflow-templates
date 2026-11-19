# Analysis plan

Before anyone opens the spreadsheet, get a one-page plan: the question, hypotheses, fields and the result that would change the decision.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See Analysis plan on our website](https://fullypowered.ai/workflows/analysis-plan/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the invented ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/analysis-plan/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan)*

## The outcome

The work starts from a decision, not from a pile of exports. The plan says what you are really asking, what you think might be true, which columns and which months would show it, and what result would make you choose one option over another. Whoever does the analysis afterwards, you or an analyst, starts with the same page and the same question.

The plan also shows the gaps while they are cheap to fix. A term with two meanings, a number you have not yet set, a column that no export holds, a period that is still incomplete: each arrives as a numbered question for a named person, before any hours are spent on the wrong cut of the data.

The assistant plans; it does not analyse. It looks at no data, reports no result and fills no gap with an assumption. The question and the decision criteria stay yours.

## Who starts the work, and when

The owner or manager who has a business question starts it, or the analytics lead on their behalf, as soon as the request exists and before anyone opens an export. The decision owner reads and approves the plan before the analysis begins. It can be run again when the question sharpens, a source turns out not to hold what was expected, or the decision date moves.

## What they supply

- **The request note.** The question in the words it was asked, who asked, the decision it feeds, who makes that decision, by when, and the options on the table.
- **A description of each source.** For each export or system: what it holds, one row per what, the column headers, the dates it covers and when it was last refreshed. Headers and descriptions only, never the data itself.
- **Your definitions.** The terms the question uses and what each means in your business.
- **Your settings.** Today's date, who the plan is for, the analytics lead's role and, if you have a rule for it, the smallest group worth reading.
- **Known events.** Changes that might affect the numbers, such as a new supplier, a price change or a new system, with dates.
- **Your hunches,** if you have them, including other people's.

## What comes out

One page where possible, in a fixed order: the question as asked and as restated; the decision and its options; up to five hypotheses, each with what the data would show if it were true and if it were false; the fields and periods needed from each source; the definitions in play; the decision criteria, in your words and numbers; the checks to make before any result is read; and the open questions, each marked blocking or not blocking. The status line says whether the plan is ready to run.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan), where the plan is the first page of every investigation.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan), where orders, campaigns and deliveries sit in separate exports and the question is which one explains a change.
- [Professional services](https://fullypowered.ai/industries/professional-services/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan), where a partner or director asks a question that spans time records, billing and pipeline.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan), where lead times, carriers and customer orders have to be lined up before any pattern means anything.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan), when decisions get bigger faster than the analytics team does.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan), where the data is plentiful, the definitions have drifted, and nobody wants a second argument about what a number means.

## What has to change for your company

Say who may ask for an investigation and who decides what it feeds. Decide the cut-off for a plan being ready: the default blocks on an unclear key term and on a decision criterion with no number, and you may widen or narrow that. Set the smallest group worth reading, if your business has a rule for it. Keep a standing list of your definitions and known events so each plan starts from them. Decide who approves a plan before the work begins.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was run once on its invented example on 10 November 2026, and the record of that run is published with it. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on two or three past questions whose decisions you already know, plus hard cases written in advance: a question with no decision behind it, a criterion with no number, a column that no source holds, a measure that needs ninety days to mature. The analytics lead checks every line against the sources before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan) describes the record we keep.

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

- [Budget-versus-actual variance commentary](https://fullypowered.ai/workflows/budget-versus-actual-variance-commentary/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan)
- [Operations KPI scorecard](https://fullypowered.ai/workflows/operations-kpi-scorecard/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan)
- [Supplier spend analysis](https://fullypowered.ai/workflows/supplier-spend-analysis/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-analysis-plan&from=gh-analytics-analysis-plan).
