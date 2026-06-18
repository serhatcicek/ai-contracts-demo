# ai-contracts-demo — Rent A Car System Contracts

This repository is the **single source of truth** for all AI agents, backend developers, and frontend developers working on the Rent A Car system.

It answers one core question: how do backend and frontend teams coordinate through AI without editing each other's codebases directly?

---

## How to use this repository

**Every agent MUST read this README first, then the relevant contract files before planning or writing any code.**

| Agent type | Must read before starting |
|---|---|
| Backend Agent | `domain/`, `architecture/backend-architecture.md`, `database/`, `models/`, `api/openapi.yaml`, `api/endpoints.md`, `governance/agent-boundaries.md` |
| Frontend Agent | `domain/`, `architecture/frontend-architecture.md`, `design/`, `api/openapi.yaml`, `api/endpoints.md`, `governance/agent-boundaries.md` |
| API Contract Owner | `api/`, `models/`, `governance/change-control.md` |
| Database Architect | `database/`, `models/`, `architecture/backend-architecture.md` |
| QA Tester | `api/`, `domain/business-rules.md`, `workflows/qa-workflow.md` |

---

## Repository structure

```
ai-contracts-demo/
├── README.md                        ← Start here (this file)
├── domain/
│   ├── rent-a-car-prd.md            ← Product requirements
│   ├── glossary.md                  ← Domain vocabulary
│   ├── business-rules.md            ← Pricing, availability, validation rules
│   └── user-roles.md                ← Who can do what
├── architecture/
│   ├── system-overview.md           ← High-level system map
│   ├── backend-architecture.md      ← Backend stack and structure
│   ├── frontend-architecture.md     ← Frontend stack and structure
│   └── integration-architecture.md ← How backend and frontend connect
├── database/
│   ├── entities.md                  ← Table definitions
│   ├── er-diagram.md                ← Entity-relationship diagram (text)
│   ├── migrations-plan.md           ← Migration sequence
│   └── seed-data.md                 ← Sample / seed data
├── api/
│   ├── openapi.yaml                 ← Authoritative API spec (OpenAPI 3.1)
│   ├── endpoints.md                 ← Human-readable endpoint summary
│   ├── request-response-examples.md ← Worked request/response pairs
│   └── error-format.md              ← Standard error envelope
├── models/
│   ├── vehicle.md
│   ├── reservation.md
│   ├── customer.md
│   ├── location.md
│   ├── pricing.md
│   └── media.md
├── design/
│   ├── design-system.md             ← Tokens, palette, typography
│   ├── page-map.md                  ← All pages and their routes
│   ├── components.md                ← Reusable UI component catalogue
│   └── frontend-rules.md           ← SEO, accessibility, performance rules
├── workflows/
│   ├── backend-workflow.md
│   ├── frontend-workflow.md
│   ├── api-change-workflow.md
│   └── qa-workflow.md
├── governance/
│   ├── repo-ownership.md
│   ├── agent-boundaries.md          ← What each agent may and may not do
│   └── change-control.md
└── templates/
    ├── story-template.md
    ├── bug-template.md
    ├── adr-template.md
    └── api-change-template.md
```

---

## Governance rules (non-negotiable)

1. Backend and frontend agents **may read** this folder freely.
2. Backend agents **must not edit** frontend source code unless explicitly approved by the Frontend Agent owner.
3. Frontend agents **must not edit** backend source code unless explicitly approved by the Backend Agent owner.
4. API changes **must first** be reflected in `api/openapi.yaml` and `api/endpoints.md`.
5. Database/model changes **must first** be reflected in `database/` and `models/`.
6. Frontend design changes **must first** be reflected in `design/`.
7. If frontend needs a backend endpoint, create a story document in `docs/stories/` instead of directly editing backend code.
8. If backend needs a frontend change, create a story document in `docs/stories/` instead of directly editing frontend code.

---

## Change flow

```
Idea / requirement
       ↓
  domain/ PRD + business-rules
       ↓
  models/ + database/ (schema first)
       ↓
  api/openapi.yaml (contract first)
       ↓
  Backend implements against contract
  Frontend implements against contract
       ↓
  QA validates against contract
```

---

## Original demo note

The `contracts/` and `requests/` directories from the original payment demo are preserved for reference. All new Rent A Car work lives in the directories listed above.
