# Connectors

The connectors this repo's tasks rely on, what access each needs, and which tasks use them. Connect them once in Cowork settings. Claude only ever sees what the connected account can already see.

| Connector | Access | Used by | Notes |
|-----------|--------|---------|-------|
| Atlassian (Jira) | read | morning_ticket_report, daily_personal_brief | queries tickets, reads links and flags |
| Slack | read and write | morning_ticket_report, daily_personal_brief | posts the report to a channel, sends the brief as a DM to self |
| Gmail | read | daily_personal_brief | reads mail when mail_source is gmail |
| Microsoft 365 | read | daily_personal_brief | reads Outlook mail and calendar when mail_source or calendar_source is m365 |
| Google Calendar | read | daily_personal_brief | reads today's events when calendar_source is google |
| Atlassian (Confluence) | read | future: ticket_research | pulls linked docs for context |
| GitHub | read | future: ticket_research | pulls linked pull requests and code context |

When you add a task, add its connectors here so adopters know what to authorize before running it.

## Authorization notes

* Org owner or admin enablement may be required before these connectors appear for individuals, depending on your workspace policy.
* The Microsoft 365 connector is read only. It can read Outlook, Teams, SharePoint, and OneDrive, but cannot send mail. Distribution that needs to reach inboxes should go through Slack or be forwarded by a person.
