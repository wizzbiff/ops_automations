# [Task name], task

Copy this folder to tasks/your_task_name/ to start a new automation, then replace everything in brackets. Keep the step shape. It is the pattern every task in this repo follows: load context first, do the work, write output, distribute, and stop safely on failure.

---

Run [the task, in one line].

**Step 1. Load everything.** Read these files in full first and treat them as the source of truth:
* config/config.md, for teams, status mapping, and distribution.
* standards/[your_domain]/[definitions].md, for the classification this task uses.
* standards/shared/style.md, for tone and formatting.
* tasks/[your_task_name]/[output_template.md], for the output shape.
* [any task specific config or context this task needs].

If config/config.md does not exist, stop and say so.

**Step 2. Gather.** [Which connectors to call and what to pull. Reference shared JQL or query patterns from standards where possible rather than inventing new ones.]

**Step 3. Process.** [How to classify, summarize, or transform what you gathered. Reuse the definitions in your domain standard under standards/[your_domain]/ so terms mean the same thing across every task in the domain.]

**Step 4. Generate.** Produce the output using this folder's template, following style.md.

**Step 5. Write output.** Save to output/[your_task_name]/[name]_YYYY_MM_DD.md and overwrite output/[your_task_name]/latest.md.

**Step 6. Distribute.** [Where the result goes, by name from config, not hardcoded.]

**Rules.**
* Only include data the recipients can access.
* If a required connector is unavailable, stop, write a short note to output/[your_task_name]/latest.md, and distribute nothing.
* Flag anything material that was guessed.

---

## Where fixes go

* Domain definitions or thresholds: standards/[your_domain]/.
* Shared tone: standards/shared/style.md.
* Adopter values: config/config.md.
* This task's shape: this folder's template.
