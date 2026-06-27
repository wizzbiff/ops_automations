# Connectors

The connectors this repo's tasks rely on, what access each needs, and which tasks use them. Connect them once in Cowork settings. Claude only ever sees what the connected account can already see.

| Connector | Access | Used by | Notes |
|-----------|--------|---------|-------|
| Atlassian (Jira) | read and write | morning_ticket_report, daily_personal_brief, ticket_research, weekly_leadership_rollup, board_metrics | queries tickets, reads links, flags, and status history; reads OKR objectives and key results for board_metrics; write used only by ticket_research, to post one research brief comment on the input ticket |
| Slack | read and write | morning_ticket_report, daily_personal_brief, ticket_research, weekly_leadership_rollup, board_metrics | posts the report to a channel, sends the brief as a DM to self; ticket_research reads threads only |
| Gmail | read | daily_personal_brief | reads mail when mail_source is gmail |
| Microsoft 365 | read | daily_personal_brief | reads Outlook mail and calendar when mail_source or calendar_source is m365 |
| Google Calendar | read | daily_personal_brief | reads today's events when calendar_source is google |
| Atlassian (Confluence) | read | ticket_research | pulls linked docs for context |
| GitHub | read | ticket_research | pulls linked pull requests and code context |
| Looker | read | board_metrics | runs the configured looks for growth and product metrics |
| NetSuite | read | board_metrics | pulls the configured financial report for the closed month |

When you add a task, add its connectors here so adopters know what to authorize before running it.

## Authorization notes

* Org owner or admin enablement may be required before these connectors appear for individuals, depending on your workspace policy.
* The Microsoft 365 connector is read only. It can read Outlook, Teams, SharePoint, and OneDrive, but cannot send mail. Distribution that needs to reach inboxes should go through Slack or be forwarded by a person.
* The Atlassian write scope is exercised only by ticket_research, only as a comment on the ticket you research. Every other task reads from Atlassian and never writes.
* Looker and NetSuite are not part of the default connector set the engineering tasks use. They are required only by board_metrics and must be added in Cowork before that task runs; depending on your workspace they may need a custom or MCP-based connector. Both are read only here: board_metrics never writes to a BI or finance system.
