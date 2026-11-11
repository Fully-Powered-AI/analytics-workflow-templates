# Dashboard brief

Before anyone builds the dashboard, the requester gets one brief that settles the work: the decisions it serves, what is shown, each metric's definition, the filters, notes on every source and who refreshes it. The requester approves what is shown and the definitions.

*Capability template · Analytics and reporting · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/dashboard-brief/)*

## The outcome

A dashboard built from a settled brief answers a question somebody has to answer. A dashboard built from a request such as "we need a dashboard for sales" shows whatever was easy to chart. This capability turns the request into a short document that the requester, the person who owns the data and the person who builds can all read and agree to before a single chart exists.

Each decision the dashboard serves is written as a choice with a named decider and a rhythm. Each metric is defined once, in the exact columns of the export it reads. Each filter is checked against the data it would act on. Each source is described: what a row is, what dates it covers, when it was pulled and who owns it. Anything that cannot be built as asked is said so, and written as a question.

## Who starts the work, and when

The person asked to build a dashboard in a spreadsheet or a reporting tool starts it, before building: an analyst, an operations manager, a finance lead or whoever has been handed the request. The requester, who will use the dashboard to decide something, answers the questions and approves the brief. The owner of each export confirms its source notes.

## What they supply

- Notes from the requester: what they want to decide, who will look, how often, where it will be built, the reporting grain, and any limits on who may see what.
- A decision sheet: one row per decision, with who decides and how often.
- A metric list: one row per metric, with its meaning, formula, source and the decisions it serves.
- A source sheet describing each export: what it holds, what one row is, its columns, its dates, when it was pulled and who owns it.
- The date the brief is prepared, and who will refresh the dashboard.

## What comes out

One brief in a fixed order: the decisions served; what is shown, view by view; every metric definition; the filters and where each applies; notes on each source; the refresh owner and steps; what was left off and why; checks on the inputs; numbered questions for the requester; and approval lines. The brief holds no figures. A layout is described with placeholders, never sample values.

Metrics that cannot be built from the exports supplied are left off and explained, not quietly dropped or filled in. When the columns in any sheet do not match the ones the work expects, it stops and asks which column is which.

It stays separate from two neighbours. A fixed monthly scorecard of ten or fewer measures belongs to the [Operations KPI scorecard](https://fullypowered.ai/capabilities/operations-kpi-scorecard/), and the owner's weekly one-pager belongs to the [Weekly owner business brief](https://fullypowered.ai/capabilities/weekly-owner-business-brief/). This one settles a new dashboard before it exists.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/), where a request for a dashboard arrives before anyone has agreed what it is for.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where utilization, billing and pipeline views are asked for by partners and leads who each mean something slightly different.
- [Ecommerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where orders, ad spend and stock sit in separate exports that have to be joined by name.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where product, support and revenue numbers are asked for in one view.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), where the numbers live in several systems and one person's spreadsheet.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/), when leaders start asking for a regular view they used to carry in their heads.

## What has to change for your company

Decide who counts as the requester, each export owner and the refresh owner, so each approval has a name. Set the limits that suit you: how many decisions, metrics and filters one dashboard may carry, how many periods a trend shows, and how old an export may be before it is flagged. Fix your rounding and your week start. Say where the approved brief is kept and who builds from it. It runs in ChatGPT, Claude, Copilot or Gemini, from the sheets and exports you supply; it needs no access to any system and asks for no password or login code.

## What has been checked

Fully Powered AI wrote this capability template. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026 in two runs: the instructions were revised after the first, and the second is the run published with the example. That run was not fully blind, because the example's earlier output had been read; the record says so and lists what the first run found. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a dashboard request your analyst already settled by hand, with hard cases written in advance: a renamed export column, a metric nobody can name a decision for, a grain finer than the export holds, a filter with no column behind it, an export that is a week old. The requester and the data owner check every definition and every source note before anyone relies on the brief. [Pilot acceptance-test preparation](https://fullypowered.ai/capabilities/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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

- [Operations KPI scorecard](https://fullypowered.ai/capabilities/operations-kpi-scorecard/)
- [Weekly owner business brief](https://fullypowered.ai/capabilities/weekly-owner-business-brief/)
- [Spreadsheet check before sharing](https://fullypowered.ai/capabilities/spreadsheet-check-before-sharing/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
