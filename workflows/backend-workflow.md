# Backend Workflow — Rent A Car System

This is the required workflow for all backend agents and developers. Do not skip steps.

---

## Before writing any code

1. Read `ai-contracts-demo/README.md`.
2. Read `ai-contracts-demo/domain/rent-a-car-prd.md` and `domain/business-rules.md`.
3. Read `ai-contracts-demo/api/openapi.yaml` — this is the contract you must implement against.
4. Read `ai-contracts-demo/database/entities.md` and the relevant model file in `ai-contracts-demo/models/`.
5. Read `ai-contracts-demo/architecture/backend-architecture.md`.
6. Read `ai-contracts-demo/governance/agent-boundaries.md`.

---

## Adding a new feature

1. Confirm the feature exists in `domain/rent-a-car-prd.md`. If not, raise it as a story first.
2. Check `api/openapi.yaml` — is the required endpoint already defined?
   - **Yes:** implement it.
   - **No:** follow the API Change Workflow (`workflows/api-change-workflow.md`) first.
3. Check `database/entities.md` — does the required table/column exist?
   - **No:** update `database/entities.md` and `models/{model}.md` first, then write the migration.
4. Write the migration file in `demo-backend/src/migrations/`.
5. Implement the route, controller, and model query in `demo-backend/src/`.
6. Write tests in `demo-backend/src/__tests__/`.
7. Run tests: `npm test`.
8. Update `database/migrations-plan.md` with the new migration entry.

---

## Fixing a bug

1. Read the bug report (from `docs/bugs/` or equivalent).
2. Identify which contract files are relevant.
3. Write a failing test that reproduces the bug.
4. Fix the bug.
5. Confirm the test passes.
6. Do **not** change the API contract unless the contract itself was wrong — if so, follow the API Change Workflow.

---

## Code review checklist (self-review before done)

- [ ] All business rules from `domain/business-rules.md` are respected.
- [ ] API response shape exactly matches `api/openapi.yaml`.
- [ ] Error responses use the format in `api/error-format.md`.
- [ ] No frontend source files modified.
- [ ] No breaking changes to existing endpoints without updating `api/openapi.yaml` first.
- [ ] Migration file added if schema changed.
- [ ] Tests added or updated.

---

## Forbidden actions

- Do not edit any file under `demo-frontend/` without explicit approval.
- Do not add endpoints that are not in `api/openapi.yaml`.
- Do not change the error envelope format without updating `api/error-format.md` first.
