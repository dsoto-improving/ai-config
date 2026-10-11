---
name: task-validate
description: Run backend validation checks quickly (typecheck, lint, tests) and report results without blocking on warnings.
---

# Task: Validate backend

Run the fastest validation suite that covers the current change. Do not run the full slow test suite unless the user asks for it.

## Default checks

1. **Syntax / import smoke test:**
   ```bash
   PYTHONPATH=. poetry run python -c "import app.main"
   ```
2. **Relevant tests:**
   ```bash
   PYTHONPATH=. poetry run pytest -q tests/test_<related>.py
   ```
   If no specific test is obvious, run a targeted subset that touches the changed module.
3. **Full test suite (only when asked):**
   ```bash
   PYTHONPATH=. poetry run pytest -q
   ```

## Lint / format

- This project currently has no configured linter. Do not introduce one unless the user asks.
- If a linter is added later, run it here.

## Output

- Command(s) run.
- Pass/fail summary.
- If failures exist, show the smallest actionable excerpt. Do not dump the entire log.
- If only warnings, note them and continue.

## Guardrails

- Fail fast: stop at the first real failure and report it.
- Do not treat warnings as blockers unless the user says so.
- Keep feedback concise so the user can iterate quickly.
