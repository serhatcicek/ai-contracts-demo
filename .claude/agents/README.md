# Claude Code Subagents — Rent A Car System

These are Claude Code project subagents (`@agent-name`) scoped to the `ai-contracts-demo` contract repository. They enforce the contract-first discipline: no implementation code is written before the relevant contract is authored and approved.

---

## Quick reference

| Agent | When to use |
|---|---|
| `@contract-owner` | Multi-layer changes; contract conflicts; end-to-end feature authoring |
| `@domain-analyst` | New features; business rule questions; user stories; PRD updates |
| `@api-architect` | Endpoint changes; request/response shape changes; breaking API changes |
| `@database-architect` | Table/column changes; new migrations; seed data; ER diagram |
| `@design-contract-owner` | New pages; design token changes; component catalogue; frontend rules |
| `@contract-drift-auditor` | Post-sprint audits; implementation review; consistency checks |

---

## Agents in detail

### `@contract-owner`

**File:** `contract-owner.md`

The master steward of all contract documents. Use when a task crosses multiple contract layers — for example, a new feature that needs a domain rule, a database table, an API endpoint, and a new page all at once. Also use when two contract files contradict each other and a ruling is needed.

The Contract Owner is the only agent that can touch all files in `ai-contracts-demo/`. It enforces the mandatory change order:

```
domain/ → models/database/ → api/openapi.yaml → backend impl → frontend impl → QA
```

**Do not use** for narrow, single-layer tasks — use the specialist below instead.

---

### `@domain-analyst`

**File:** `domain-analyst.md`

The product expert. Owns `domain/rent-a-car-prd.md`, `domain/business-rules.md`, `domain/glossary.md`, and `domain/user-roles.md`.

Use when:
- A stakeholder asks "can we add a feature that does X?"
- A business rule is ambiguous and needs clarification before implementation.
- A new user story needs to be written in `docs/stories/`.
- You need to know what the system is *supposed* to do (not how it is built).

Backend agents: when you receive a task that references a business rule (BR-NN), this agent is the authority. If the rule is unclear or missing, ask this agent to define it first.

Frontend agents: when validation UX behavior is uncertain (e.g., "what happens if the user picks a return date before pickup date?"), this agent provides the answer from `business-rules.md`.

---

### `@api-architect`

**File:** `api-architect.md`

The API contract owner. Owns `api/openapi.yaml`, `api/endpoints.md`, `api/error-format.md`, `api/request-response-examples.md`, and `models/`.

Use when:
- Adding a new endpoint or modifying an existing one.
- Changing a request or response field name, type, or structure.
- Deprecating or removing an endpoint.
- Checking whether a field the frontend wants to consume is documented in the spec.
- Writing a breaking-change notice.

**Backend agents:** never implement an endpoint that is not in `openapi.yaml`. If you need a new endpoint, ask `@api-architect` to add it first.

**Frontend agents:** never call an endpoint not in `openapi.yaml`. If a needed endpoint is missing, create a story document requesting it — do not touch backend code.

---

### `@database-architect`

**File:** `database-architect.md`

The database schema owner. Owns `database/entities.md`, `database/er-diagram.md`, `database/migrations-plan.md`, and `database/seed-data.md`. The only agent allowed to write migration and seed files in `demo-backend/src/migrations/` and `demo-backend/src/seeds/`.

Use when:
- A new table or column is needed.
- A foreign key relationship is being added or changed.
- The migration sequence needs to be reviewed or extended.
- Seed data needs to be updated for local development.
- You want to verify that a column referenced in `api/openapi.yaml` actually exists in the database.

**Backend agents:** always check `database/entities.md` before writing queries. If you need a schema change, ask `@database-architect` to update the contract and write the migration first.

---

### `@design-contract-owner`

**File:** `design-contract-owner.md`

The frontend design contract owner. Owns `design/design-system.md`, `design/page-map.md`, `design/components.md`, and `design/frontend-rules.md`.

Use when:
- A new page needs to be added to the frontend.
- A design token (color, spacing, typography) needs to change.
- A new reusable UI component needs to be catalogued.
- You want to verify that a frontend implementation meets SEO, accessibility, or performance requirements.
- A frontend agent asks "which Tailwind colors are approved?" or "what is the canonical URL for the reservation confirmation page?"

**Frontend agents:** always check `design/page-map.md` before creating a route, and `design/design-system.md` before using a color or spacing value. If a page is not in `page-map.md`, ask `@design-contract-owner` to add it first.

---

### `@contract-drift-auditor`

**File:** `contract-drift-auditor.md`

The consistency watchdog. Read-only across all code. Produces structured drift reports in `docs/bugs/`.

Use when:
- A sprint is complete and you want to verify the implementation matches the contracts.
- A bug was reported and you want to determine if it reflects a contract violation or an implementation bug.
- You are onboarding and want to understand the gap between contracts and current state.
- You suspect the backend is returning undocumented fields, missing endpoints, or skipping business rule validation.

This agent never fixes anything — it only reports findings with severity levels (CRITICAL / HIGH / MEDIUM / LOW) and assigns each finding to the responsible owner agent. After an audit, use the relevant owner agent to fix the findings.

---

## How backend and frontend repos use these contracts

### For both repos

1. **Start every task** by reading `ai-contracts-demo/README.md`.
2. **Identify the relevant contract files** from the table in `README.md`.
3. **Plan before coding**: list files to create/modify and confirm alignment with contracts.
4. **Never implement before the contract is written.** If a contract section is missing, stop and ask the appropriate agent to author it first.

### Backend repo (`demo-backend/`)

- Check `api/openapi.yaml` before writing a route — the endpoint must exist in the spec.
- Check `database/entities.md` before writing a migration or query.
- Enforce every business rule in `domain/business-rules.md` in your controllers.
- Use the error envelope format from `api/error-format.md` for all error responses.
- If you need a frontend change: create `docs/stories/story-{date}-{name}.md`.

### Frontend repo (`demo-frontend/`)

- Check `design/page-map.md` before creating a route or template file.
- Use only colors and spacing values from `design/design-system.md`.
- Check `api/openapi.yaml` before making an API call — the endpoint must be documented.
- Implement the SEO and accessibility rules from `design/frontend-rules.md` on every page.
- If you need a new backend endpoint: create `docs/stories/story-{date}-{name}.md`.

### Cross-boundary requests

Neither backend nor frontend agents may edit each other's source code. When one side needs something from the other:

1. Create `docs/stories/story-{YYYYMMDD}-{short-name}.md` using `templates/story-template.md`.
2. Describe what is needed, why, and the acceptance criteria.
3. Tag the responsible agent and the contract files that need updating first.
