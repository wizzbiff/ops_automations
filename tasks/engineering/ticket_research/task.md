# Ticket Research, task

This is the instruction the task runs. It is on demand, not scheduled: you give it a ticket and it produces a ready-to-start brief. Paste this body into a Cowork task and fill in the Ticket field, or ask in natural language, for example "research PROJ-123 using tasks/engineering/ticket_research/task.md". Paths are written from the repo root so they resolve no matter where this file sits.

This is the repo's first parameterized task. The Ticket field below is a run-time input you fill in, not a config placeholder, so it is written as a blank rather than `{{...}}`.

---

**Ticket:** ____  (paste a Jira key like PROJ-123, or a full Jira issue URL, when you run this)

Run ticket research for the ticket above.

**Step 1. Load everything.** Read these files in full before doing anything else, and treat them as the source of truth:
* tasks/engineering/ticket_research/config.md, for the GitHub repo allowlist, search scopes, the comment toggle, and the caps.
* standards/engineering/research.md, for what a ready-to-start brief contains and how to gather it.
* standards/shared/style.md, for tone and formatting.
* tasks/engineering/ticket_research/research_template.md, for the output shape.
* config/config.md, optional, only to label related-issue status via standards/engineering/definitions.md. Not required.

If tasks/engineering/ticket_research/config.md does not exist, stop and say so. The system is not configured. Parse the ticket key from the Ticket field using `ticket_key_pattern` from config if set; if no key can be extracted, stop and say so rather than guessing.

**Step 2. Gather.** Following research.md:
* Jira, **required**, through the Atlassian connector. Resolve the ticket, its fields and comments, and follow its issue links one hop only. If Atlassian is unavailable, stop: without the ticket there is no brief.
* Confluence, enrichment, through the Atlassian connector. Pull linked docs from the ticket and its epic, scoped to `confluence_spaces` if set.
* GitHub, enrichment, through the GitHub connector. Search only the repos in `github_repos` for the ticket key in branch names, PR titles, and commit messages. If the allowlist is empty, skip GitHub and note it. Never search beyond the allowlist.
* Slack, enrichment, through the Slack connector. Search `slack_channels` for the key and title. If empty, skip and note it.

If an enrichment source is unavailable or its scope is empty, degrade gracefully: build the brief from what you have and flag the gap at the top. Only Atlassian (Jira) read is required.

**Step 3. Process.** Synthesize the gathered material into the brief per research.md. Keep facts and inferences distinct and flag every inference, including draft acceptance criteria and the suggested starting point. Label related-issue status and mark unconfirmed PR matches as such. Apply the section caps, honouring `code_context_cap` for code touchpoints.

**Step 4. Generate** the brief using research_template.md exactly, following style.md for tone. Put any data-incompleteness or guess flag at the very top.

**Step 5. Write output.** Save to output/ticket_research/<KEY>_YYYY_MM_DD.md using the ticket key and today's date, and overwrite output/ticket_research/latest.md with the same content.

**Step 6. Distribute.** If `post_jira_comment` is true, post a short pointer comment on the input ticket through the Atlassian connector. The comment is a notification, not the brief: a few plain lines (problem, one or two prior-art links, suggested starting point, and the output file path), ending with the signature token `[ticket_research:brief]`. Do not paste restricted Slack, Confluence, or private-repo content into the comment. Before posting, read the ticket's existing comments and look for one by the connected account containing `[ticket_research:brief]`: if found, edit it in place, or skip if the connector cannot edit; if not found, post one. Never create a duplicate. Record the comment action, posted, updated, or skipped, in the output file. If `post_jira_comment` is false, write the file only.

**Rules.**
* Required connector: Atlassian (Jira) read. Confluence, GitHub, and Slack are enrichment; degrade gracefully and flag gaps rather than stopping.
* The only write this task performs is exactly one comment on the input ticket. Never comment on related or linked issues. Never edit ticket fields, status, assignee, or links. Never @-mention anyone. Honour the `post_jira_comment` toggle.
* Never search GitHub beyond the allowlist. Never widen distribution beyond the input ticket and the output file.
* Do not fabricate missing docs, PRs, or threads. Distinguish searched-and-found-nothing from could-not-search.
* If you had to guess or infer anything material, flag it at the top of the brief, and in the comment if one is posted.

---

## Where fixes go

* What a brief should contain, how to follow links, match PRs, or search: fix standards/engineering/research.md, so every research brief gets the correction.
* How a related issue's status is labelled: fix standards/engineering/definitions.md, so it stays aligned with the other tasks.
* The repo allowlist, search scopes, comment toggle, or caps: fix your own tasks/engineering/ticket_research/config.md.
* Wrong shape or length: fix this folder's research_template.md.
* Wrong tone across all reports: fix standards/shared/style.md.
