# cpp

## Development setup

Use Python 3.12, available as `python3.12`, and create and activate a virtual
environment. Install the development tools and both Git hooks:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install pre-commit==4.2.0 pytest==8.3.5 ruff==0.11.13
pre-commit install
pre-commit install --hook-type pre-push
```

Keep the environment active when committing or pushing: the pytest hook uses
its Python interpreter and installed dependencies. Install the project's test
dependencies there as they are introduced.

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
pre-commit run --all-files
pre-commit run --hook-stage pre-push --all-files
```

For individual tools, run `ruff check .`, `ruff format --check .`, and `pytest`.
To update pinned hook versions, run `pre-commit autoupdate`, update the matching
Ruff version in the installation command above, and rerun both hook stages.
The framework installs its remote hook environments automatically. These local
hooks are not a substitute for CI: no GitHub Actions quality workflow is
configured yet, so developers must install and run the hooks themselves.
