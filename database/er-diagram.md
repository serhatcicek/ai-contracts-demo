# ER Diagram — Rent A Car System

Text-based entity-relationship diagram.

---

## Entities and relationships

```
┌──────────────┐       ┌──────────────┐
│  categories  │       │   locations  │
├──────────────┤       ├──────────────┤
│ id (PK)      │       │ id (PK)      │
│ name         │       │ name         │
│ slug         │       │ address      │
│ image_url    │       │ city         │
│ created_at   │       │ phone        │
│ updated_at   │       │ latitude     │
└──────┬───────┘       │ longitude    │
       │               │ is_active    │
       │ 1..N          │ created_at   │
       │               │ updated_at   │
       ▼               └──────┬───────┘
┌──────────────┐             │
│   vehicles   │             │ 1..N (pickup)
├──────────────┤             │ 1..N (return)
│ id (PK)      │             │
│ category_id  │◄────────────┘
│ name         │
│ slug         │
│ description  │
│ daily_price  │      ┌──────────────┐
│ fuel_type    │      │    media     │
│ transmission │      ├──────────────┤
│ seat_count   │      │ id (PK)      │
│ year         │◄─────│ vehicle_id   │
│ status       │      │ filename     │
│ created_at   │      │ original_name│
│ updated_at   │      │ mime_type    │
└──────┬───────┘      │ size_bytes   │
       │              │ display_order│
       │ 1..N         │ created_at   │
       │              └──────────────┘
       ▼
┌──────────────┐      ┌──────────────┐
│ reservations │      │  customers   │
├──────────────┤      ├──────────────┤
│ id (PK)      │      │ id (PK)      │
│ reference_no │      │ first_name   │
│ customer_id  │◄─────│ last_name    │
│ vehicle_id   │      │ email        │
│ pickup_loc_id│      │ phone        │
│ return_loc_id│      │ created_at   │
│ pickup_date  │      └──────────────┘
│ return_date  │
│ rental_days  │      ┌──────────────┐
│ price_snap   │      │    admins    │
│ total_price  │      ├──────────────┤
│ status       │      │ id (PK)      │
│ notes        │      │ username     │
│ admin_notes  │      │ password_hash│
│ created_at   │      │ created_at   │
│ updated_at   │      │ last_login_at│
└──────────────┘      └──────────────┘
```

---

## Cardinality summary

| Relationship | Type |
|---|---|
| categories → vehicles | One-to-Many |
| vehicles → media | One-to-Many |
| vehicles → reservations | One-to-Many |
| customers → reservations | One-to-Many |
| locations → reservations (pickup) | One-to-Many |
| locations → reservations (return) | One-to-Many |

---

## Key constraints

- `vehicles.category_id` — NOT NULL; a vehicle must belong to a category.
- `reservations.vehicle_id` — NOT NULL; every reservation references a vehicle.
- `reservations.customer_id` — NOT NULL; every reservation references a customer.
- `reservations.pickup_location_id` — NOT NULL.
- `reservations.return_location_id` — NOT NULL (defaults to pickup if not specified by user).
- `media.vehicle_id` — NOT NULL with CASCADE DELETE.
