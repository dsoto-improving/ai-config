---
name: task-qa
description: Functional QA for backend changes. Verify behavior against the OpenSpec change or user request, including manual API checks.
---

# Task: Backend QA

Verify that a backend change behaves as intended. Combine automated tests with targeted manual checks.

## Steps

1. **Read the spec or change request.** If an OpenSpec change exists, read `tasks.md` and `design.md`.
2. **Run relevant tests.**
3. **Manually exercise the API** when needed:
   ```bash
   curl -s http://localhost:8001/<endpoint>
   ```
   or use the FastAPI docs at `http://localhost:8001/docs`.
4. **Check common failure modes:**
   - Missing auth header returns 401/403 as expected.
   - Invalid payload returns 422 with clear errors.
   - Non-existent resource returns 404.
   - Duplicate create returns 409 if the endpoint supports it.

## Output

- What was verified.
- Pass/fail for each check.
- Any bugs or inconsistencies found.
- Suggested next step (fix, merge, or deeper test).

## Guardrails

- Do not QA production systems.
- Do not create or modify real user data during manual checks.
- Keep manual checks minimal; prefer automated tests for regression coverage.
