# Product Requirements Document — Rent A Car System

**Version:** 1.0  
**Status:** Draft  
**Last updated:** 2026-06-18

---

## 1. Purpose

Build a web-based Rent A Car platform that allows customers to browse vehicles, make reservations or inquiry requests, and allows admins to manage the fleet, categories, and reservations.

---

## 2. Goals

- Provide a fast, SEO-friendly public vehicle catalogue.
- Allow customers to submit reservation or inquiry requests without requiring account registration.
- Give admins a complete management panel for vehicles, categories, reservations, and customers.
- Support WhatsApp and contact CTAs to drive conversions.

---

## 3. Non-goals (v1)

- Online payment processing.
- Customer self-service account portal.
- Multi-currency pricing.
- Multi-language support (Turkish is primary for v1).

---

## 4. User roles

See `user-roles.md` for full role definitions.

| Role | Description |
|---|---|
| Guest | Anonymous visitor browsing vehicles |
| Customer | Submits a reservation or inquiry request |
| Admin | Manages fleet, categories, reservations |

---

## 5. Feature list

### 5.1 Public — Vehicle listing

- Display all available vehicles in a card grid.
- Filter by category (SUV, Sedan, Economy, etc.).
- Show vehicle name, thumbnail image, daily price, and category badge.
- Link to vehicle detail page.

### 5.2 Public — Vehicle detail page

- Full vehicle description.
- Image gallery (multiple photos).
- Daily price prominently displayed.
- Category, fuel type, transmission, seat count displayed.
- Pickup and return location selector.
- Pickup and return date pickers.
- Reservation / Inquiry request button.
- WhatsApp CTA button.

### 5.3 Public — Reservation / Inquiry form

- Customer first name, last name, email, phone.
- Selected vehicle (pre-filled from detail page).
- Pickup location, return location.
- Pickup date, return date.
- Optional notes.
- Submit → confirmation message with reference number.

### 5.4 Admin — Vehicle management

- List all vehicles with status (Available, Rented, Maintenance).
- Create / edit / soft-delete vehicles.
- Upload multiple images per vehicle.
- Set daily price, category, fuel type, transmission, seat count, description.

### 5.5 Admin — Category management

- List, create, edit, delete vehicle categories.
- Each category has a name and optional icon/image.

### 5.6 Admin — Reservation / Inquiry management

- List all reservation requests with status (Pending, Confirmed, Cancelled, Completed).
- View full request details.
- Update status.
- Add internal notes.
- Export to CSV (optional v1 stretch).

### 5.7 SEO

- Public pages must have `<title>`, `<meta description>`, and Open Graph tags.
- URLs must be human-readable (e.g. `/vehicles/ford-focus-2023`).
- Page render must not depend on client-side JS for initial content (SSR or static preferred).

---

## 6. Acceptance criteria summary

| Feature | Acceptance criteria |
|---|---|
| Vehicle listing | Loads in < 2 s; filter updates without full reload |
| Vehicle detail | All fields present; gallery works; form submits |
| Reservation form | Validates required fields; returns reference number |
| Admin vehicle | CRUD works; image upload works |
| Admin reservation | Status update persists; list is filterable |
| SEO | Lighthouse SEO score ≥ 90 on public pages |

---

## 7. Out-of-scope items (defer to v2)

- Customer login / registration.
- Payment gateway integration.
- Driver's licence upload / verification.
- Email / SMS confirmation notifications.
- Fleet GPS tracking.
