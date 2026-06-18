# Change Control — Rent A Car System

Rules for making controlled changes to contracts and application code.

---

## Change types

| Type | Document first? | Approval needed? | Notify? |
|---|---|---|---|
| New domain requirement | PRD update | Product Analyst | All agents |
| API endpoint change | `api/openapi.yaml` | API Contract Owner | Backend + Frontend |
| Database schema change | `database/entities.md` | Database Architect | Backend |
| New UI page | `design/page-map.md` | Frontend team | — |
| Design token change | `design/design-system.md` | Frontend team | — |
| New business rule | `domain/business-rules.md` | Product Analyst | Backend + QA |
| Bug fix (no API change) | Bug report in `docs/bugs/` | — | — |
| Bug fix (API change) | Bug report + `api/openapi.yaml` update | API Contract Owner | Frontend |

---

## Contract file change order

Changes that touch multiple layers must follow this order:

```
1. domain/ (requirements first)
2. models/ + database/ (schema)
3. api/openapi.yaml (contract)
4. demo-backend/ (implementation)
5. demo-frontend/ (consumer)
6. QA validation
```

Never implement before the contract is written.

---

## Breaking change policy

A breaking API change requires:
1. Written notice in `docs/api-changes/api-change-{date}-{name}.md`.
2. `api/openapi.yaml` updated.
3. Backend and frontend updated in a coordinated sequence (backend first, then frontend).
4. QA validates both sides before marking complete.

---

## Rollback policy

If a change causes production issues:
1. Revert to the previous version of `api/openapi.yaml`.
2. Revert the backend implementation.
3. Revert the frontend implementation.
4. Write a post-mortem note in `docs/incidents/`.

---

## Documentation-only changes

Changes that only update `ai-contracts-demo/` (no application code) can be made freely by the relevant role owner. They do not require a formal change document unless they change a breaking contract (API schema, database schema, business rules).
