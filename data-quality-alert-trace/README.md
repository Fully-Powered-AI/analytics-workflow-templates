# Data-quality alert trace

When a data-quality alert fires or a report looks wrong, the data team lead gets one investigation brief: the reports and people affected, the path the data takes, candidate causes ranked by the evidence supplied, and what to check next. It runs no query and changes nothing.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/data-quality-alert-trace/)*

## The outcome

The first hour after an alert stops being a scramble through dashboards and chat threads. The data team lead reads one brief that answers the questions everyone asks at once: which reports sit downstream of the broken table, who uses them, which have already refreshed with the data in question, and which is used next.

The brief draws the path the data takes from its sources to the reports, step by step, with each step's schedule and owner, and shows where the row counts changed. Every change, failed or partial run and upstream event you supply is placed against that path and against the time between the last good data and the first bad. Each candidate cause is ranked by three plain tests: is it on the path, did it happen in that window, and is it the kind of change that produces this kind of alert. Changes made after the alert, or downstream of the table, are set aside with the reason, never quietly dropped.

For every candidate the brief says what to compare, who to ask, and what result would confirm it or rule it out. It never names the cause and judges no one's work. The data owner confirms the cause; the data team lead decides who is told and who checks what.

## Who starts the work, and when

A data engineer, an analytics engineer or the data team lead starts it as soon as an agreed data-quality alert fires, or when a report owner says a number looks wrong. The data team lead reads the brief and decides who is told about the affected reports and who checks what. The data owner for the tables concerned confirms the cause and, with the owner of the step concerned, authorizes any fix, rerun or change to the alert.

## What they supply

- **The alert details:** the check that failed, the table it checked, what was expected, what was observed and when it fired.
- **Lineage notes,** one row per hop: where the data comes from, where it goes, the step that moves it, its schedule and its owner.
- **A recent change log:** when each change was made, to what, what kind of change it was, and the ticket.
- **A run log, if you have one:** each step's runs, their status and the rows they wrote.
- **A report users list, if you have one:** each report's owner, who uses it and when it is next used.
- **Notes:** when the data was last known to be good, any upstream event such as a supplier's delayed file, what has already been done, and who owns the data.

Each export has default column headers. If a header does not match, the workflow template stops and asks which column is which rather than guessing.

## What comes out

One brief in a fixed order: the alert and the size of the gap; the affected reports and users, soonest use first, with any report that may also be affected if a candidate is confirmed; the path the data takes, with row counts and gaps in the lineage; candidate causes ranked Strong, Possible or Weak, with those set aside and those off the path; what to check next for each; and the decisions for the data team lead. A section with nothing to report says so.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/), where the team that keeps the data trustworthy needs to know where to look before the next report goes out.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where product, billing and event data pass through many steps before they reach a dashboard.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where order, payment and stock feeds land overnight and the trading team reads the numbers each morning.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/), where shipment and carrier files arrive late or in parts and the operations reports depend on them.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/), when the data platform grows faster than anyone's memory of how it fits together.
- [Acquisitions & integration](https://fullypowered.ai/situations/acquisitions-and-integration/), when new sources join the warehouse and the first alerts arrive before the lineage is well known.

When two reports disagree because they define a metric differently, [metric definition reconciliation](https://fullypowered.ai/workflows/metric-definition-reconciliation/) is the one to use; for a new extract nobody has worked with yet, use the [dataset profile](https://fullypowered.ai/workflows/dataset-profile/); to learn which source system holds a data domain before anything goes wrong, use the [data domain source guide](https://fullypowered.ai/workflows/data-domain-source-guide/). This workflow template is for the moment something that used to be right has gone wrong.

## What has to change for your company

Map your lineage export and change log to the default columns once. Set how far back to look for changes, how large a change in row counts is worth flagging, and how late a run must start to count as late. Match the check types to the ones your monitoring tool uses. Write changed_by as a team or role, not a person. Name the data owner for each important table, so the decisions section can name them, and agree who tells report users and how. It works from files and notes you supply in ChatGPT, Claude, Copilot or Gemini; it needs no connection to your warehouse, pipelines or monitoring tool, and never asks for a login.

## What has been checked

Fully Powered AI wrote this workflow template. It was editorially reviewed on 12 November 2026. It was tried on its invented example on 12 November 2026 in Claude, in two runs. The first found gaps in the instructions, which were then edited; the second is the record published with it, and was made by the assistant that made the edits, so it is not an independent check. Small wording edits were made after that run and have not been run again. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on two or three past incidents your data team has already resolved, with hard cases written in advance: a change made after the alert fired, a change to a model downstream of the alerted table, a lineage with a missing owner, a partial load upstream, a planted line in a change description that tries to give an instruction. The data team lead checks every figure and every ranking against the inputs before anyone relies on the brief. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 12 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 12 November 2026. The record is in [TRIAL.md](TRIAL.md).
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

- [Metric definition reconciliation](../metric-definition-reconciliation/)
- [Source guide for a data domain](../data-domain-source-guide/)
- [Dataset profile](../dataset-profile/)
- [Dashboard brief](../dashboard-brief/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
