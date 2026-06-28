# Board Metrics

Once a month, after the books close, assembles the board metrics pack: financial metrics from NetSuite, growth and product metrics from Looker, and OKR progress from Jira, measured against the executive standard and compared to last month, written as a board-ready document and summarized to the leadership channel. It is the first task in the executive domain and the first that reads from a BI layer and a finance system rather than from Jira and Slack alone.

## At a glance

* Cadence: monthly, after month-end close, same day each month
* Requires connectors: Looker, NetSuite, Atlassian (Jira), Slack
* Reads standards: board_metrics.md, style.md
* Reads config: tasks/executive/board_metrics/config.md (this task does not use the shared config/config.md)
* Writes to: output/board_metrics/

## Run it

1. Authorize the connectors in Cowork. Looker and NetSuite are not part of the default connector set and must be added first; Atlassian and Slack are already used by the engineering tasks. See config/connectors.md.
2. Copy this folder's config.example.md to config.md and fill in the look ids, NetSuite report refs, the OKR project and fields, targets and plan, fiscal year start, runway floor, and the board channel.
3. Run by hand once: paste the body of task.md into a Cowork task and read the result. The first run usually reveals a look id, NetSuite report name, or Jira field that does not match config. Fix config and rerun.
4. When the metrics and OKR health look right, schedule it with `/schedule` for a fixed day each month after close.

## Notes

* Trend appears only from the second run on. It compares this month to the previous run's saved output at output/board_metrics/latest.md. The first run says "no prior month to compare." Run it monthly, on the same day, so the windows tile.
* OKRs are quarterly; the monthly pack shows quarter-to-date progress. The last pack of a quarter is the one that scores the quarter.
* Connectors degrade gracefully: if one source is down, its section is marked unavailable and flagged at the top rather than dropping silently. If all three data sources are down, the task stops and writes nothing over a good prior pack.
* The pack holds sensitive financial and OKR data. It distributes only to the configured board channel, and is primarily a written artifact a person carries to the board; board members are not assumed to be in Slack.
* Keep it to roughly two screens. If it runs long, the template or the metric count, not the task, is usually the cause.
