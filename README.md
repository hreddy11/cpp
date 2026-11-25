# cpp

## Development setup

Install [uv](https://docs.astral.sh/uv/getting-started/installation/) (for
example, `brew install uv` on macOS). From the repository root, synchronize the
Python 3.12 environment and install both Git hooks:

```bash
uv sync --locked
uv run --locked pre-commit install
uv run --locked pre-commit install --hook-type pre-push
```

`uv sync` creates `.venv` and installs the locked development dependencies.
Run commands through `uv run --locked` without activating the environment.
Git hooks require `uv` to be on `PATH`, including when invoked from an IDE.

The commit hook removes trailing whitespace, fixes missing final newlines, and
checks YAML, JSON, merge conflict markers, and Python syntax trees. It also
checks Python with Ruff and formats changed Python files. These checks catch
common mistakes before they enter the repository; fixes must be staged again.

The push hook runs Ruff lint and formatting checks across the project and runs
pytest once. A failed check blocks the push; pytest's "no tests collected" exit
code is treated as a skip until tests are added. Ruff handles both linting and
formatting, as required by the repository's development instructions; Black is
not installed or run.

Run all checks manually, including against all tracked files, with:

```bash
uv run --locked pre-commit run --all-files
uv run --locked pre-commit run --hook-stage pre-push --all-files
```

For individual tools, run `uv run --locked ruff check .`,
`uv run --locked ruff format --check .`, and `uv run --locked pytest`.
Pytest exits with code 5 when no tests are collected; only the push hook treats
that as a skip.

To update pinned hook versions, run `uv run --locked pre-commit autoupdate`.
Keep the Ruff development dependency in sync with the Ruff hook version using
`uv add --dev ruff==<version>`, commit the updated lockfile, and rerun both hook
stages. The framework installs its remote hook environments automatically.
These local hooks are not a substitute for CI: no GitHub Actions quality
workflow is configured yet, so developers must install and run the hooks.
