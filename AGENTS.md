# Repository Guidelines

## Project Structure & Module Organization
The repository currently hosts curated corpora in data/ (e.g., data/data.txt, data/2101.03697v3.pdf). Keep raw assets there and add a README per subfolder describing provenance and preprocessing. Place production-grade agents, workflows, and utilities under src/ (create the directory if your contribution introduces the first module) using package-style layout (src/rag_ops/...). Mirror pipelines with scenario-focused notebooks under 
otebooks/ only when narrative context is required; export distilled logic back into src/. Stage evaluations inside 	ests/resources/ to separate fixtures from large source documents.

## Build, Test, and Development Commands
Use Python 3.11+. Create an environment with python -m venv .venv then .venv\\Scripts\\Activate.ps1. Install runtime and tooling via python -m pip install -r requirements-dev.txt (update the file whenever dependencies change). Run python -m pytest for the full suite and python -m pytest tests/path::TestClass::test_case for focused runs. Add uff check . and uff format before opening a PR; the repo relies on Ruff for both linting and formatting to keep diffs small.

## Coding Style & Naming Conventions
Follow PEP 8 with 4-space indentation and type hints on public functions. Organize modules by agent responsibility (etrievers.py, outers.py, etc.) and name chains or workflows with the pattern erb_noun_pipeline. Constants stay uppercase, environment variables map to settings.py using pydantic-style models when possible.

## Testing Guidelines
Author tests with pytest and structure files as 	ests/test_<module>.py. Prefer fixture-driven tests that load lightweight slices of data/ rather than entire corpora; add mocks for external services. Maintain coverage above 85% for new code and document any intentional gaps in the PR description.

## Commit & Pull Request Guidelines
History shows short imperative commits (e.g., dd data txt, ix:readme.md). Continue using present-tense subjects, optionally prefixed with a Conventional Commit type (eat:, ix:). Each PR should describe scope, list primary commands run (tests, lint), link any tracking issue, and include screenshots or logs when agent behaviour changes.

## Security & Configuration Tips
Never commit API keys or service credentials. Reference secrets via .env (already gitignored) and load them with a helper in settings.py. Compress large corpora before committing, track provenance in data/README.md, and share checksums so reviewers can verify integrity.
