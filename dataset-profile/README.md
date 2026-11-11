# Dataset profile

Before anyone joins or relies on a new export, the analyst gets one profile of it: what one row stands for, where keys repeat, what is missing, which values look odd, and a numbered list of questions for the data owner. No data is changed and no verdict is given.

*Capability template · Analytics and reporting · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/dataset-profile/)*

## The outcome

An unfamiliar table stops being a surprise. Before the first join, the analyst has a page that says what a row is meant to be and whether the data bears that out, which keys appear more than once and in what way the repeats differ, which columns hold blanks or stand-in text, which values sit far from the rest, and where two columns disagree with each other. Every finding points to the line in the file where it can be seen.

Each finding that needs an answer from someone else becomes a question addressed to the data owner, with the lines beside it, so the conversation with the source team starts with facts. The profile also notes which findings touch the use the analyst has in mind, and lists the decisions that remain open.

The analyst decides what to clean, what to exclude and whether the data is usable. The profile changes no row, removes none and states no business conclusion.

## Who starts the work, and when

An analyst starts it when a new extract arrives, or before relying on a table inherited from someone else, for example a file received during a handover, an acquisition or an investor data request. It is also worth running when a familiar export changes shape. The analyst supplies the file and what it is for, and reads the result before anything is joined, loaded or reported on.

## What they supply

- **The extract itself,** as a CSV or a pasted table. If it is a sample, say so.
- **Schema notes,** one line per column: its name, what it means, its type and any allowed values. A column's absence from the notes is itself a finding.
- **The expected key,** the columns that should make a row unique, and the join key if it differs.
- **The intended use,** in a sentence, so the profile can say which findings touch it.
- **Optional settings:** the period the dates should fall in, the far-out rule, columns that hold personal data, and who owns the data.

## What comes out

One profile in a fixed order: the file and its header check, row grain, duplicates, missing and stand-in values, types and formats, value spreads, consistency rules, what the findings touch for the intended use, questions for the data owner, decisions for the analyst, and what was not checked. A section with nothing to report says what was checked and found nothing.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/), where the first hour with a new table decides how much of the later work can be trusted.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where product and billing exports change shape between releases.
- [Finance and investment](https://fullypowered.ai/industries/finance-and-investment/), where portfolio and transaction extracts arrive from several sources with different habits.
- [Ecommerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where order, product and returns tables are joined constantly.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where time, billing and project exports are joined for utilization and margin questions.
- [Acquisitions and integration](https://fullypowered.ai/situations/acquisitions-and-integration/), when the other company's data arrives with no one left who built it.
- [Private equity and portfolios](https://fullypowered.ai/situations/private-equity-and-portfolios/), when a portfolio company's extracts must be understood quickly before they are compared.

Before a finished workbook is sent out, [spreadsheet check before sharing](https://fullypowered.ai/capabilities/spreadsheet-check-before-sharing/) is the one to use. This capability is for a table you are about to start working with.

## What has to change for your company

Write your schema notes once per source and keep them: the profile is only as good as the meaning you give each column. Set the far-out rule that suits your data, the stand-in values your systems use for "unknown", and the period you expect. Name the columns that hold personal data so the profile reports counts for them and shows no values. Name the data owner for each source, so every question has an addressee. Decide where profiles are filed. It runs in ChatGPT, Claude, Copilot or Gemini, from a file or pasted rows you supply; it needs no connection to your database, and it never asks for a login.

## What has been checked

Fully Powered AI wrote this capability template. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026; the record is published with it. The first run found that the example tested a date order the instructions did not call for; the template and the example were then changed, and the edited version was run once more on the example by the assistant that made the edits, not independently. That run covered one export with a repeated key, a second date format, a stand-in word and a rule the analyst listed; it did not reach a header that does not match the notes, a column marked as personal data, or a request to clean the file. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on two or three extracts your analysts already know well, with faults planted in copies and written down in advance: a repeated key whose rows differ, a date in a second format, a stand-in word in a numeric column, a column missing from the notes. The analyst confirms each finding against the file before anyone relies on the profile. [Pilot acceptance-test preparation](https://fullypowered.ai/capabilities/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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
- [Supplier spend analysis](https://fullypowered.ai/capabilities/supplier-spend-analysis/)
- [Budget-versus-actual variance commentary](https://fullypowered.ai/capabilities/budget-versus-actual-variance-commentary/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
