# Tracking event plan

Before analytics goes onto a website or app, the founder or product owner gets one plan: the events and properties worth collecting, when each fires, where it goes, what it is called and who owns it, each tied to a question the business needs answered. The owner approves what is collected.

*Workflow template · Analytics and reporting · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflow templates/tracking-event-plan/)*

## The outcome

You start measuring with a plan instead of a guess. Before anyone adds a line of tracking, you hold a short list of the things the site or app should record, and next to each one the question it will help you answer. If nothing you want to know needs a thing, it is not on the list.

Each event comes with a plain statement of the moment it fires and the moments that do not count, so a developer cannot reasonably read it two ways. Each carries only the details your questions need, a name that follows one rule, the places the data goes and the person who owns what it means.

The plan is honest about its edges. A question the plan cannot answer, because the answer lives somewhere else, is listed with what is missing. A detail that would identify a person, or that sits on your own never-collect list, is held for you and never slipped in. You decide what is collected. The plan writes no tracking code and gives no advice about privacy rules or consent notices.

## Who starts the work, and when

The founder, product owner or marketing lead starts it before a website or app is instrumented, when a new feature or step needs measuring, or when an old tracking setup has grown names nobody trusts. That person brings the questions and the description of the journey, and reviews the result with whoever will build it.

The owner approves what is collected. The person who builds it confirms the plan can be built as written.

## What they supply

- **The questions** the business wants answered, in its own words, each with the decision it will inform.
- **The journey:** the steps a visitor or user takes, where each happens and what the site or app does in response.
- **The events already collected,** if any, with a name, a description and a destination each.
- **The destinations:** the tools the data goes to, what each is for and who owns it.
- **The settings:** who approves, who owns meaning, who builds, a naming rule if the business has one, and anything that must never be collected.

## What comes out

One dated plan, in a fixed order: each question with the measure that answers it, or the reason it cannot be answered yet; each event with when it fires, when it does not, its properties, its destinations, its owner and how to check it once built; existing events that were not reused and why; fields held for the owner and fields on the journey that are not collected; and a numbered list of decisions for the owner. Nothing is built, switched on or sent.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Analytics and reporting](https://fullypowered.ai/functions/analytics-and-reporting/), where measurement definitions are written down before they are built.
- [Product management](https://fullypowered.ai/functions/product-management/), where a new feature needs a way to tell whether it worked.
- [Software and technology](https://fullypowered.ai/industries/software-technology/), where a product team adds events to every release.
- [Ecommerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where the path from product page to order is the thing to measure.
- [Professional services](https://fullypowered.ai/industries/professional-services/), where a firm's website exists to bring in enquiries.
- [Startups & new ventures](https://fullypowered.ai/situations/startups-and-new-ventures/), where the first analytics set-up shapes every report that follows.
- [New business lines](https://fullypowered.ai/situations/new-business-lines/), where a new offer needs its own measures from day one.

It is a different piece of work from [website findability audit](https://fullypowered.ai/workflows/website-findability-audit/), which looks at whether search engines can reach and read your pages, and from [lead magnet plan](https://fullypowered.ai/workflows/lead-magnet-plan/), which plans a free resource. Here the website or app already exists or is about to, and the question is what it should record.

## What has to change for your company

Write your own questions and the decision behind each; the plan is only as sharp as they are. Set your naming rule once and keep it. List the destinations you actually use and who owns each. Decide what must never be collected and put it in the settings, so it is held every time. Agree who approves and who builds. Give the plan to the person who will build the events, and have them confirm each trigger before work starts.

## What has been checked

Fully Powered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was tried on its invented example by Claude on 10 November 2026 (the second recorded run, which replaced a first); the record is in the trial. It has not yet been tested in a client environment, or as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a journey you know well, with cases written in advance: a question with no decision, an existing event whose name is close to a new one, a question that needs a personal detail. The owner and the builder read every trigger before anything is built.

- Written by Fully Powered AI.
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

- [Website findability audit](https://fullypowered.ai/workflow templates/website-findability-audit/)
- [Lead magnet plan](https://fullypowered.ai/workflow templates/lead-magnet-plan/)
- [Creator campaign performance report](https://fullypowered.ai/workflow templates/creator-campaign-performance-report/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
