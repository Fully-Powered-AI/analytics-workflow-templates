# The distribution behind an average

See the spread behind an average: percentiles from your export, extreme cases by line and segment differences, with every figure checkable.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** This is a template, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See The distribution behind an average on our website](https://fullypowered.ai/workflows/distribution-behind-an-average/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Quick start**

1. Read EXAMPLE.md to see what a good result looks like.
2. Copy all of TEMPLATE.md into your assistant, then give it your own inputs, or the sample ones from EXAMPLE.md.
3. Read what comes back. It marks what it checked and what is left for you.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/distribution-behind-an-average/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average)*

## The outcome

An average of 21 hours can describe a desk where most work closes in half a day and a handful of cases run for most of a week. This workflow template shows which of those the review is looking at. The analyst gets one page: the middle of the range and the upper end of it, how much of the total the largest records carry, how many records sit over the target, which records are the extreme cases and on which lines of the export they sit, and how each segment's spread differs from the whole.

Every figure is worked out by one stated method from the rows supplied, so anyone holding the export can check it with a sorted column and a calculator. Rows that could not be counted are listed with the reason. Odd records, such as a zero or a record that appears twice, are listed for checking and kept in every figure as supplied. It removes or corrects no row. The extreme cases are kept too, because a valid extreme is evidence, not an error.

The page states what the numbers are and never why. The analytics owner confirms the figures and the method; the process owner decides which cases or segments, if any, to follow up.

## Who starts the work, and when

An analyst, or an operations lead who owns a service or process measure, starts it when a review is about to rest on an average: a monthly service review, a target being set or questioned, a complaint that "it always takes too long", or a new team or site whose numbers look different. The measure is a duration or an amount per record, such as hours to resolve a ticket, days from order to delivery or days to turn a request around. The view looks at the high end only: an extreme case is an unusually large value.

## What they supply

- **The export,** one row per record, as a CSV or a pasted table. The default column headers are `record_id`, `segment`, `recorded_on` (a date, YYYY-MM-DD) and `measure` (a number). If your export uses other names, say which column is which; if a header does not match and no mapping is given, the work stops and asks.
- **The measure and its unit,** such as "hours to resolve, in hours".
- **The population,** in a sentence: which records the export is meant to hold.
- **The observation window,** a first and last date. Rows dated outside it are not counted and are listed.
- **Optional settings:** a target to count against, a different cut for extreme cases, the smallest segment worth its own percentiles, segments to report together, and who the analytics owner and process owner are.

## What comes out

One page in a fixed order: the header check and the rows counted and not counted; the whole population's mean, minimum, percentiles from P25 to P95 and maximum, with a few lines on what the average leaves out; the same figures for each segment; the differences between each segment and the whole; the extreme cases, largest first, each with its line number; records to check; numbered points for the analytics owner to confirm; numbered choices for the process owner; and what the page does not show. A section with nothing to report says what was checked and that none was found.

See the worked example in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), where a distribution is the honest companion to any average that goes into a review.
- [Operations and process improvement](https://fullypowered.ai/functions/operations-and-process-improvement/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), where the slowest tenth of the work is often what customers remember.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), where delivery and dwell times have long upper tails that an average smooths away.
- [Software and technology](https://fullypowered.ai/industries/software-technology/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), where support resolution times differ sharply by queue and product.
- [Ecommerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), where order-to-dispatch and refund times are reviewed against a promise to the customer.
- [Professional services](https://fullypowered.ai/industries/professional-services/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), where turnaround on requests and deliverables varies by team and client.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), when volume rises and the upper end of the range moves before the average does.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average), when a long-standing service target needs to be checked against how the work really spreads.

To profile a new export before relying on it, start with [dataset profile](https://fullypowered.ai/workflows/dataset-profile/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average). To test whether a difference between two groups holds up, use [comparison claim check](https://fullypowered.ai/workflows/comparison-claim-check/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average). This workflow template describes a spread; it runs no test.

## What has to change for your company

Write down once how your exports name the four columns, so the mapping travels with the measure. Set the target your service is reviewed against, the cut you treat as extreme, and the smallest segment you will read percentiles for. Agree with whoever builds your reports that percentiles here use the nearest-rank method, so nobody is surprised when a spreadsheet function that interpolates gives a slightly different figure. Name the analytics owner who confirms the figures and the process owner who decides follow-up. It runs in ChatGPT, Claude, Copilot or Gemini from an export or pasted rows you supply; it needs no connection to your systems, and it never asks for a login.

## What has been checked

FullyPowered AI wrote this workflow template from its own published map of analytics work. It was editorially reviewed on 11 November 2026. It was tried on its example in Claude on 11 November 2026, on the instructions as they stood that day; the record of that run is published with the template, and later edits have not been run again. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on two or three past months whose spread your analyst already knows, with cases written in advance: a header that does not match, a row outside the window, a blank measure, a zero, a record that appears twice, a segment too small for its own percentiles. The analyst recomputes every figure from the sorted export before anyone relies on the page. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average) describes the record we keep.

- Written by FullyPowered AI.
- Sources and rights reviewed.
- Editorially reviewed on 11 November 2026.
- Package format checked by script on every release.
- Tried once on its example in Claude on 11 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete workflow template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example.
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
- [Comparison claim check](../comparison-claim-check/)
- [Operations KPI scorecard](https://fullypowered.ai/workflows/operations-kpi-scorecard/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average)

## Make it yours

This workflow template is an example and a starting point. FullyPowered AI adapts it to how your company works, proves it on real work and rolls it out to the roles that use it. We can also build any other workflow for your company, including one that runs several steps, in a Workflow Sprint or a scoped implementation. [Talk with us](https://fullypowered.ai/contact/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=analytics-distribution-behind-an-average&from=gh-distribution-behind-an-average).
