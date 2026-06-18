# Page Map — Rent A Car System

All pages and their routes. Frontend agent must implement all pages listed here.

---

## Public pages (no auth required)

| Route | Template | Title | Description |
|---|---|---|---|
| `/` | `views/home.ejs` | Ana Sayfa | Hero section + featured vehicles + category filter |
| `/vehicles` | `views/vehicles/listing.ejs` | Araç Listesi | Full vehicle listing with category filter |
| `/vehicles/:slug` | `views/vehicles/detail.ejs` | {Vehicle Name} - Kiralık Araç | Vehicle detail + image gallery + reservation form |
| `/reservations/new` | `views/reservation/form.ejs` | Rezervasyon Yap | Standalone reservation form (if accessed directly) |
| `/reservations/confirm` | `views/reservation/confirm.ejs` | Rezervasyon Alındı | Confirmation page with reference number |
| `/contact` | `views/contact.ejs` | İletişim | Contact info + WhatsApp CTA |

---

## Admin pages (session required)

| Route | Template | Title | Description |
|---|---|---|---|
| `/admin/login` | `views/admin/login.ejs` | Admin Giriş | Login form |
| `/admin` | `views/admin/dashboard.ejs` | Dashboard | Summary stats: vehicle count, pending reservations |
| `/admin/vehicles` | `views/admin/vehicles/list.ejs` | Araçlar | Vehicle list table with search and filter |
| `/admin/vehicles/new` | `views/admin/vehicles/form.ejs` | Yeni Araç | Create vehicle form + image upload |
| `/admin/vehicles/:id/edit` | `views/admin/vehicles/form.ejs` | Araç Düzenle | Edit vehicle form + image management |
| `/admin/categories` | `views/admin/categories/list.ejs` | Kategoriler | Category list + CRUD |
| `/admin/reservations` | `views/admin/reservations/list.ejs` | Rezervasyonlar | Reservation list with status filter |
| `/admin/reservations/:id` | `views/admin/reservations/detail.ejs` | Rezervasyon Detay | Full reservation detail + status update |
| `/admin/locations` | `views/admin/locations/list.ejs` | Şubeler | Location list + CRUD |

---

## HTTP redirects

| From | To | Condition |
|---|---|---|
| `/admin` (unauthenticated) | `/admin/login` | No valid session |
| `/admin/login` (authenticated) | `/admin` | Already logged in |
| `/reservations` | `/vehicles` | GET request (form is on detail page) |

---

## 404 page

| Route | Template |
|---|---|
| `*` (unmatched) | `views/404.ejs` |

---

## Page data requirements

| Page | Data fetched from backend |
|---|---|
| `/` | `GET /api/v1/vehicles?limit=6`, `GET /api/v1/categories` |
| `/vehicles` | `GET /api/v1/vehicles?...`, `GET /api/v1/categories` |
| `/vehicles/:slug` | `GET /api/v1/vehicles/:slug`, `GET /api/v1/locations` |
| `/admin/vehicles` | `GET /api/v1/admin/vehicles`, `GET /api/v1/admin/categories` |
| `/admin/reservations` | `GET /api/v1/admin/reservations` |
| `/admin/reservations/:id` | `GET /api/v1/admin/reservations/:id` |
