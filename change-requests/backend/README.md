# Backend Change Requests

This directory holds formal backend change requests raised by frontend agents when a required API endpoint, field, response shape, or API behavior is missing from the documented contract.

---

## When to create a file here

A frontend agent must create a file here — and stop all frontend implementation — when:

- A required endpoint is absent from `../api/openapi.yaml` or `../api/endpoints.md`.
- A required response field is absent from `../models/*.md` or `../api/openapi.yaml`.
- The documented response shape does not match what the frontend page needs.
- A required query parameter, path parameter, or request body field is undocumented.

**Do not** edit backend source code. **Do not** invent the endpoint. **Do not** continue frontend implementation until the backend agent has implemented the change and the API Contract Owner has updated `../api/openapi.yaml`.

---

## Filename format

```
BR-YYYYMMDD-short-description.md
```

Examples:
- `BR-20260618-vehicle-slug-endpoint.md`
- `BR-20260618-reservation-status-field.md`

---

## Required file contents

Every backend change request must contain all sections below. Incomplete requests will not be actioned.

```markdown
# BR-YYYYMMDD — {Short title}

## Frontend need
{What the frontend page or component requires and why it cannot proceed without this change.}

## Page / component
{Which page (from design/page-map.md) or component (from design/components.md) is blocked.}

## Required endpoint
{HTTP method + path, e.g. GET /api/v1/vehicles/:slug}

## Required request parameters
{List all query params, path params, and request body fields with types.}
| Parameter | In | Type | Required | Description |
|---|---|---|---|---|
| slug | path | string | yes | URL-friendly vehicle identifier |

## Required response fields
{List all fields the frontend needs, with types. Map to existing model files where possible.}
| Field | Type | Source model | Description |
|---|---|---|---|
| data.slug | string | models/vehicle.md | URL slug |

## Why existing contract is insufficient
{Explain which part of openapi.yaml or endpoints.md is missing or wrong, and why the frontend cannot use what is already there.}

## Acceptance criteria
- [ ] Endpoint exists in `../api/openapi.yaml` with the documented path, method, and response shape.
- [ ] Response fields listed above are present and correctly typed.
- [ ] Endpoint is listed in `../api/endpoints.md`.
- [ ] At least one worked example added to `../api/request-response-examples.md`.

## Suggested priority
Low / Medium / High / Critical

## Raised by
Frontend agent — {agent name} — {date}
```

---

## After the backend implements the change

1. The API Contract Owner updates `../api/openapi.yaml` and `../api/endpoints.md`.
2. The frontend agent re-reads the updated contract.
3. The frontend agent proceeds with implementation.
4. Mark this file resolved by adding `**Status: Resolved — {date}**` at the top.
