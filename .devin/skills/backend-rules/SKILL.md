---
name: backend-rules
description: Backend development rules for the measurable-backend FastAPI service. Keep velocity high while avoiding regressions.
---

# Backend development rules

Stack: Python 3.11+, FastAPI, SQLAlchemy 2, Alembic, Poetry, pytest.

## Code style

- Follow the existing flat structure in `app/`. Do not force hexagonal architecture on legacy modules.
- For new modules, prefer a single file until it becomes painful; then split by concern (models, schemas, routes, logic).
- Use clear, pronounceable names in English. Avoid `helper`, `util`, `manager`.
- Keep functions small enough to read in one screen. If a function needs more than 3 parameters, group them in a Pydantic model.
- Avoid boolean flags that change behavior; prefer explicit functions.

## FastAPI endpoints

- Add Pydantic schemas for request/response. Reuse `schemas.py` patterns or define them next to the route if localized.
- Use `Depends(get_db)` for DB sessions and `Depends(get_current_user)` for auth.
- Return appropriate HTTP status codes: 201 for creation, 204 for no-content deletes.
- Do not expose stack traces, SQL details, or internal paths in error responses.

## Database

- SQLAlchemy models live in `app/models.py` or in a domain module if splitting.
- Every model change needs an Alembic migration:
  ```bash
  PYTHONPATH=. poetry run alembic revision --autogenerate -m "describe change"
  PYTHONPATH=. poetry run alembic upgrade head
  ```
- Keep migrations backward-compatible when possible during active development.
- Use PostgreSQL for local dev (Docker container). SQLite is acceptable only for tests.

## Tests

- Use pytest. Tests live in `tests/`.
- For unit tests, use SQLite in-memory or a temp file and set required env vars (`DATABASE_URL`, `JWT_SECRET`, `AWS_REGION`, etc.).
- Mock external services (Meta, Shopify, TikTok, Stripe, Anthropic, AWS) with `monkeypatch` or `unittest.mock`.
- Do not mock the database itself.
- Add tests for: happy path, one failure path, and any edge case that could silently corrupt data.

## Secrets and env

- Required env vars are documented in `AGENTS.md` and `.env`.
- Never log secrets. Never commit `.env` files.
- New integrations must read credentials from `app.config.settings`, not hardcode them.

## Error handling

- Raise `HTTPException` for client errors with a clear `detail` message.
- Let unexpected technical errors bubble up to the FastAPI default handler during development.
- Use custom exceptions in `app/errors.py` where a pattern already exists.

## When to ask the user

- Schema migrations that drop data.
- Changes to authentication or authorization rules.
- New external integrations that need real credentials or sandbox setup.
