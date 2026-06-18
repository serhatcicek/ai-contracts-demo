# Model: Pricing

Pricing is not a separate database table. It is defined as `daily_price` on the `vehicles` table and computed at reservation time.

---

## Price fields

| Field | Table | Type | Notes |
|---|---|---|---|
| `vehicles.daily_price` | vehicles | DECIMAL(10,2) | Per-day rental price in TRY |
| `reservations.daily_price_snapshot` | reservations | DECIMAL(10,2) | Copied from vehicle at reservation time |
| `reservations.rental_days` | reservations | INTEGER | Computed: return_date − pickup_date |
| `reservations.total_price` | reservations | DECIMAL(10,2) | daily_price_snapshot × rental_days |

---

## Calculation rules

See `domain/business-rules.md` PR-01 to PR-05.

```
rental_days   = (return_date - pickup_date) as full calendar days
total_price   = daily_price_snapshot × rental_days
```

Example:
- `pickup_date = 2026-07-01`
- `return_date = 2026-07-05`
- `rental_days = 4`
- `daily_price = 1800.00`
- `total_price = 7200.00`

---

## Snapshot rule

`daily_price_snapshot` is captured from `vehicles.daily_price` at the moment the reservation is submitted. If the vehicle's `daily_price` changes later, existing reservations are not affected. This is enforced by copying the value during reservation creation, not by reference.

---

## Currency

- All prices are in Turkish Lira (TRY) in v1.
- Prices are stored and displayed without VAT in v1.
- Multi-currency support is a v2 item.

---

## Display format

- Turkish locale: `1.800,00 ₺`
- Frontend must format using `Intl.NumberFormat('tr-TR', { style: 'currency', currency: 'TRY' })`.
