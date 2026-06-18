# Agent Boundaries — Rent A Car System

This document defines exactly what each AI agent may and may not do. All agents must read this file before starting work.

---

## Universal rules (all agents)

1. Always read `ai-contracts-demo/README.md` before starting any task.
2. Always read the relevant contract files before planning or writing code.
3. Never modify application source code without a written plan listing the exact files to be changed.
4. If uncertain about a boundary, stop and raise a question rather than guessing.

---

## Backend Agent

**May:**
- Read all files in `ai-contracts-demo/`.
- Write to `demo-backend/src/`, `demo-backend/src/migrations/`, `demo-backend/src/seeds/`, `demo-backend/package.json`.
- Run backend tests.
- Update `ai-contracts-demo/database/migrations-plan.md` to register new migrations.

**Must not:**
- Modify any file under `demo-frontend/`.
- Add endpoints not defined in `api/openapi.yaml`.
- Change the API response shape without updating `api/openapi.yaml` first.
- Change the error envelope format without updating `api/error-format.md` first.

---

## Frontend Agent

**May:**
- Read all files in `ai-contracts-demo/`.
- Write to `demo-frontend/src/`, `demo-frontend/public/`, `demo-frontend/package.json`.
- Call API endpoints defined in `api/openapi.yaml`.

**Must not:**
- Modify any file under `demo-backend/`.
- Call endpoints that are not in `api/openapi.yaml`.
- Hardcode backend URLs, phone numbers, or secrets.
- Change the design system without updating `ai-contracts-demo/design/design-system.md` first.
- Add new pages without updating `ai-contracts-demo/design/page-map.md` first.

---

## API Contract Owner Agent

**May:**
- Update `ai-contracts-demo/api/openapi.yaml`.
- Update `ai-contracts-demo/api/endpoints.md`.
- Update `ai-contracts-demo/api/request-response-examples.md`.
- Update `ai-contracts-demo/api/error-format.md`.
- Update `ai-contracts-demo/models/`.

**Must not:**
- Modify `demo-backend/` or `demo-frontend/` source code.
- Change `database/entities.md` without coordinating with the Database Architect.

---

## Database Architect Agent

**May:**
- Update `ai-contracts-demo/database/entities.md`.
- Update `ai-contracts-demo/database/er-diagram.md`.
- Update `ai-contracts-demo/database/migrations-plan.md`.
- Update `ai-contracts-demo/database/seed-data.md`.
- Write migration files in `demo-backend/src/migrations/`.
- Write seed files in `demo-backend/src/seeds/`.

**Must not:**
- Modify business logic in `demo-backend/src/controllers/` or `demo-backend/src/routes/`.
- Modify `demo-frontend/`.
- Change the API schema in `api/openapi.yaml` without coordinating with the API Contract Owner.

---

## QA Tester Agent

**May:**
- Read all files in `ai-contracts-demo/`.
- Write bug reports to `docs/bugs/`.
- Run tests.
- Access both backend and frontend to test behavior.

**Must not:**
- Modify application source code.
- Modify contract files.

---

## Documentation Agent

**May:**
- Update any file in `ai-contracts-demo/`.
- Create or update files in `docs/`.

**Must not:**
- Modify application source code in `demo-backend/` or `demo-frontend/`.

---

## Product Analyst Agent

**May:**
- Update `ai-contracts-demo/domain/` files.
- Create story documents in `docs/stories/`.

**Must not:**
- Modify application source code.
- Modify `api/`, `database/`, `models/`, or `design/` without coordinating with the relevant owner.

---

## Story/RFC process (cross-boundary requests)

When one agent needs work done by another agent:

1. Create `docs/stories/story-{YYYYMMDD}-{short-name}.md` using `templates/story-template.md`.
2. Describe: what is needed, why, acceptance criteria, which agent should pick it up.
3. Do not directly modify the other agent's codebase.
