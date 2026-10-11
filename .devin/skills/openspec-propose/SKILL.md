---
name: openspec-propose
description: Propose a new change using OpenSpec. Creates proposal, design, and tasks when the change is non-trivial or uncertain. Skip OpenSpec for one-line fixes.
---

# OpenSpec: Propose a change

Use this skill when the user wants to build or fix something that is non-trivial, affects more than one file, or has open questions.

## When to skip OpenSpec

Do NOT create a formal change for:
- One-line bug fixes.
- Renames or small refactors confined to a single file.
- Updating an env variable or config value.
- Trivial copy/label changes.

In those cases, implement directly and move on.

## Steps

1. **Understand the request.** If it is vague, ask a clarifying question before proceeding.
2. **Pick a kebab-case name** (e.g. `add-meta-ads-summary`, `fix-report-pdf-export`).
3. **Create the change:**
   ```bash
   openspec new change "<name>"
   ```
4. **Check required artifacts:**
   ```bash
   openspec status --change "<name>" --json
   ```
5. **Create artifacts in dependency order** using the output of:
   ```bash
   openspec instructions <artifact-id> --change "<name>" --json
   ```
   Common artifact order: `proposal` → `design` → `tasks`.
   - Keep artifacts concise. Hackathon velocity over encyclopedic docs.
   - Read dependency artifacts before writing the next one.
   - Do NOT copy `context` or `rules` blocks from the instructions into the artifact.
6. **Stop when `applyRequires` artifacts are done.** Usually `tasks` is the last required artifact.
7. **Summarize:** change name, artifacts created, and next action (`/opsx:apply <name>` or manual implementation).

## Output

- Change location: `openspec/changes/<name>/`
- Created artifacts with one-line descriptions.
- Prompt the user to review the proposal before applying.
