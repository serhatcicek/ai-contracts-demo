# Model: Reservation

**Table:** `reservations`  
**Source of truth for schema:** `database/entities.md`

---

## Fields

| Field | Type | Notes |
|---|---|---|
| `id` | integer | Auto-increment primary key |
| `reference_number` | string | Unique, format: `RAC-YYYYMMDD-NNNN` |
| `customer_id` | integer | FK → customers |
| `vehicle_id` | integer | FK → vehicles |
| `pickup_location_id` | integer | FK → locations |
| `return_location_id` | integer | FK → locations |
| `pickup_date` | date | |
| `return_date` | date | |
| `rental_days` | integer | Computed: `return_date - pickup_date` in days |
| `daily_price_snapshot` | decimal | Copied from vehicle at time of submission |
| `total_price` | decimal | `daily_price_snapshot × rental_days` |
| `status` | enum | `pending` \| `confirmed` \| `cancelled` \| `completed` |
| `notes` | string\|null | Customer-submitted notes |
| `admin_notes` | string\|null | Internal admin notes (not visible to customer) |
| `created_at` | timestamp | |
| `updated_at` | timestamp | |

---

## Status lifecycle

```
[submitted] → pending
pending → confirmed    (Admin confirms)
pending → cancelled    (Admin cancels)
confirmed → completed  (Rental period ends)
confirmed → cancelled  (Admin or customer cancels)
```

---

## Reference number format

`RAC-YYYYMMDD-NNNN`

- `YYYYMMDD` = date of submission (UTC)
- `NNNN` = zero-padded daily sequence starting at 0001

Example: `RAC-20260618-0042`

---

## Business rules

See `domain/business-rules.md` BR-01 to BR-10.

Key rules:
- `pickup_date` must not be in the past (BR-01).
- `return_date` must be after `pickup_date` (BR-02).
- Minimum 1 day (BR-03), maximum 90 days (BR-04).
- Vehicle must be `available` status (BR-05).
- `daily_price_snapshot` is captured at submission time and never changes retroactively (PR-05).

---

## API endpoints

See `api/endpoints.md` — Reservations section.
