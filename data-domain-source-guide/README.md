# Source guide for a data domain

Turn one analyst's knowledge of a data domain into a guide: grain, keys, joins, definitions and traps, each marked by its source, every gap a question.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See Source guide for a data domain on our website](https://fullypowered.ai/workflows/data-domain-source-guide/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide) Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the invented ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/data-domain-source-guide/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide)*

## The outcome

The knowledge that lives in one analyst's head becomes a page the whole team can work from. For each table in the domain, the guide says what one row stands for, which columns make it unique, which date to use and in which time zone, whether rows change after they load, which rows are normally left out, and who owns it. It says how the tables join and in what proportion, so nobody sums a total after a join that repeats it. It records the business definitions built on the tables and the traps the analyst has learned the hard way.

Every line carries a mark: from the table list, said in the interview, said with doubt, or shown by a count the analyst ran. No meaning is guessed from a column name. Where a count disagrees with what was said, both stand side by side as a conflict. Every unanswered field, doubt, conflict and unstated join proportion becomes a numbered question addressed to the person or team who can answer it, so the next conversation starts from a list. A trap whose remedy nobody stated says so, for the domain analyst to complete.

The domain analyst verifies the guide and names owners for what is still open. The data lead approves it before anyone relies on it.

## Who starts the work, and when

The analytics lead or data lead starts it when a data domain is relied on by many people and understood well by one: before that analyst moves on or goes on leave, when new analysts join, or when a team inherits a warehouse after a reorganisation or an acquisition. The lead interviews the domain analyst, using the interview sheet the workflow template prepares from the table list, then runs it again with the notes. The domain analyst reads every line before the guide is shared, and each table's owner answers the questions about their table.

## What they supply

- **A short scope note:** the domain, who the guide is for, the analyst interviewed and the lead who approves.
- **The table list:** one row per column, with the table, the column, its type and any note, exported or copied from your own catalogue or warehouse listing.
- **The interview notes,** typed during the conversation with the domain analyst, statement by statement under each table.
- **Optional counts the analyst ran:** rows, distinct values, and rows that find no match in another table, pasted in with the date they were run.

It connects to no database or catalogue and never asks for a login. Anyone who wants a statement confirmed runs the count with their own access and pastes in the result.

## What comes out

One guide in a fixed order: the scope, then each table with its six standard answers, the columns with and without a recorded meaning, and the personal data columns named but never shown; the joins with their proportions and conditions; the definitions; the known traps, each with what the analyst said to do instead; the conflicts between what was said and what a count showed; the numbered open questions, each for a named role or team; and the counts to run next to confirm the joins. A section with nothing in it says so. Without interview notes it returns the interview sheet instead and drafts nothing.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide), where the joins and definitions the best analyst knows by heart should be written down beside the tables.
- [Software and technology](https://fullypowered.ai/industries/software-technology/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide), where product, billing and usage tables are added faster than anyone documents them.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide), where orders, lines, refunds and customers are joined every day and one repeated total skews a report.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide), where shipment, stop and invoice tables each count something slightly different.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide), where one long-serving analyst has become the only map of the warehouse.
- [Acquisitions and integration](https://fullypowered.ai/situations/acquisitions-and-integration/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide), when another company's tables arrive and the people who built them are leaving.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide), when new analysts join faster than the old ones can explain the data.

For the contents of a single new extract, [dataset profile](https://fullypowered.ai/workflows/dataset-profile/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide) is the one to use. When two reports disagree about one metric, use [metric definition reconciliation](https://fullypowered.ai/workflows/metric-definition-reconciliation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide). This workflow template is for the tables a team keeps coming back to.

## What has to change for your company

Set the columns of your table list to match what your catalogue or warehouse exports, and the counts your analysts are willing to run and paste back. Decide how many tables one guide may cover; the default is 25. Add to the six standard questions if your team always needs another, such as how late data arrives. Name the domain analyst and the owner of each table, so every question has someone to answer it. Agree who approves a guide, where guides are kept, and when one is run again: after the analyst moves on, after a schema change, or once a year. It works from files and notes you supply in ChatGPT, Claude, Copilot or Gemini.

## What has been checked

FullyPowered AI wrote this workflow template. It was editorially reviewed on 12 November 2026. It was tried on its invented example in Claude on 12 November 2026; the record is published with it. The first run found that the instructions did not say when a relationship the analyst describes counts as a join, or how a column the analyst did not name is written; the template and the example were then changed, and the edited version was run once more on the example by the assistant that made the edits, not independently. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a domain your senior analyst already knows well, with cases written in advance: a key whose count does not hold, a column nobody can explain, a statement made with doubt, a login detail left in the notes. The domain analyst checks every line against the notes before anyone relies on the guide. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide) describes the record we keep.

- Written by FullyPowered AI.
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

- [Dataset profile](../dataset-profile/)
- [Metric definition reconciliation](../metric-definition-reconciliation/)
- [Departing-employee knowledge capture](https://fullypowered.ai/workflows/departing-employee-knowledge-capture/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-data-domain-source-guide&from=gh-analytics-data-domain-source-guide).
