# Contributing

This repo is a shared standard. The value comes from everyone running the same definitions, so changes to shared files are deliberate and visible.

## Conventions

* **Placeholders.** Every value an adopter supplies is written `{{UPPER_SNAKE_CASE}}` and lives only in a `config.example.md`. If you see `{{...}}` in `standards/` or in a task's logic, it is a bug. Reference config by name instead.
* **Paths.** Task instructions reference files from the repo root, for example `standards/engineering/definitions.md`, so they resolve regardless of where they run.
* **No secrets in committed files.** Real project keys, board ids, channels, and handles go only in `config.md` files, which git ignores. Never paste them into a committed file.
* **Output.** Each task writes to `output/its_name/`. The output folder is ignored by git.

## Changing a standard

Standards come in two kinds. A shared standard under `standards/shared/` changes the voice of every report in every domain. A domain standard under `standards/<domain>/` changes behavior for that domain's tasks only. Either way, the change affects everyone who runs the affected tasks. So:

1. Open the change for review rather than committing directly.
2. Describe what changes and why in the change.
3. Add an entry to CHANGELOG.md with a new version.
4. Once merged, adopters get the new standard by pulling. Their config is untouched.

If only your team needs a different value, that is usually a sign it belongs in config as an override, not a fork of the standard. Discuss before forking.

## Adding a domain

1. Create `standards/your_domain/` and write its definitions there. Reuse `standards/shared/style.md` for tone rather than restating it.
2. Add the domain's tasks under `tasks/`, each copied from the template and pointed at the new domain standard.
3. Update the task catalog in the README and add a CHANGELOG note.

Nothing in an existing domain changes when you add another.

## Adding a task

1. Copy `tasks/_task_template/` to `tasks/your_task_name/`.
2. Replace every bracketed field in task.md, the output template, and the README.
3. Reuse existing definitions and style. Only add to `standards/` if a genuinely new shared concept is needed.
4. Record required connectors in config/connectors.md.
5. Add a row to the task catalog in the root README.
6. Test by running the task by hand before anyone schedules it.

## Reviewing

A task is ready to share when: it loads context before acting, it stops safely and distributes nothing if a connector is missing, it writes to its own output folder, and it contains no personal values or secrets.
