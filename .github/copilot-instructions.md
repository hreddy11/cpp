# Portfolio Management API — Copilot Instructions

## 1. Project overview

We are building a production-oriented Portfolio Management API
using Python 3.12 and FastAPI.

The project is intended to demonstrate:
- Python backend engineering
- REST API design
- PostgreSQL and SQL optimization
- Docker and Kubernetes
- Helm deployments
- GitHub Actions CI/CD
- Responsible AI-assisted software development

Keep the implementation simple, modular, testable, and maintainable.

## 2. General development rules

- Use Python 3.12.
- Follow PEP 8 (enforced by Ruff).
- Add type hints to all function signatures.
- Prefer clear, readable code over unnecessary abstractions.
- Use meaningful variable and function names.
- Add docstrings to public functions and classes.
- Avoid unnecessary dependencies.
- Do not introduce unrelated changes.

## 3. API development

- Use FastAPI for REST APIs.
- Use Pydantic for request and response validation.
- Use appropriate HTTP status codes.
- Keep API routes separate from business logic.
- Version API endpoints under `/v1`.
- Handle errors consistently.
- Never expose internal exception details to API clients.

## 4. Financial data rules

This is a portfolio management application.

- Use `Decimal` for financial calculations.
- Never use `float` for monetary values.
- Use PostgreSQL `NUMERIC` for monetary database columns.
- Validate financial inputs.
- Use database transactions for operations that must succeed or fail together.
- Make write operations idempotent so duplicate requests are handled safely
  (for example, with idempotency keys).
- Do not silently overwrite financial records.
- Prefer auditable corrections or reversals where appropriate.

## 5. Testing

- Use pytest.
- Add tests for new functionality.
- Include positive, negative, and edge-case tests.
- Do not modify or remove tests merely to make an implementation pass.
- Run relevant tests before submitting changes.

## 6. Code quality

- Use Ruff for both linting and formatting.
  - Lint: `ruff check .`
  - Format: `ruff format .`
- Do not add Black, isort, or Flake8; Ruff replaces them.
- Keep Ruff configuration in `pyproject.toml`.
- Follow the repository's pre-commit configuration.
- Avoid hardcoded credentials, secrets, and environment-specific paths.
- Use environment variables for configuration.

## 7. Security

- Never commit passwords, API keys, access tokens, or private keys.
- Validate all external input.
- Avoid logging sensitive information.
- Follow least-privilege principles.
- Do not disable security checks to make tests pass.

## 8. Git and pull request workflow

- Work on a feature branch.
- Do not commit directly to the default branch.
- Keep changes focused on the assigned issue.
- Add or update tests and documentation where needed.
- Explain important design decisions in the pull request.
- Never merge a pull request without explicit human approval.

## 9. AI-assisted engineering

- Use AI tools to accelerate implementation, testing, debugging, and documentation.
- Review generated code for correctness, security, performance, and maintainability.
- Do not assume AI-generated code is correct.
- Do not invent requirements when the issue is unclear.
- State assumptions explicitly and ask for clarification when necessary.

## 10. Scope control

- Implement only what the assigned issue requests.
- Do not introduce PostgreSQL, Docker, Kubernetes, AWS, or other infrastructure
  until the issue for that project stage requests it. The financial data rules
  in section 4 apply once the database exists.
- Preserve existing project conventions.
- Prefer the smallest complete implementation.
