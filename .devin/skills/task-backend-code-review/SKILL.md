---
name: task-code-review
description: Lightweight code review for the backend. Focus on bugs, clarity, security, and regression risks, not architectural purity.
---

# Task: Backend code review

Review a code change quickly. This is a lightweight review for hackathon velocity, not a deep architectural audit.

## Checklist

1. **Correctness**
   - Does the change do what the task says?
   - Are edge cases handled (empty input, missing DB rows, duplicate keys)?
   - Are date/time, timezones, and currency handled consistently with the rest of the app?

2. **Security**
   - No secrets hardcoded.
   - No SQL injection via raw queries (use SQLAlchemy parameters).
   - Auth checks present on mutating endpoints.
   - Error messages do not leak internal details.

3. **Database**
   - Model changes have a matching Alembic migration.
   - Migrations do not drop data unexpectedly.
   - Indexes added for queries that will run frequently.

4. **Testing**
   - New behavior has at least a happy-path test.
   - External services are mocked.
   - Tests run and pass.

5. **Readability**
   - Names are clear.
   - Functions are not overly long.
   - No dead code or commented-out blocks left behind.

## Output

- List of issues found, ordered by severity: blocking / should-fix / nit.
- If blocking issues exist, suggest fixes or ask the user before merging.
- If only nits, mention them but do not block.
- Keep each issue to one sentence with a file/line reference when possible.
