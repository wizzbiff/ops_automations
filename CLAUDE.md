# CLAUDE.md

Operating rules for building this repo with Claude Code. At the start of a session, read PROJECT_CONTEXT.md (roadmap, backlog, and decisions), CONTRIBUTING.md (how to add tasks and domains), and README.md (structure and catalog). This file holds only the rules whose absence would cause a mistake.

## What this repo is

A library of Claude Cowork automations across operational domains. The automations run in Cowork. This repo only authors them. The full picture is in PROJECT_CONTEXT.md.

## Build surface boundary, read this first

Claude Code authors and commits the files. It cannot run the automations. Connectors, scheduled tasks, and Slack posting only execute in Cowork. So "done" for a backlog item means the files are complete, consistent, and committed, not that the automation was seen working. Do not claim an automation works. Say the artifacts are ready to install and test in Cowork. Runtime validation happens there.

## Non negotiable rules

* Build from the existing files. Extend them. Do not regenerate a file from memory.
* Keep the layers separate. Shared content lives in standards/shared/ and config/. Domain content lives in standards/<domain>/ and tasks/<task>/. Never put domain specifics in the shared layer, and never copy shared content into a domain.
* Never commit a real config.md. Only config.example.md is committed. No project keys, board ids, channels, or handles in any committed file.
* Placeholders are written {{UPPER_SNAKE_CASE}} and live only in config.example.md or template files, never in a standard or a task's logic.
* Identifiers (folders, task names, skill and plugin names) use underscores, to match the existing tree. Do not introduce hyphenated names.
* Any change that adds or renames a task or domain updates three places in the same commit: the README task catalog, CHANGELOG.md, and the item status in PROJECT_CONTEXT.md.

## Standard workflow for a backlog item

1. Read PROJECT_CONTEXT.md and pick the next item marked PLANNED.
2. Create one branch for that item.
3. Build it using CONTRIBUTING.md. For a task, copy tasks/_task_template/. For a new domain, create standards/<domain>/ first, then add its first task.
4. Wire references: point the task at standards/shared/style.md and its domain standard, read config from the local config.md, and write output to output/<task>/.
5. Run the verify checks below.
6. Update the README catalog, CHANGELOG.md, and the item status in PROJECT_CONTEXT.md.
7. Commit in small, reviewable steps with clear messages. Do not push to a shared branch unless asked.

The /add_task, /add_domain, and /check_repo commands in .claude/commands encode these steps.

## Verify before commit

* grep the tree for path references after any move or rename. No reference should point at a path that no longer exists.
* No {{...}} placeholders remain in committed standards or task logic.
* Nothing under config/ except config.example.md and connectors.md is staged. config.md is gitignored; confirm nothing slipped in.
* The README catalog and CHANGELOG reflect the change.

## Two artifacts

ops_automations is this repo, the folder library and the source of truth you build in. ops_marketplace is a parallel plugin marketplace, parked, kept in its own separate repo. Build here. Do not maintain both in lockstep. PROJECT_CONTEXT.md explains when to promote the marketplace.
