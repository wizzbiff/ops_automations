# Daily Personal Brief, task

This is the instruction the scheduled task runs. Paste it as the task body when you run by hand, and use the same text when you set up `/schedule`. Paths are written from the repo root so they resolve no matter where this file sits. Unlike the morning ticket report, this is a private digest to yourself, not a team report.

---

Run the daily personal brief.

**Step 1. Load everything.** Read these files in full before doing anything else, and treat them as the source of truth:
* config/config.md, for the Jira status mapping. Personal triage reuses the same buckets the team report uses.
* tasks/engineering/daily_personal_brief/config.md, for your personal values: mail and calendar source, your handles, important senders, Slack scopes, the brief timezone, and the Slack target the brief is delivered to.
* standards/engineering/personal_triage.md, for what counts as needing your attention, the dedup rules, the ranking, and the item caps.
* standards/engineering/definitions.md, for the Blocked, At risk, and Stale classification and thresholds the Jira section reuses.
* standards/shared/style.md, for tone and formatting.
* tasks/engineering/daily_personal_brief/brief_template.md, for the output shape.

If either config/config.md or tasks/engineering/daily_personal_brief/config.md does not exist, stop and say so. The system is not configured. If `mail_source` or `calendar_source` is unset or not a recognized value, treat it as missing required config and stop.

**Step 2. Gather.** Pull from each source for the window in personal_triage.md, computing "today" and the lookback in the `brief_timezone` from config:
* Mail: branch on `mail_source`. If `gmail`, read unread and recent threads through the Gmail connector. If `m365`, read them through the Microsoft 365 connector. Use only the selected connector.
* Slack: read your direct messages, @-mentions, and the configured channels through the Slack connector.
* Jira: query issues assigned to you through the Atlassian connector, using the assignee-scoped JQL in personal_triage.md with the status names from the config mapping.
* Calendar: branch on `calendar_source`. If `google`, read today's events through the Google Calendar connector. If `m365`, read them through the Microsoft 365 connector. Use only the selected connector and the calendars named in config.

**Step 3. Process.** Apply personal_triage.md to decide what surfaces from each source, and definitions.md for the Jira classification scoped to issues assigned to you. Dedup across sources using the precedence in personal_triage.md, preferring the native item over a notification email. Rank the few most important things for "Start here", and trim each section to its cap with an overflow count.

**Step 4. Generate** the brief using brief_template.md exactly, following style.md for tone. Lead with "Start here", then today's calendar, then the email, Slack, and Jira queues. Put any data-incompleteness or guess flag at the very top. Stay within the caps in the template.

**Step 5. Write output.** Save to output/daily_personal_brief/brief_YYYY_MM_DD.md using today's date in the brief timezone, and overwrite output/daily_personal_brief/latest.md with the same content.

**Step 6. Distribute.** Send the brief as a Slack direct message to yourself, to the `slack_dm_target` from config. This is a private digest: do not post it to a channel and do not copy anyone else.

**Rules.**
* This brief contains only what your own connected accounts can already see. Never widen distribution: no channel post, no cc, no forward.
* If a required connector is unavailable, stop, write a short note to output/daily_personal_brief/latest.md explaining what failed, and distribute nothing. The required connectors are Slack, Atlassian, and the selected mail and calendar connectors only. An unauthorized connector you did not select (for example M365 mail when `mail_source` is `gmail`) is not a failure.
* The Microsoft 365 connector is read only. On any M365 branch, never attempt to send mail.
* If you had to guess at anything material, say so at the top of the brief.

---

## Where fixes go

* Wrong things surfaced as needing attention, wrong dedup, ranking, or caps: fix standards/engineering/personal_triage.md, so every personal brief gets the correction.
* Wrong Jira thresholds for blocked, at risk, or stale: fix standards/engineering/definitions.md, so the team report and this brief stay aligned.
* Wrong mail or calendar source, handles, important senders, channels, timezone, or delivery target: fix your own tasks/engineering/daily_personal_brief/config.md.
* Wrong Jira status names: fix your own config/config.md.
* Wrong shape or length: fix this folder's brief_template.md.
* Wrong tone across all reports: fix standards/shared/style.md.
