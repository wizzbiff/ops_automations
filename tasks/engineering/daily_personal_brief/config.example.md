# Daily Personal Brief config

This task needs its own config. These are personal values specific to you, not overrides of the shared config, so they do not fall back to anything. The shared config/config.md is still read too, for the Jira status mapping.

Copy this file to config.md in this folder and fill in every value. config.md is ignored by git, so your real handles and channels never get committed. Each value is written as `{{UPPER_SNAKE_CASE}}`. Replace the whole token, braces included.

## Sources

Pick where mail and calendar are read from. Each is independent: you can run Gmail mail with Outlook calendar if that is your setup.

```yaml
mail_source:     {{MAIL_SOURCE}}      # gmail or m365
calendar_source: {{CALENDAR_SOURCE}}  # google or m365
calendars:       [{{CALENDARS}}]      # which calendars to read. leave empty for your primary only
```

Filled example, for reference only. Delete it in your real config.

```yaml
mail_source:     gmail
calendar_source: google
calendars:       []
```

## Identity

Your handles in each system, so the task knows what "to me", "mentions me", and "assigned to me" mean.

```yaml
email_address:   {{EMAIL_ADDRESS}}
slack_handle:    {{SLACK_HANDLE}}
jira_account:    {{JIRA_ACCOUNT}}   # leave as currentUser to use the connected Jira account
```

## What to surface

```yaml
important_senders: [{{IMPORTANT_SENDERS}}]   # emails or names that always surface
slack_channels:    [{{SLACK_CHANNELS}}]      # channels to scan beyond DMs and mentions
slack_keywords:    [{{SLACK_KEYWORDS}}]      # words that surface a channel message
```

Filled example, for reference only:

```yaml
important_senders: ["ceo@example.com", "Jordan Lee"]
slack_channels:    ["incidents", "team_eng"]
slack_keywords:    ["prod down", "release"]
```

## Timing and delivery

```yaml
brief_timezone:  {{BRIEF_TIMEZONE}}    # IANA name, for example America/New_York. controls "today" and the lookback
lookback:        {{LOOKBACK}}          # how far back to scan, for example "since previous business day"
slack_dm_target: {{SLACK_DM_TARGET}}   # where the brief is delivered. your own handle, for a DM to yourself
```

Filled example, for reference only:

```yaml
brief_timezone:  America/New_York
lookback:        since previous business day
slack_dm_target: "@rob"
```
