# Metric definition reconciliation

When two reports show different numbers, get the definitions side by side, the gap bridged from your records and a proposed common measure. You choose.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See Metric definition reconciliation on our website](https://fullypowered.ai/workflows/metric-definition-reconciliation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the invented ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/metric-definition-reconciliation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation)*

## The outcome

The argument about which number is right stops being an argument about numbers. The owner sees, element by element, where the two reports differ: the source, the population counted, the exclusions, the date and time zone, what is summed, how refunds and adjustments are treated. Where each report's records are supplied, the gap is bridged step by step from one reported figure to the other, and the steps add up to it.

Each likely cause is labelled by how well it is supported. Some are shown by the records themselves. Some are only consistent with the definitions. Anything left over is stated as unexplained, never smoothed away. A small gap can hide large differences that cancel; the page says so when it happens.

The page ends with a proposed common measure, built from the purpose of the figure, and with a list of the cases where both reports are right and deserve different names. The metric owner decides. The workflow template never says one figure is correct.

## Who starts the work, and when

An analyst, a finance lead or a report owner starts it when two teams report different values for the same metric, usually after a meeting where both numbers were on screen. The metric owner reviews the page and decides the definition. Analytics then documents the agreed computation.

## What they supply

- A definition sheet for each report: the formula in words, the source, what one row is, what is included and excluded, the date used and its time zone, how refunds and adjustments are treated, the unit and when the data was pulled.
- Each report's value for the period, as it shows today.
- Where possible, an extract of the records each report counts, with a record number, a date, the amount counted and a status.
- What the figure is used for, and who owns the metric.

## What comes out

One page in a fixed order: the reported values and the gap, the definitions side by side, the record comparison, the bridge from one figure to the other, the causes in three groups (shown, consistent with, not explained), the cases where both are right, a proposed common measure and the questions the owner has to answer. With no extracts, the page gives likely causes from the definitions alone and says which extract would test each.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation), where the definition of a metric should travel with the query that produces it.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation), where finance, marketing and the shop platform each count sales a little differently.
- [Software and technology](https://fullypowered.ai/industries/software-technology/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation), where product, finance and sales report customers and revenue from different systems.
- [Professional services](https://fullypowered.ai/industries/professional-services/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation), where utilization and billed hours come from time entry and from billing.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation), where each department has run its own report for years.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation), when a new reporting tool starts disagreeing with the old one.

## What has to change for your company

Fix the fields on your definition sheet so every report owner can fill it in the same way. Decide who owns each shared metric, and who documents the agreed computation. Set the columns of your record extracts once. Agree what counts as a separate measure worth its own name, and where the agreed definitions are kept. It works from files you supply in ChatGPT, Claude, Copilot or Gemini and needs no connection to a reporting tool.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026; the record of that run is published with it. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a past disagreement your analyst already resolved, with cases written in advance: a gap that is mostly offsetting differences, an extract that does not add up to its report, a definition sheet with a field left blank. The analyst checks every figure in the bridge against the extracts before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation) describes the record we keep.

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

- [Spreadsheet check before sharing](https://fullypowered.ai/workflows/spreadsheet-check-before-sharing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation)
- [Operations KPI scorecard](https://fullypowered.ai/workflows/operations-kpi-scorecard/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation)
- [Budget-versus-actual variance commentary](https://fullypowered.ai/workflows/budget-versus-actual-variance-commentary/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-metric-definition-reconciliation&from=gh-metric-definition-reconciliation).
