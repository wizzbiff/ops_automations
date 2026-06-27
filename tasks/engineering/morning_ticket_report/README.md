# Morning Ticket Report

Pulls every team's Jira activity each morning, classifies what is blocked, at risk, or stale against the shared standard, writes a short report, and posts the leader facing summary to Slack.

## At a glance

* Cadence: weekday mornings, before standup
* Requires connectors: Atlassian, Slack
* Reads standards: definitions.md, style.md
* Reads config: config/config.md
* Writes to: output/morning_ticket_report/

## Run it

1. Authorize the Atlassian and Slack connectors in Cowork.
2. Copy config/config.example.md to config/config.md and fill it in.
3. Run by hand once: paste the body of task.md into a Cowork task and read the result. The first run usually reveals that your real Jira status names do not match the config mapping. Fix config and rerun.
4. When the classification looks right, schedule it with `/schedule`.

## Notes

* The whole report stays under 500 words by standard. If it runs long, the template or the team count, not the task, is usually the cause.
* Distribution is Slack only. See config/connectors.md for why, and the options if your leaders live in email.
