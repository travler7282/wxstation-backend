# AGENTS-IMPROVEMENT-SPEC.md

Audit of agent-guidance quality for `wxstation-backend`.
Date: 2026-05-01

---

## Current State

| Artifact | Status |
|---|---|
| `AGENTS.md` | ✅ Present and aligned to standalone backend |
| `.github/copilot-instructions.md` | ✅ Thin adapter points to `AGENTS.md` |
| `.claude/CLAUDE.md` | ✅ Thin adapter points to `AGENTS.md` |
| `README.md` | ✅ Uses `.venv`-first local workflow |
| `.github/pull_request_template.md` | ✅ Updated for Python backend validation |

---

## Key Fixes Completed

1. Removed monorepo-specific guidance from `AGENTS.md`.
2. Replaced workspace/frontend/backend matrix with standalone backend scope.
3. Updated command examples to use root `.venv` workflow.
4. Updated CI documentation to match current image build/push workflows.
5. Removed stale references to unrelated services and apps.

---

## Remaining Recommendations

1. Keep adapter files minimal and avoid policy duplication.
2. If branch strategy changes, update both `AGENTS.md` and PR templates together.
3. Add API contract notes if response schemas become non-mock or backward compatibility becomes strict.

---

## Priority

| Priority | Item | Effort |
|---|---|---|
| P1 | Keep docs in sync with CI workflow edits | 10 min per workflow change |
| P2 | Add endpoint compatibility/versioning notes if API evolves | 20-30 min |
