# Ticket Research

On demand, given a ticket, gathers its linked Confluence docs, related issues, GitHub pull requests and code context, and relevant Slack threads, then writes a ready-to-start brief and posts a short pointer to it on the ticket. It exists so you can begin work with the context already assembled instead of hunting across four apps.

## At a glance

* Cadence: on demand
* Requires connectors: Atlassian (Jira and Confluence), GitHub, Slack
* Reads standards: research.md, style.md (definitions.md optionally, to label related-issue status)
* Reads config: tasks/ticket_research/config.md (config/config.md optional)
* Writes to: output/ticket_research/, and one comment on the input ticket

## Run it

1. Authorize the connectors in Cowork: Atlassian, GitHub, and Slack.
2. Copy this folder's config.example.md to config.md and fill it in: the GitHub repo allowlist, optional Confluence spaces and Slack channels, the comment toggle, and the caps.
3. Invoke it with a ticket. Either paste the body of task.md into a Cowork task and fill the Ticket field with a Jira key or URL, or ask in natural language, for example "research PROJ-123 using tasks/ticket_research/task.md".
4. Read the brief in output/ticket_research/, and the pointer comment on the ticket if the toggle is on.

## Notes

This is the repo's first parameterized task and the only one that writes back to a source system. These are best confirmed on the first real run in Cowork, since this repo authors the task but cannot run it:

* The Ticket field in task.md is a run-time input, not a config placeholder. That is why it is a blank, not a `{{...}}` token.
* GitHub scope: the task searches only the repos in `github_repos`. If results look thin, widen the allowlist. It never searches beyond it.
* The Jira comment is a short pointer, not the full brief, so that restricted Slack, Confluence, or private-repo content is not widened to everyone who can see the ticket. The full brief stays in the output file.
* Idempotency: re-running on the same ticket edits or leaves the existing brief comment in place rather than adding a duplicate. Confirm your Atlassian connector can edit its own comments; if it cannot, the task leaves the old comment and notes it in the file.
* Enrichment outages degrade rather than fail: if GitHub, Confluence, or Slack is down or unscoped, you still get a brief, with the gap flagged at the top. Only Jira is required.
* Set `post_jira_comment` to false for a dry run that writes the file and posts nothing.
