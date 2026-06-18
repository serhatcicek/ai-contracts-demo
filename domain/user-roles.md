# User Roles — Rent A Car System

---

## Guest

**Who:** Any anonymous visitor.

**Can:**
- Browse the public vehicle listing.
- Filter vehicles by category.
- View vehicle detail pages.
- Click WhatsApp / contact CTAs.

**Cannot:**
- Submit a reservation (must provide contact info → becomes a Customer).
- Access the admin panel.

---

## Customer

**Who:** A person who fills in the reservation / inquiry form.

**How they are identified:** By email address + phone number. No account or password in v1.

**Can:**
- Submit a reservation request.
- Receive a reference number.

**Cannot:**
- Cancel or modify their reservation online in v1.
- Log in or view their reservation history online in v1.

---

## Admin

**Who:** A staff member of the rental company.

**How they are identified:** Username + password (session-based auth in v1).

**Can:**
- Create, edit, soft-delete vehicles.
- Upload / reorder vehicle images.
- Manage vehicle categories.
- View all reservation requests.
- Update reservation status (Pending → Confirmed → Completed or Cancelled).
- Add internal notes to reservations.
- Manage pickup / return locations.

**Cannot:**
- Impersonate customers.
- Process online payments (v1 out of scope).

---

## Role matrix

| Action | Guest | Customer | Admin |
|---|---|---|---|
| View vehicle listing | ✓ | ✓ | ✓ |
| View vehicle detail | ✓ | ✓ | ✓ |
| Submit reservation | — | ✓ | ✓ |
| View reservation list | — | — | ✓ |
| Update reservation status | — | — | ✓ |
| Create / edit vehicle | — | — | ✓ |
| Upload vehicle image | — | — | ✓ |
| Manage categories | — | — | ✓ |
| Manage locations | — | — | ✓ |
| Access admin panel | — | — | ✓ |
