# Metric definition reconciliation

When two reports give different numbers for one metric, the owner gets a page: the definitions side by side, the gap bridged step by step from supplied records, each cause marked shown or not, and a proposed common measure. The owner chooses.

*Capability template · Analytics and reporting · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/metric-definition-reconciliation/)*

## The outcome

The argument about which number is right stops being an argument about numbers. The owner sees, element by element, where the two reports differ: the source, the population counted, the exclusions, the date and time zone, what is summed, how refunds and adjustments are treated. Where each report's records are supplied, the gap is bridged step by step from one reported figure to the other, and the steps add up to it.

Each likely cause is labelled by how well it is supported. Some are shown by the records themselves. Some are only consistent with the definitions. Anything left over is stated as unexplained, never smoothed away. A small gap can hide large differences that cancel; the page says so when it happens.

The page ends with a proposed common measure, built from the purpose of the figure, and with a list of the cases where both reports are right and deserve different names. The metric owner decides. The capability never says one figure is correct.

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

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/), where the definition of a metric should travel with the query that produces it.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where finance, marketing and the shop platform each count sales a little differently.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where product, finance and sales report customers and revenue from different systems.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where utilization and billed hours come from time entry and from billing.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), where each department has run its own report for years.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/), when a new reporting tool starts disagreeing with the old one.

## What has to change for your company

Fix the fields on your definition sheet so every report owner can fill it in the same way. Decide who owns each shared metric, and who documents the agreed computation. Set the columns of your record extracts once. Agree what counts as a separate measure worth its own name, and where the agreed definitions are kept. It works from files you supply in ChatGPT, Claude, Copilot or Gemini and needs no connection to a reporting tool.

## What has been checked

Fully Powered AI wrote this capability template. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026; the record of that run is published with it. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a past disagreement your analyst already resolved, with cases written in advance: a gap that is mostly offsetting differences, an extract that does not add up to its report, a definition sheet with a field left blank. The analyst checks every figure in the bridge against the extracts before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/capabilities/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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

- [Spreadsheet check before sharing](https://fullypowered.ai/capabilities/spreadsheet-check-before-sharing/)
- [Operations KPI scorecard](https://fullypowered.ai/capabilities/operations-kpi-scorecard/)
- [Budget-versus-actual variance commentary](https://fullypowered.ai/capabilities/budget-versus-actual-variance-commentary/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
