# API Endpoints — Rent A Car System

Human-readable summary of all endpoints. Authoritative spec is `openapi.yaml`.

Base URL: `http://localhost:3001/api/v1` (dev)

---

## Public endpoints (no auth required)

### Vehicles

| Method | Path | Description |
|---|---|---|
| `GET` | `/vehicles` | List available vehicles. Filter: `?category_slug=suv`. Paginated. |
| `GET` | `/vehicles/:slug` | Get full vehicle detail including media array. |

### Categories

| Method | Path | Description |
|---|---|---|
| `GET` | `/categories` | List all categories with vehicle count. |

### Locations

| Method | Path | Description |
|---|---|---|
| `GET` | `/locations` | List all active pickup/return locations. |

### Reservations

| Method | Path | Description |
|---|---|---|
| `POST` | `/reservations` | Submit a reservation request. Returns reference number. |

---

## Admin endpoints (session cookie required)

### Auth

| Method | Path | Description |
|---|---|---|
| `POST` | `/admin/login` | Login with username + password. Sets session cookie. |
| `DELETE` | `/admin/logout` | Destroy session. |

### Vehicles (admin)

| Method | Path | Description |
|---|---|---|
| `GET` | `/admin/vehicles` | List all vehicles (all statuses). |
| `POST` | `/admin/vehicles` | Create a new vehicle. |
| `PUT` | `/admin/vehicles/:id` | Update vehicle fields. |
| `DELETE` | `/admin/vehicles/:id` | Soft-delete (sets status to inactive). |

### Media (admin)

| Method | Path | Description |
|---|---|---|
| `POST` | `/admin/vehicles/:id/media` | Upload one or more images (multipart). |
| `DELETE` | `/admin/vehicles/:id/media/:mediaId` | Delete a specific image. |

### Categories (admin)

| Method | Path | Description |
|---|---|---|
| `GET` | `/admin/categories` | List categories. |
| `POST` | `/admin/categories` | Create category. |
| `PUT` | `/admin/categories/:id` | Update category. |
| `DELETE` | `/admin/categories/:id` | Delete category (fails if vehicles exist). |

### Reservations (admin)

| Method | Path | Description |
|---|---|---|
| `GET` | `/admin/reservations` | List all reservations. Filter: `?status=pending`. Paginated. |
| `GET` | `/admin/reservations/:id` | Get full reservation detail. |
| `PUT` | `/admin/reservations/:id` | Update status and/or admin notes. |

### Locations (admin)

| Method | Path | Description |
|---|---|---|
| `GET` | `/admin/locations` | List all locations (including inactive). |
| `POST` | `/admin/locations` | Create a location. |
| `PUT` | `/admin/locations/:id` | Update a location. |
| `DELETE` | `/admin/locations/:id` | Deactivate a location. |

---

## Standard response envelope

All responses follow the format:

```json
{
  "success": true,
  "data": { ... }
}
```

or for lists:

```json
{
  "success": true,
  "data": [ ... ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 45,
    "total_pages": 3
  }
}
```

Errors follow the format in `error-format.md`.

---

## HTTP status codes used

| Code | Meaning |
|---|---|
| 200 | OK |
| 201 | Created |
| 204 | No Content (delete/logout) |
| 400 | Bad Request (malformed JSON) |
| 401 | Unauthorized (missing/invalid session) |
| 404 | Not Found |
| 409 | Conflict (e.g. delete category with vehicles) |
| 422 | Unprocessable Entity (validation error) |
| 500 | Internal Server Error |
