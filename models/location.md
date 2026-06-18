# Model: Location

**Table:** `locations`  
**Source of truth for schema:** `database/entities.md`

---

## Fields

| Field | Type | Notes |
|---|---|---|
| `id` | integer | Auto-increment primary key |
| `name` | string | Branch name e.g. "İstanbul Havalimanı Şubesi" |
| `address` | string | Full street address |
| `city` | string | City name |
| `phone` | string\|null | Branch contact phone |
| `latitude` | decimal\|null | GPS latitude (10,8) |
| `longitude` | decimal\|null | GPS longitude (11,8) |
| `is_active` | boolean | Inactive locations are hidden from public dropdowns |
| `created_at` | timestamp | |
| `updated_at` | timestamp | |

---

## Business rules

- A reservation must have a `pickup_location_id` (LR-01).
- `return_location_id` defaults to `pickup_location_id` if not specified by the user (LR-02).
- Only active locations (`is_active = true`) appear in the public location dropdown.
- Deactivating a location does not affect existing reservations.

---

## Usage in reservations

The `reservations` table has two location foreign keys:
- `pickup_location_id` — where customer collects the car.
- `return_location_id` — where customer returns the car.

These may be the same location (most common in v1).

---

## API endpoints

See `api/endpoints.md` — Locations section.
