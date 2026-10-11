---
name: openspec-archive-change
description: Archive a completed OpenSpec change. Moves it to openspec/changes/archive/ after verifying tasks and artifacts.
---

# OpenSpec: Archive a change

Finalize a change after implementation is complete.

## Steps

1. **Select the change.** If not provided, run:
   ```bash
   openspec list --json
   ```
   and ask the user.
2. **Check artifact completion:**
   ```bash
   openspec status --change "<name>" --json
   ```
3. **Check tasks file** for incomplete tasks (`- [ ]`). Warn if any remain, but archive if the user confirms.
4. **Sync delta specs if they exist.** If `openspec/changes/<name>/specs/` has files, compare them with `openspec/specs/<capability>/spec.md` and offer to sync.
5. **Archive:**
   ```bash
   mkdir -p openspec/changes/archive
   mv openspec/changes/<name> openspec/changes/archive/$(date +%Y-%m-%d)-<name>
   ```
6. **Show summary:** change name, schema, archive location, spec sync status.

## Guardrails

- Always prompt for the change if not provided.
- Do not delete the `.openspec.yaml` inside the change directory.
- Archive does not mean deploy; it means the change is no longer active.
