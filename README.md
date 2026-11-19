# AI workflow templates for analysts and reporting teams

FullyPowered Workflow Templates for analytics and reporting teams turn the AI your company already pays for into a team that knows how the work is done: an analyst with a new export profiled before anyone joins it, a manager with a comparison claim checked and plainly worded, a founder with the tracking event plan drafted before launch. 9 workflow templates, made to be customized and deployed. All plain Markdown, all free, MIT license.

We are FullyPowered AI. We build AI workflows for companies, and these are the templates we start from. We publish them because a good starting point should be open to everyone. Copy one. Change it. Make it yours.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** These are templates, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See more examples for analytics and reporting teams](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-readme&from=gh-analytics-readme) · [Have one built for your team](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-readme&from=gh-analytics-readme) Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Who this is for**

- Owners and CEOs who want decisions made on numbers they can trace and trust.
- Data and analytics leads who want their team's method written down and shared.
- The analyst who does the work, gets a careful starting point and still makes the call.

**What these are for**

- **Your best way of doing it, for the whole team.** One piece of work, written down precisely enough that an assistant prepares it the same way every time.
- **Work you can check.** Every template says what it needs, what it produces, what it checked and what it could not.
- **A person decides.** Anything that sends, posts, pays or changes a record waits for someone to approve it.
- **Tied into your business systems.** A workflow can be designed to pull from the systems your company already runs, and even push data back into them, with guardrails and a person approving. [Browse the Connectors Directory](https://fullypowered.ai/connectors/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-readme&from=gh-analytics-readme).
- **Free, open and portable.** MIT-licensed plain instructions that run in the assistant or agent your team already uses: ChatGPT, Claude, Claude Code, Claude Cowork, Codex, Copilot, Gemini, Grok, Perplexity.

**Quick start**

1. **Profile a new data file before you use it.** Take a spreadsheet or export you have received and not yet relied on. Open ChatGPT, Claude, Copilot or Gemini, paste the text below, then add your own file contents and a line about each column. Read the answer before you join or report on anything.

   ```text
   You are preparing a dataset profile for me, an analyst. I will paste one data extract with its header on line 1, one line of notes per column (name, meaning, type, allowed values), the columns that should make a row unique, and what I plan to use the file for. Check that the headers match my notes. Then report, in numbered sections: what one row should be and whether the data bears that out, repeated keys, identical rows, blank or stand-in values, odd formats, spreads and values far from the rest, and any rule I list that a row breaks. Give line numbers for every finding. End with numbered questions for the data owner and a list of decisions that stay with me. Do not change, remove or correct any row. Do not say whether the data is usable. Do not state any conclusion about the business. I decide what to clean and what to exclude. Nothing is sent or changed. [Paste your notes, key, intended use and file contents here.]
   ```

2. Read what comes back. It marks what it checked and what is left for you. What comes back for an invented order file:

   ```text
   DATASET PROFILE: order_lines_oct2026.csv

   For: the analyst. Prepared 10 November 2026 from the settings, schema notes and extract supplied. Intended use: join to the returns table on order_id and sku, to look at returns by channel.

   1. THE FILE
   Header check: the 10 headers match the 10 columns in the schema notes, in the same order. 24 data rows, 10 columns; every row has 10 fields. Full export, as stated; the figures describe the rows supplied.

   2. ROW GRAIN
   Expected: one row per order line, key order_id + line_no. 22 distinct keys among 24 rows. The grain does not hold: 2 keys appear more than once (5004 / 2 on lines 7 and 25; 5006 / 1 on lines 9 and 10).
   Identifier order_id: 18 distinct values.
   Join key order_id + sku: 23 distinct among 24 rows. 1 repeat: 5006 / SKU-205 on lines 9 and 10.
   ```

3. Stop there. You will know if this is for you. When you want it fitted to your company, or built into your agents, [that is what we do](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-readme&from=gh-analytics-readme).

In every workflow a person starts the work, supplies the inputs and decides, and the template only prepares and checks.

These are examples and a starting point, made to be changed to fit how your team works. Work that is not listed here can still be built, as one step or as many.

## The workflow templates here today

- **[Analysis plan](analysis-plan/)**: Before anyone opens the spreadsheet, the owner or manager gets a one-page plan: the question restated, the hypotheses, the fields and periods needed, and the result that would change the decision. It runs no analysis and states no finding. You own the question and the criteria.
- **[Comparison claim check](comparison-claim-check/)**: A manager holding a claim such as "version B converts better" and two groups of numbers gets back the method used, the size of the difference, how uncertain it is, the assumptions checked, and plain wording for what the data does and does not support. The manager decides what to do.
- **[Dashboard brief](dashboard-brief/)**: Before anyone builds the dashboard, the requester gets one brief that settles the work: the decisions it serves, what is shown, each metric's definition, the filters, notes on every source and who refreshes it. The requester approves what is shown and the definitions.
- **[Source guide for a data domain](data-domain-source-guide/)**: When what a domain's tables really mean lives with one analyst, the data lead gets a written source guide from an interview and the table list: what one row is, the keys, the joins, the definitions and the known traps, each marked by where it came from, and the open points as numbered questions.
- **[Data-quality alert trace](data-quality-alert-trace/)**: When a data-quality alert fires or a report looks wrong, the data team lead gets one investigation brief: the reports and people affected, the path the data takes, candidate causes ranked by the evidence supplied, and what to check next. It runs no query and changes nothing.
- **[Dataset profile](dataset-profile/)**: Before anyone joins or relies on a new export, the analyst gets one profile of it: what one row stands for, where keys repeat, what is missing, which values look odd, and a numbered list of questions for the data owner. No data is changed and no verdict is given.
- **[The distribution behind an average](distribution-behind-an-average/)**: Before a service or process review leans on an average, the analyst gets the spread behind it: percentiles from the supplied rows, the extreme cases by line, and how each segment differs. Every figure recomputes from the export, and no cause is stated. The process owner decides what to look into.
- **[Metric definition reconciliation](metric-definition-reconciliation/)**: When two reports give different numbers for one metric, the owner gets a page: the definitions side by side, the gap bridged step by step from supplied records, each cause marked shown or not, and a proposed common measure. The owner chooses.
- **[Tracking event plan](tracking-event-plan/)**: Before analytics goes onto a website or app, the founder or product owner gets one plan: the events and properties worth collecting, when each fires, where it goes, what it is called and who owns it, each tied to a question the business needs answered. The owner approves what is collected.

## How to use one

Open a folder and start with its README. Every folder stands alone, so copy the one you want and leave the rest. The templates are written for ChatGPT, Claude, Copilot and Gemini: paste the instruction block and the output format in as custom instructions, or load the folder in a product that reads `SKILL.md` packages.

To take the whole collection, press **Use this template** at the top of this page: it copies every folder into a repository in your own account, yours to change.

In every template a person starts the work, supplies the inputs and decides. The template prepares and checks. Anything that sends, posts, pays or changes a record waits for a person to approve it.

## What SKILL.md is

Each folder holds a file named `SKILL.md`. It is the technical file: the same instructions and output format as the template, in the packaged form that AI products which load instructions from a folder read. It is generated from `TEMPLATE.md`, so the two always agree. The workflow template is the whole folder; `SKILL.md` is one way of loading it. If your AI product does not read that format, use `TEMPLATE.md`.

## What "checked" means here

Each folder says exactly what was checked and when: who wrote it, that its sources and rights were reviewed, the date of its editorial review, and whether it has been tried on its invented example in a named AI product. Nothing is described as tested for a client unless it was. Test a template on your own past work before your team relies on it; each one comes with acceptance tests for that.

## More workflow templates

The [FullyPowered Workflows Directory](https://fullypowered.ai/workflows/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-readme&from=gh-analytics-readme) lists every workflow template across functions and industries, with search. A machine-readable list of this repository is in [index.json](index.json).

For the work these templates come from, by team and by task, see [AI workflow examples for analytics and reporting teams](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-readme&from=gh-analytics-readme).

## Licence and credits

MIT, in [LICENSE](LICENSE) and in every folder. Each folder's SOURCES.md names what the workflow template drew on. Published by [FullyPowered AI](https://fullypowered.ai/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-readme&from=gh-analytics-readme).
