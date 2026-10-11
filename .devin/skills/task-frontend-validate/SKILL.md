---
name: task-validate
description: Run frontend validation checks quickly (build, lint, typecheck, targeted tests) and report results without blocking on warnings.
---

# Task: Validate frontend

Run the fastest validation suite that covers the current change.

## Default checks

1. **Type check:**
   ```bash
   npx tsc --noEmit
   ```
2. **Lint:**
   ```bash
   npm run lint
   ```
3. **Build smoke test** (only when the change affects build-critical paths):
   ```bash
   npm run build
   ```
4. **Targeted tests** (when a relevant test exists):
   ```bash
   npm run test:<relevant-script>
   ```

## Output

- Commands run.
- Pass/fail summary.
- If failures exist, show the smallest actionable excerpt.
- If only warnings, note them and continue.

## Guardrails

- Fail fast: stop at the first real failure.
- Do not run the full build on every tiny change unless the user asks.
- Keep feedback concise.
