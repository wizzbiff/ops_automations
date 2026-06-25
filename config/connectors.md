# Connectors

The connectors this repo's tasks rely on, what access each needs, and which tasks use them. Connect them once in Cowork settings. Claude only ever sees what the connected account can already see.

| Connector | Access | Used by | Notes |
|-----------|--------|---------|-------|
| Atlassian (Jira) | read and write | morning_ticket_report | queries tickets, reads links and flags |
| Slack | read and write | morning_ticket_report | posts the report to a channel |
| Atlassian (Confluence) | read | future: ticket_research | pulls linked docs for context |
| GitHub | read | future: ticket_research | pulls linked pull requests and code context |

When you add a task, add its connectors here so adopters know what to authorize before running it.

## Authorization notes

* Org owner or admin enablement may be required before these connectors appear for individuals, depending on your workspace policy.
* The Microsoft 365 connector is read only. It can read Outlook, Teams, SharePoint, and OneDrive, but cannot send mail. Distribution that needs to reach inboxes should go through Slack or be forwarded by a person.
