# API Change Workflow — Rent A Car System

Any change to the API (new endpoint, changed request/response shape, new field, removed field, changed status code) must follow this workflow. No exceptions.

---

## Why this exists

Backend and frontend agents read `api/openapi.yaml` as their shared truth. If one side changes the API without updating the contract, the other side breaks silently.

---

## Workflow steps

### Step 1 — Create an API change document

Copy `templates/api-change-template.md` to `docs/api-changes/api-change-{date}-{name}.md`.

Fill in:
- What is changing and why.
- The new/updated endpoint definition (method, path, request body, response body).
- Which consumers are affected (frontend pages / admin features).
- Breaking or non-breaking classification.

### Step 2 — Update `api/openapi.yaml`

Update the relevant path, schema, or component in `api/openapi.yaml`.

**This file is the contract. Update it before writing any implementation code.**

### Step 3 — Update `api/endpoints.md`

Add or update the human-readable endpoint summary row.

### Step 4 — Update `api/request-response-examples.md` (if helpful)

Add an example for the new/changed endpoint.

### Step 5 — Implement on the backend

Backend Developer implements the endpoint in `demo-backend/` against the updated contract.

### Step 6 — Update the frontend

Frontend Developer updates `demo-frontend/` to consume the new/changed endpoint.

### Step 7 — QA validation

QA Tester validates the implemented endpoint against `api/openapi.yaml`.

---

## Breaking vs non-breaking changes

| Change type | Breaking? | Notes |
|---|---|---|
| New optional field in response | No | Frontend can ignore |
| New required field in request body | **Yes** | Frontend must send it |
| Removed field from response | **Yes** | Frontend may rely on it |
| Changed field name | **Yes** | Must coordinate both sides |
| New endpoint (additive) | No | Frontend may adopt at its own pace |
| Removed endpoint | **Yes** | Frontend must stop calling it |
| Changed HTTP status code | **Yes** | Frontend error handling may be affected |

---

## Hotfix exception

If a breaking bug requires an immediate backend fix that changes the API, the Backend Developer must update `api/openapi.yaml` **simultaneously** (in the same commit or PR) and notify the Frontend Developer immediately.

---

## Forbidden

- Implementing an endpoint that is not in `api/openapi.yaml`.
- Returning a response shape that differs from `api/openapi.yaml`.
- Changing an endpoint without updating `api/openapi.yaml` first.
