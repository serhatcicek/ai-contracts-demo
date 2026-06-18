# Repository Ownership — Rent A Car System

---

## Repository responsibilities

| Repository | Owner role | What it contains |
|---|---|---|
| `ai-contracts-demo` | API Contract Owner, Software Architect | All contracts, models, designs, workflows, governance |
| `demo-backend` | Backend Developer | Backend application source code, migrations, tests |
| `demo-frontend` | Frontend Developer | Frontend application source code, templates, assets |

---

## Who may write to what

| Role | ai-contracts-demo | demo-backend | demo-frontend |
|---|---|---|---|
| Product Analyst | ✓ (domain/) | — | — |
| Software Architect | ✓ (architecture/) | read-only | read-only |
| API Contract Owner | ✓ (api/, models/) | read-only | read-only |
| Database Architect | ✓ (database/, models/) | ✓ (migrations/) | — |
| Backend Developer | read-only | ✓ | — |
| Frontend Developer | read-only | — | ✓ |
| QA Tester | ✓ (docs/bugs/) | read-only | read-only |
| Documentation Agent | ✓ | read-only | read-only |
| Deployment Agent | read-only | ✓ (config) | ✓ (config) |

---

## Cross-boundary requests

If a Backend Developer needs a frontend change:
1. Create `docs/stories/story-{date}-{description}.md`.
2. Frontend Developer reviews and implements.
3. Do not modify `demo-frontend/` directly.

If a Frontend Developer needs a backend endpoint:
1. Create `docs/stories/story-{date}-{description}.md`.
2. API Contract Owner updates `api/openapi.yaml`.
3. Backend Developer implements.
4. Frontend Developer consumes the new endpoint.

---

## ai-contracts-demo change authority

Changes to these files require explicit cross-team approval:

| File | Approver |
|---|---|
| `api/openapi.yaml` | API Contract Owner |
| `database/entities.md` | Database Architect |
| `domain/business-rules.md` | Product Analyst + Software Architect |
| `governance/agent-boundaries.md` | Software Architect |
