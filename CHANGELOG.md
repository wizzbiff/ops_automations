# Changelog

Versioned history of the standards. Config changes by individuals are not tracked here. Only changes to `standards/` (shared or per domain) and to the repo structure belong in this file, because those affect everyone.

## 1.1.0

Added the daily personal brief, the second engineering task.

* standards/engineering/personal_triage.md: new standard defining what counts as needing your attention across email, Slack, Jira, and calendar, plus dedup precedence, deterministic "Start here" ranking, and per-section item caps. Reuses the Blocked, At risk, and Stale thresholds from definitions.md by pointer rather than restating them.
* tasks/daily_personal_brief: personal morning digest of email, Slack, Jira, and calendar, delivered as a Slack DM to self. Mail source (Gmail or Microsoft 365) and calendar source (Google Calendar or Outlook) are config-selectable.
* config/connectors.md: added Gmail, Microsoft 365, and Google Calendar rows for the new task.

## 1.0.0

Initial release.

* Structure: standards split into a shared house layer (standards/shared/) and per domain standards (standards/engineering/), so additional domains such as executive ops can be added without disturbing existing ones.
* standards/engineering/definitions.md: blocked, at risk, stale, completed yesterday, net new, needs review. Thresholds set: at risk window 2 business days, stale 3 business days, escalation age 2 business days, escalation date window 3 days.
* standards/shared/style.md: shared tone and formatting rules.
* tasks/morning_ticket_report: first task. Morning report of ticket health by team, posted to Slack.
* config: shared adopter config for teams, status mapping, and distribution. connectors reference.
* _task_template: copyable shape for new tasks.
