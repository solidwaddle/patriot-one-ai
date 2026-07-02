# Capabilities

What Patriot One AI can do today, with example prompts. The bot is @-mentioned in a Slack channel and answers in-thread.

## Ask the data (natural-language → read-only SQL)

Ask operational questions in plain English; the bot writes and runs a read-only query against the Salesforce mirror and answers with the result.

- *"What's our quoted margin MTD?"*
- *"Top 3 lanes for [customer] this quarter."*
- *"Which active reps are up month-over-month on GP?"*
- *"How many loads booked last week vs the week before?"*

The bot knows the curated analytics tables, the status lifecycle, dedup rules, and which fields are stored as text vs numeric — so it targets the right tables and avoids common pitfalls.

## Analyze & summarize

Beyond raw lookups, it computes and explains:

- Margin / gross-profit roll-ups by rep, account, or lane
- Lane and customer performance trends
- Billing velocity and operational throughput
- Comparisons across time windows

## Read files & attachments

Attach a file to your mention and the bot reads it natively:

- **PDFs** — rate sheets, contracts, statements (layout and tables preserved)
- **Images / screenshots** — read directly
- **Documents & transcripts** — `.docx`, `.txt`, meeting-tool exports
- Cross-reference an attached doc against live data in the same request

Example: drop a meeting transcript and ask for an outline; attach a rate sheet PDF and ask how it compares to recent lane averages.

## Export to CSV

When you want the underlying rows, ask for an export:

- *"Give me a CSV of all loads for [customer] this month."*
- *"Export that table as a downloadable file."*

The bot turns the query result into a CSV and returns a working download link.

## Knowledge base

- Searches the company intranet's SOPs and policies for procedures and structure.
- Reads live operational records (requests, initiatives, training, and other allow-listed tables) through a secured read-only API.

## Learn permanently

Teach it a durable rule and it applies it from then on, no redeploy:

- *"remember: 'done' and 'completed' mean the same for tech requests."*
- *"remember: [customer] is always billed net-30."*

## Continual improvement — capture & analysis *(next phase)*

> Planned. Implements the QP-160-1 Continual Improvement Procedure. Full design in **[CONTINUAL-IMPROVEMENT.md](CONTINUAL-IMPROVEMENT.md)**.

Submit an observation in plain language and the bot captures it, asks the right follow-ups, and analyzes it for the monthly leadership review:

- *"@Patriot One I keep seeing carrier fallout on our reefer lanes in the last few weeks."*
- *"remember this as an observation: billing handoffs are slipping when the POD comes in late."*

The bot will guide the submission, assign an Observation ID (`JUNE-001`), suggest a classification and affected Quality Objectives, surface similar past observations, and flag potential trends — then generate a monthly trend report ahead of the first-Thursday review. Observations are stored in Salesforce (`Observation__c`, alongside the Corrective Action Program), and the whole lifecycle — submit, edit, review — stays in Slack. All suggestions are decision support; leadership validates, prioritizes, and decides.

## Safety guarantees

- Read-only to source systems: only `SELECT`/`WITH` queries run against them; everything else is rejected.
- Row and time caps on every query.
- No path to modify existing Salesforce data, the intranet, or any source system. The one controlled write — Continual Improvement observations — goes through a scoped connected app limited to the `Observation__c` object, and nothing else.
- Sensitive tables are excluded from the live-records API.

---

*This list grows as data sources are added. See the roadmap in the [README](../README.md).*
