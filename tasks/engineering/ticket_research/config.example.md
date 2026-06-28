# Ticket Research config

This task needs its own config. These are values specific to your setup, not overrides of the shared config, so they do not fall back to anything. The shared config/config.md is read only optionally, to label related-issue status.

Copy this file to config.md in this folder and fill in every value. config.md is ignored by git, so your real repo names and channels never get committed. Each value is written as `{{UPPER_SNAKE_CASE}}`. Replace the whole token, braces included.

## GitHub

The allowlist of repositories to search for related PRs, branches, and commits, by ticket key. Required for any GitHub lookup. If you leave it empty, GitHub is skipped entirely; the task never searches beyond this list.

```yaml
github_repos: [{{GITHUB_REPOS}}]   # owner/repo entries
```

Filled example, for reference only. Delete it in your real config.

```yaml
github_repos: ["acme/web", "acme/api"]
```

## Search scope

Optional. Narrow where the task looks. Leave a list empty to follow links only (Confluence) or to skip that search (Slack).

```yaml
confluence_spaces: [{{CONFLUENCE_SPACES}}]   # space keys to prioritize. empty = follow links only
slack_channels:    [{{SLACK_CHANNELS}}]      # channels to search for the key and title. empty = skip Slack search
```

## Output and behavior

```yaml
post_jira_comment: {{POST_JIRA_COMMENT}}   # true to post a pointer comment on the ticket, false to write the file only
code_context_cap:  {{CODE_CONTEXT_CAP}}    # max PRs or files to detail before summarizing, for example 5
ticket_key_pattern: {{TICKET_KEY_PATTERN}} # optional, to parse the key from a URL or text, for example [A-Z]+-[0-9]+
```

Filled example, for reference only:

```yaml
post_jira_comment: true
code_context_cap:  5
ticket_key_pattern: "[A-Z]+-[0-9]+"
```
