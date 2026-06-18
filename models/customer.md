# Model: Customer

**Table:** `customers`  
**Source of truth for schema:** `database/entities.md`

---

## Fields

| Field | Type | Notes |
|---|---|---|
| `id` | integer | Auto-increment primary key |
| `first_name` | string | Required |
| `last_name` | string | Required |
| `email` | string | Required, valid email format |
| `phone` | string | Required |
| `created_at` | timestamp | |

---

## Notes

- Customers do not have accounts or passwords in v1.
- A new customer record is created each time a reservation is submitted.
- The same person may appear multiple times if they submit multiple reservations (no deduplication in v1).
- `email` is not unique in the table; duplicates are allowed.
- Admin can view all customers indirectly via reservation detail.

---

## Privacy considerations

- Customer PII (name, email, phone) is stored in the database.
- Admin notes on reservations must not contain sensitive data beyond operational notes.
- Future versions should add a KVKK/GDPR compliance layer.

---

## API endpoints

Customers are not exposed as a standalone endpoint in v1. Customer data is submitted as part of `POST /api/v1/reservations` and read back as part of reservation detail in the admin panel.
