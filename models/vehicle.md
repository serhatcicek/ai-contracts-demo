# Model: Vehicle

**Table:** `vehicles`  
**Source of truth for schema:** `database/entities.md`

---

## Fields

| Field | Type | Notes |
|---|---|---|
| `id` | integer | Auto-increment primary key |
| `category_id` | integer | FK → categories |
| `name` | string | Display name e.g. "Ford Focus 2023" |
| `slug` | string | URL-safe unique identifier |
| `description` | string\|null | Full marketing description |
| `daily_price` | decimal | Per-day price in TRY |
| `fuel_type` | enum | `petrol` \| `diesel` \| `hybrid` \| `electric` |
| `transmission` | enum | `manual` \| `automatic` |
| `seat_count` | integer | 2–9 |
| `year` | integer\|null | Manufacturing year |
| `status` | enum | `available` \| `rented` \| `maintenance` \| `inactive` |
| `created_at` | timestamp | |
| `updated_at` | timestamp | |

---

## Computed / joined fields (API response only)

| Field | Source |
|---|---|
| `category` | Joined from `categories` table |
| `primary_image_url` | First media item (display_order = 0) URL |
| `media` | Array of all media items (detail endpoint only) |

---

## Status lifecycle

```
[new] → available
available → rented         (when reservation confirmed)
available → maintenance
rented → available         (when reservation completed)
rented → maintenance
maintenance → available
any → inactive             (soft delete)
```

---

## Business rules

- See `domain/business-rules.md` VR-01 to VR-06.
- `slug` is auto-generated from `name` (lowercased, spaces to hyphens, year appended). Must be unique.
- A vehicle must have at least one image before status can be set to `available` (VR-02).
- Soft-delete sets `status = inactive` — do not hard-delete.

---

## Slug generation example

Input: `name = "Ford Kuga 2023"`  
Slug: `ford-kuga-2023`

If slug already exists, append `-2`, `-3`, etc.

---

## API endpoints

See `api/endpoints.md` — Vehicles section.
