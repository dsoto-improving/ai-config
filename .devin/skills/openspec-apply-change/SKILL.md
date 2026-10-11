---
name: openspec-apply-change
description: Implement tasks from an OpenSpec change. Works through the tasks file, marks them complete, and pauses on blockers.
---

# OpenSpec: Apply a change

Implement the tasks of an existing OpenSpec change. Use after the proposal/design/tasks artifacts are ready.

## Steps

1. **Identify the change.** If not provided, run:
   ```bash
   openspec list --json
   ```
   and ask the user which one to apply.
2. **Check status:**
   ```bash
   openspec status --change "<name>" --json
   ```
3. **Get apply instructions:**
   ```bash
   openspec instructions apply --change "<name>" --json
   ```
4. **Read the context files** listed in `contextFiles` (proposal, design, tasks, specs).
5. **Show progress:** schema, N/M tasks complete, current task.
6. **Implement each pending task:**
   - Keep the change minimal and focused on the task.
   - Mark the task complete (`- [ ]` → `- [x]`) immediately after it works.
   - Run the relevant validate command before moving on.
   - Pause if a task is unclear, reveals a design issue, or hits an error.
7. **On completion or pause, show status.**

## Validate as you go

For this repo:
```bash
PYTHONPATH=. poetry run pytest -q <relevant-test>
PYTHONPATH=. poetry run ruff check . || true
```

Use the fastest check that covers the task. Do not run the full slow suite on every green step.

## Guardrails

- Do not skip reading the tasks file.
- Do not batch-unrelated changes into one task.
- Do not rewrite unrelated code "while I'm here".
- If the implementation invalidates the design, pause and suggest updating `design.md` before continuing.
