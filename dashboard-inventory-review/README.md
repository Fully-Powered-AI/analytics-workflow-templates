# Dashboard and report inventory review

Before a licence renewal, review every dashboard and report from your tool's export: unused items, missing owners, duplicates and unopened scheduled sends.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See Dashboard and report inventory review on our website](https://fullypowered.ai/workflows/dashboard-inventory-review/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the invented ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/dashboard-inventory-review/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review)*

## The outcome

Reporting tools fill up quietly. A dashboard is copied for one meeting and never deleted, a report keeps emailing a team that has moved on, and the person who built half the finance folder left last spring. This workflow template turns the tool's own inventory into one review the analytics lead can act on.

Every item is read and counted, and the count line proves it. The review lists what has gone unviewed past your limit, what belongs to someone who has left or to nobody, which items look like copies of each other on the same data source, which scheduled sends nobody opens in the tool, and what sits on a data source you are switching off. Each line carries the item id and the counts from the export, so anyone can check it in a minute.

It ends with a proposed list of questions, grouped by dashboard owner, plus the items with no owner to ask. The analytics lead decides what is retired, kept or merged once the owners answer. Views and viewers stay counts per item: nobody is named or ranked by how much they use the tool.

## Who starts the work, and when

The analytics lead, or the person who administers the company's reporting tool, runs it twice a year. It is worth running before the tool's licence renews, before a move to another tool, and after two companies' reporting is brought into one place. The analytics lead, or whoever your rules name, reviews the draft and decides; each dashboard owner answers for their own items.

## What they supply

- **The dashboard and usage export from your business intelligence tool**: one row per dashboard or report, with the headers `item_id`, `name`, `type` (dashboard or report), `folder`, `owner`, `created_at`, `last_edited_at`, `last_viewed_at`, `views_90d`, `distinct_viewers_90d`, `data_source` and `scheduled` (yes or no). If a header is missing or named differently, the review stops and asks which column is which.
- **Your team's rules:** how long without a view counts as unused (90 days unless you say otherwise), which folders are exempt, such as items kept for audit, who decides retirement, and any data source marked for retirement, with its date.
- **A leavers list,** if you have one, with names written as they appear in the owner column.
- **Today's date,** so every day count can be checked.

## What comes out

One review in a fixed order. A count line comes first: items read, items flagged, items held back for an export question, and items with nothing to report, adding up to the rows in the export. Then six short sections: unused past the limit, owner left or blank, likely duplicates by name and data source, scheduled sends with no views in the tool, items on a retiring data source, and rows where the export disagrees with itself. An empty section says "None."

Last comes the proposed list to ask owners about: each flagged item once, under its owner, with every reason and a plain question for each. Items whose owner has left or is blank go to the person who decides, who names a new owner first.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review), which looks after the reporting tool and answers for what is in it.
- [Software and technology](https://fullypowered.ai/industries/software-technology/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review), where product, sales and finance each build dashboards and the tool's seat count grows with them.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review), where trading, stock and campaign reports multiply around every season and promotion.
- [Finance and investment](https://fullypowered.ai/industries/finance-and-investment/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review), where reports kept for audit must be told apart from reports nobody needs any more.
- [Professional services](https://fullypowered.ai/industries/professional-services/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review), where each client team builds its own utilization and billing views of the same data.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review), where years of reports have piled up and their builders have moved on.
- [Acquisitions & integration](https://fullypowered.ai/situations/acquisitions-and-integration/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review), when two companies' reporting lands in one tool and the same report exists twice.

## What has to change for your company

Set how long without a view counts as unused, and name the folders that are exempt. Decide who decides retirement, and who with administrator rights carries a decision out. Check your tool's export against the twelve headers once and keep the mapping with your rules. Agree how owners are asked and by when they answer. The review reads the inventory only: it never opens the data inside a dashboard and does not judge whether a metric is right, which is what [metric definition reconciliation](https://fullypowered.ai/workflows/metric-definition-reconciliation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review) is for. It runs in ChatGPT, Claude, Copilot or Gemini from the files you supply, and needs no connection to your reporting tool.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 19 November 2026. It was tried once on its invented example on 19 November 2026, and the run was not blind. It has not yet been tested in a client environment, or tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on last year's export, which your reporting administrator already knows, with hard cases written in advance: a header named differently, a report in an exempt folder, a dashboard created last month and never opened, an owner on the leavers list, two copies of one report. The administrator checks every line against the tool before any owner is asked. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review) sets those cases up.

- Written by FullyPowered AI.
- Sources and rights reviewed.
- Editorially reviewed on 19 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 19 November 2026. The record is in [TRIAL.md](TRIAL.md).
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
- [Dashboard brief](../dashboard-brief/)
- [Software subscription and vendor spend review](https://fullypowered.ai/workflows/software-subscription-and-vendor-spend-review/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-dashboard-inventory-review&from=gh-analytics-dashboard-inventory-review).
