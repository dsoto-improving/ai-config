---
name: task-qa
description: Functional QA for frontend changes. Verify UI behavior against the OpenSpec change or user request, including manual browser checks.
---

# Task: Frontend QA

Verify that a frontend change behaves as intended in the browser.

## Steps

1. **Read the spec or change request.** If an OpenSpec change exists, read `tasks.md` and `design.md`.
2. **Run targeted tests** if they exist.
3. **Manual browser check:**
   - Open http://localhost:3000 (or the relevant route).
   - Exercise the happy path.
   - Check error/empty/loading states.
   - Verify responsive behavior at 375px and 1440px if the change affects layout.
4. **Common checks:**
   - Console has no errors.
   - Network requests succeed.
   - Navigation and back button work.
   - Forms validate and show errors.

## Output

- What was verified.
- Pass/fail per check.
- Screenshots or descriptions of any visual issue.
- Suggested next step.

## Guardrails

- Do not QA production.
- Do not create real accounts or real data during manual checks.
- Keep manual checks scoped; prefer automated tests for regressions.
