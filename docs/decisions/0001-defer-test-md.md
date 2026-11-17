# ADR 0001: Defer defining `Test.md`

- **Status:** Accepted for the current change
- **Date:** 2026-11-17

## Context

The work-branch tree contains `Readme.md` and `.github/workflows/threadline-verify.yml`, but no application source, test files, or dependency manifests. The README did not describe the project. No existing decision record for this change was found on the branch.

A verification run at head `cf334c73bb10396f79d13bd1e6ba33329514e3a9` reported pytest 9.2.0 on Python 3.12.16 with `collected 0 items` and exit code 5. This indicates no tests were collected, not an identified failing test. Ruff exited 0 while warning no Python files were found; Bandit exited 0 after scanning zero lines; pip-audit exited 0 with no known vulnerabilities in the installed environment for that run. None of these results establish application behavior.

The workflow installs from `requirements.txt` and `requirements-dev.txt` when present and editable installs when `pyproject.toml` or `setup.py` exists. An independent review reported a medium concern that pip-audit examines the installed environment and may omit dependency declarations in other manifests. This remains a potential audit coverage limitation, not an established vulnerability.

## Decision

Defer creating `Test.md` until its purpose, intended audience, and required contents are clarified. If it is intended to document tests, also identify the application behaviors, test framework, and execution commands; pytest is used by CI, but this alone does not establish it as the intended project test framework. Do not add artificial tests or change CI behavior merely to hide pytest's empty-suite exit status. Do not decide whether the README should link to `Test.md` until its purpose is known.

## Consequences

- No `Test.md` or fabricated test cases are added in this change.
- The README describes only the workflow and observed verification results, with their limitations.
- The empty pytest suite remains a known verification gap; no application behavior was exercised.
- The reported pip-audit scope concern remains unresolved and should be assessed when all dependency sources are known.

## Evidence

- Work branch: `threadline/clarify-test-md-purpose`, head `cf334c73bb10396f79d13bd1e6ba33329514e3a9`.
- Workflow: `.github/workflows/threadline-verify.yml`.
- CI run: [44158813577](https://github.com/sameer-893/Threadline/actions/runs/44158813577).
