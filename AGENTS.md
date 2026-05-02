# AGENTS.md — Agent Instructions for wxstation-backend

This file defines repository-specific guidance for AI coding agents.

## Repository Scope

This repository is a standalone Python FastAPI backend for WXStation.

Key paths:
- `main.py` — FastAPI app and API routes
- `tests/` — pytest test suite
- `requirements.txt` — Python dependencies
- `pyproject.toml` — project metadata and version
- `.github/workflows/deploy_dev.yml` — dev image pipeline
- `.github/workflows/deploy_prod.yml` — prod image pipeline
- `infrastructure/k8s/` — Kubernetes manifests maintained by owner

## Runtime and Tooling

- Python: 3.11+ (CI uses Python 3.11)
- Framework: FastAPI + Uvicorn
- Testing: pytest + pytest-cov
- Packaging: pip with `requirements.txt`
- Local environment: `.venv` in repository root

## Common Commands

Run from repository root.

```bash
# Create and use a virtual environment (Windows)
python -m venv .venv
.venv/Scripts/python.exe -m pip install -r requirements.txt

# Run tests
.venv/Scripts/python.exe -m pytest

# Run app (dev)
.venv/Scripts/python.exe -m uvicorn main:app --reload --host 0.0.0.0 --port 8001

# Run app (prod-like)
.venv/Scripts/python.exe -m uvicorn main:app --host 0.0.0.0 --port 8001
```

## CI/CD Behavior

- `deploy_dev.yml` triggers on push to `dev`.
- `deploy_prod.yml` triggers on push to `main`.
- Both workflows:
  - create a venv
  - install dependencies
  - run tests
  - build and push Docker image `docker.io/travler7282/wxstation`
- Version tags are read from root `pyproject.toml`.

Required GitHub secrets:
- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

## Versioning Policy

Bump version in `pyproject.toml` for release-impacting changes.

- Patch (`x.y.Z`): bug fixes, docs-only behavior clarifications, non-breaking fixes.
- Minor (`x.Y.z`): backward-compatible endpoint additions or features.
- Major (`X.y.z`): breaking API changes.

## Code Conventions

- Keep Python code typed (function signatures and return types where practical).
- Keep endpoint paths under `/wxstation/api/v1`.
- Preserve `/healthz` and `/readyz` aliases used for health checks.
- Do not hardcode secrets in code, tests, or docs.

## Guardrails

- Do not modify Kubernetes manifests under `infrastructure/k8s/` unless explicitly requested.
- Do not change Docker image names/tags in workflows without explicit request.
- Do not commit build outputs, virtual environments, or credentials.
- Do not commit directly to `main` or `dev`; use feature branches and PRs.

## Adapter Strategy

Keep tool-specific instruction files minimal and point back to this file.

- `.github/copilot-instructions.md`
- `.claude/CLAUDE.md`

Update this file first, then adapter files in the same commit when policy changes.
