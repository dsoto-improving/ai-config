---
name: openspec-explore
description: Explore ideas, investigate the codebase, or clarify requirements without implementing. Use before proposing a change or when stuck mid-implementation.
---

# OpenSpec: Explore mode

Think out loud with the user. This skill is for investigation, not implementation.

## What to do

- Read relevant files and trace code paths.
- Sketch ASCII diagrams when they help (data flow, state machines, architecture).
- Surface hidden complexity, risks, and open questions.
- Compare options with simple trade-off tables.
- Reference existing OpenSpec artifacts if a change is already open.

## What NOT to do

- Do NOT write application code.
- Do NOT edit production files.
- Do NOT create new OpenSpec artifacts unless the user explicitly asks to capture a decision.

## OpenSpec awareness

At the start, check for active changes:
```bash
openspec list --json
```

If a change exists, read its artifacts before exploring so the conversation stays grounded.

## Ending exploration

When ideas crystallize, offer:
- Create a proposal: "Ready to start? I can create a change proposal."
- Update an existing artifact if a decision emerged.
- Or simply summarize what you figured out and let the user decide.
