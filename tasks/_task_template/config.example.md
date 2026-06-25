# [Task name] config, optional

Most tasks need nothing here. They read the shared config/config.md. Use this file only when a task must override a shared value, for example posting to a different Slack channel than the default, or running against a subset of teams.

Copy to config.md in this folder if you need it. It is ignored by git like the shared config. If you do not need overrides, delete this file from your copy of the task.

```yaml
# overrides only. anything not set here falls back to config/config.md
report_slack_channel: {{OVERRIDE_SLACK_CHANNEL}}
teams_filter:         [{{ONLY_THESE_TEAMS}}]
```
