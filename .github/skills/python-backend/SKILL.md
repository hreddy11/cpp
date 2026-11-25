---
name: python-backend
description: Use when implementing, reviewing, or testing Python backend code in this repo, including FastAPI endpoints, Pydantic schemas, service logic, and pytest tests.
---

# Python Backend Development

General rules (typing, security, git workflow, scope control) live in
`.github/copilot-instructions.md`. This skill covers the implementation workflow.

## Stack

Python 3.12, FastAPI, Pydantic, pytest, Ruff (lint and format).

## Implementation

1. Keep route handlers thin; put business logic in service functions or classes.
2. Use Pydantic models for all request and response bodies.
3. Use appropriate HTTP status codes and handle errors explicitly.
4. Never expose internal exception details to clients.
5. Avoid unnecessary abstractions and dependencies.

## Financial logic

- Use Decimal for monetary values and financial calculations, never float. Choose appropriate types for non-monetary quantities.
- Validate monetary inputs (sign, precision, range).
- Keep financial calculations separate from API routing.
- Wrap operations that must succeed or fail together in one transaction.
- Make writes idempotent; prefer reversals over overwriting records.

## Testing

For every new feature, add pytest tests covering:
1. Successful requests
2. Invalid input
3. Missing and boundary values
4. Error handling
5. Duplicate or repeated requests, for write endpoints

Use FastAPI `TestClient` for API tests.

## Before completing a task

Run and report the results of:

    ruff check .
    ruff format --check .
    pytest

Then:
- Review the diff for unrelated changes.
- List assumptions and limitations.
- Summarize changed files and test results.
- Never claim tests passed unless they were actually executed.