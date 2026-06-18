# Error Format — Rent A Car API

All error responses from the API use this standard envelope. Backend must always return this shape for non-2xx responses.

---

## Standard error envelope

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable description",
    "details": []
  }
}
```

The `details` array is optional. It is included for validation errors to list per-field issues.

---

## Error codes

| HTTP Status | Code | When used |
|---|---|---|
| 400 | `BAD_REQUEST` | Malformed JSON body |
| 401 | `UNAUTHORIZED` | No session / invalid credentials |
| 403 | `FORBIDDEN` | Authenticated but not permitted |
| 404 | `NOT_FOUND` | Resource does not exist |
| 409 | `CONFLICT` | Delete of a referenced resource; duplicate unique value |
| 422 | `VALIDATION_ERROR` | Request body fails validation rules |
| 500 | `INTERNAL_ERROR` | Unexpected server error |

---

## Validation error detail

When `code` is `VALIDATION_ERROR`, the `details` array contains per-field errors:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      {
        "field": "pickup_date",
        "message": "Pickup date must be today or in the future"
      },
      {
        "field": "email",
        "message": "Must be a valid email address"
      }
    ]
  }
}
```

---

## Not found example

```json
{
  "success": false,
  "error": {
    "code": "NOT_FOUND",
    "message": "Vehicle not found"
  }
}
```

---

## Unauthorized example

```json
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Authentication required"
  }
}
```

---

## Implementation note

The `errorHandler` middleware in `demo-backend/src/middleware/errorHandler.js` is responsible for formatting all errors into this envelope. Route handlers and controllers should throw or call `next(err)` rather than formatting error responses themselves.

Never expose stack traces in the `error` object in production. In development, stack traces may be included under a `stack` key for debugging.
