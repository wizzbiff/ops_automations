# Morning Ticket Report, task

This is the instruction the scheduled task runs. Paste it as the task body when you run by hand, and use the same text when you set up `/schedule`. Paths are written from the repo root so they resolve no matter where this file sits.

---

Run the morning team ticket report.

**Step 1. Load everything.** Read these files in full before doing anything else, and treat them as the source of truth:
* config/config.md, for teams, status mapping, and distribution.
* standards/engineering/definitions.md, for classification, thresholds, escalation, and audience rules.
* standards/shared/style.md, for tone and formatting.
* tasks/engineering/morning_ticket_report/report_template.md, for the output shape.

If config/config.md does not exist, stop and say so. The system is not configured.

**Step 2. Pull from Jira** through the Atlassian connector. For every team in config, query its project and board using the JQL patterns in definitions.md, substituting that team's project key and the status names from the config mapping. Pull active work, issues changed since the previous business day, issues moved to Done since the previous business day, and flagged or waiting issues. If a query returns nothing, record the team as clear rather than dropping it.

**Step 3. Classify** every issue using the rules and thresholds in definitions.md: blocked, at risk, stale, completed yesterday, net new, or needs review. Do not invent a status. Place anything ambiguous under needs review with a one line reason.

**Step 4. Generate** the report using report_template.md exactly, following style.md for tone. Lead with the summary and the escalation list. Apply the escalation rules from definitions.md so the escalation section holds only items that need a leader to act. Stay under the word limit in the template.

**Step 5. Write output.** Save to output/morning_ticket_report/report_YYYY_MM_DD.md using today's date, and overwrite output/morning_ticket_report/latest.md with the same content.

**Step 6. Distribute.** Post the Summary and Needs escalation sections to the `report_slack_channel` from config, with a short pointer to the full report. Send to `direct_recipients` only if config lists any.

**Rules.**
* Only include data from boards and channels the recipients can access.
* If the Atlassian or Slack connector is unavailable, stop. Write a short note to output/morning_ticket_report/latest.md explaining what failed and post nothing.
* Never include per engineer performance framing in leader facing sections.
* If you had to guess at anything material, say so at the top of the report.

---

## Where fixes go

* Wrong things flagged as blocked, or wrong thresholds: fix standards/engineering/definitions.md, so every task and every adopter gets the correction.
* Wrong teams, keys, status names, or recipients: fix your own config/config.md.
* Wrong shape or length: fix this folder's report_template.md.
* Wrong tone across all reports: fix standards/shared/style.md.
