# Threadline

## Project status

The current work-branch tree contains a verification workflow, but no application source, dependency manifest, or test files. The repository does not yet specify the purpose or audience of `Test.md`; do not infer test scenarios or commands from its name alone.

## Verification

The GitHub Actions workflow [`.github/workflows/threadline-verify.yml`](.github/workflows/threadline-verify.yml) runs on pushes to `threadline/**` branches and supports manual dispatch. It uses Python 3.12, installs pytest, Ruff, Bandit, and pip-audit, and installs dependencies from `requirements.txt`, `requirements-dev.txt`, and editable project metadata when those files exist. It then runs `pytest -rA`, `ruff check .`, `bandit -r . -x ./tests,./.git`, and `pip-audit`.

A recorded run (head `cf334c73bb10396f79d13bd1e6ba33329514e3a9`) failed because pytest collected zero tests and exited 5. Ruff found no Python files; Bandit scanned zero lines; pip-audit found no known vulnerabilities in the installed environment for that run. These results do not demonstrate application behavior or a complete audit of dependency sources not installed by the workflow.

## Documentation decision

See [ADR 0001](docs/decisions/0001-defer-test-md.md): defer creating `Test.md` until its purpose, audience, and required contents are clarified. If it is to document tests, confirm behaviors, framework, and commands first. Whether this README should link to a future `Test.md` remains undecided.
