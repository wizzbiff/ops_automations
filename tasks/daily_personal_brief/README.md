# Daily Personal Brief

Pulls your email, Slack, Jira, and calendar each morning, keeps only what needs your attention against the personal triage standard, writes a short digest, and sends it to you as a Slack direct message. It exists so you start the day with one read instead of logging into four apps.

## At a glance

* Cadence: weekday mornings
* Requires connectors: Gmail or Microsoft 365 (your choice), Slack, Atlassian, and Google Calendar or Outlook (your choice)
* Reads standards: personal_triage.md, definitions.md, style.md
* Reads config: config/config.md (Jira status mapping) and tasks/daily_personal_brief/config.md (your personal values)
* Writes to: output/daily_personal_brief/

## Run it

1. Authorize the connectors you will use in Cowork: Slack and Atlassian, plus your chosen mail source (Gmail or Microsoft 365) and calendar source (Google Calendar or Outlook).
2. Copy config/config.example.md to config/config.md and fill in the Jira status mapping, if you have not already.
3. Copy this folder's config.example.md to config.md and fill it in: your mail and calendar source, handles, important senders, channels, timezone, and the Slack target for delivery.
4. Run by hand once: paste the body of task.md into a Cowork task and read the result. Check it against the first-run notes below.
5. When the brief looks right, schedule it with `/schedule`.

## Notes

These are best confirmed on the first real run in Cowork, since this repo authors the task but cannot run it:

* Mail and calendar source: confirm the selected connectors are authorized. A connector you did not select is fine to leave unauthorized.
* Jira status mapping: the brief reuses the team report's mapping in config/config.md. If your blocked or stale items look wrong, the mapping is the usual cause.
* Timezone: confirm "today" on the calendar and the lookback window match your day. A wrong `brief_timezone` shifts the brief by a day.
* Volume: if a section runs long, the caps in the template should trim it to the top items plus an overflow count. Tune `important_senders`, `slack_channels`, and `slack_keywords` to cut noise.
* Slack mentions and unread detection depend on the connector's view of your account; verify the Slack section catches what you expect.
* Delivery is a private Slack DM to yourself. The brief is never posted to a channel. Output files under output/ are ignored by git, so the contents are never committed.
