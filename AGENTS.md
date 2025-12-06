# AGENTS.md

## Project Overview

Dify is an open-source platform for developing LLM applications with an intuitive interface combining agentic AI workflows, RAG pipelines, agent capabilities, and model management.

The codebase is split into:

- **Backend API** (`/api`): Python 3.11-3.12 Flask application organized with Domain-Driven Design
- **Frontend Web** (`/web`): Next.js 15 application using TypeScript 5.9+ and React 19
- **Docker deployment** (`/docker`): Containerized deployment configurations

## Environment Requirements

- **Python**: 3.11 to <3.13 (3.11 or 3.12 recommended)
- **Node.js**: >=22.11.0
- **pnpm**: 10.22.0 (auto-installed via corepack)
- **uv**: Latest version for Python dependency management

## Backend Workflow

- Run backend CLI commands through `uv run --project api <command>`.

- Before submission, all backend modifications must pass local checks:
  ```bash
  make lint         # Code formatting and linting (ruff)
  make type-check   # Type checking (basedpyright)
  make test         # Unit tests (pytest)
  ```

- Integration tests are CI-only and are not expected to run in the local environment.

## Frontend Workflow

```bash
cd web
pnpm lint          # ESLint linting
pnpm lint:fix      # Auto-fix linting issues
pnpm type-check    # TypeScript type checking
pnpm test          # Jest unit tests
```

## Testing & Quality Practices

- Follow TDD: red → green → refactor.
- Use `pytest` for backend tests with Arrange-Act-Assert structure.
- Enforce strong typing; avoid `Any` in Python and `any` in TypeScript.
- Write self-documenting code; only add comments that explain intent.

## Language Style

- **Python**: Keep type hints on functions and attributes, implement relevant special methods (e.g., `__repr__`, `__str__`), and use `ruff` for formatting.
- **TypeScript**: Use strict config, follow ESLint rules (@antfu/eslint-config), and avoid `any` types.

## General Practices

- Prefer editing existing files; add new documentation only when requested.
- Inject dependencies through constructors and preserve clean architecture boundaries.
- Handle errors with domain-specific exceptions at the correct layer.

## Project Conventions

- Backend architecture adheres to DDD and Clean Architecture principles.
- Async work runs through Celery with Redis as the broker.
- Frontend user-facing strings must use `web/i18n/en-US/` translation files; avoid hardcoded text.
- Use provided i18n tools: `pnpm check-i18n` and `pnpm auto-gen-i18n` for managing translations.
