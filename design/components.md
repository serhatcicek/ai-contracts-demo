# UI Component Catalogue — Rent A Car System

Reusable components used across pages. Frontend agent must follow these specifications.

---

## VehicleCard

Used on: home page, vehicle listing.

**Props:**
- `vehicle.name`
- `vehicle.slug`
- `vehicle.daily_price`
- `vehicle.primary_image_url`
- `vehicle.fuel_type`
- `vehicle.transmission`
- `vehicle.seat_count`
- `vehicle.category.name`

**Layout:**
```
┌─────────────────────────────┐
│  [vehicle image - 16:9]     │
├─────────────────────────────┤
│  [Category badge]           │
│  Ford Kuga 2023             │
│  ⛽ Dizel  ⚙ Otomatik  👥 5 │
│  ──────────────────────     │
│  1.800 ₺ / gün              │
│  [Detayları Gör →]          │
└─────────────────────────────┘
```

**Behavior:** entire card is a link to `/vehicles/:slug`.

---

## CategoryFilterBar

Used on: vehicle listing page.

**Props:**
- `categories[]` — array of category objects
- `activeSlug` — currently selected category slug (null = all)

**Layout:** Horizontal scrollable pill buttons. "Tümü" pill is always first.

**Behavior:** Clicking a pill filters the vehicle list. Uses `?category_slug=` query param (triggers SSR re-render or client-side AJAX).

---

## VehicleGallery

Used on: vehicle detail page.

**Props:**
- `media[]` — array of media objects with `url` and `display_order`

**Behavior:**
- Large primary image on left.
- Thumbnail strip below or on right.
- Clicking thumbnail updates primary image.
- Works without JavaScript for initial render (first image pre-rendered).

---

## ReservationForm

Used on: vehicle detail page (inline) and `/reservations/new`.

**Fields:**
- First name, last name (text)
- Email (email input)
- Phone (tel input)
- Pickup location (select)
- Return location (select, defaults to pickup)
- Pickup date (date picker)
- Return date (date picker)
- Notes (textarea, optional)
- Submit button: "Rezervasyon Talep Et"

**Validation** (client-side mirrors server-side rules):
- All fields except notes are required.
- Email format validation.
- Pickup date ≥ today.
- Return date > pickup date.
- Max 90 days.

---

## PriceDisplay

Used on: vehicle card, vehicle detail.

**Props:**
- `daily_price` (number)

**Render:**
```html
<span class="price">1.800 ₺</span>
<span class="price-unit">/ gün</span>
```

Format: Turkish locale (`Intl.NumberFormat('tr-TR', { style: 'currency', currency: 'TRY' })`).

---

## WhatsAppCTA

Used on: vehicle detail page, contact page.

**Props:**
- `phoneNumber` (from `WHATSAPP_NUMBER` env var)
- `vehicleName` (optional — pre-fills message)

**Render:**
```html
<a href="https://wa.me/{number}?text={encoded}" class="btn-whatsapp">
  [WhatsApp icon] WhatsApp ile İletişim
</a>
```

---

## StatusBadge

Used on: admin vehicle list, admin reservation list.

**Props:**
- `status` (string)

Colors defined in `design-system.md`.

---

## AdminTable

Used on: admin listing pages.

Generic table component with:
- Column definitions
- Sortable headers (optional v1 stretch)
- Action column (edit, delete, view buttons)
- Empty state message
- Pagination controls

---

## ConfirmationBanner

Used on: `/reservations/confirm` page.

**Props:**
- `reference_number`
- `vehicle_name`
- `pickup_date`
- `return_date`
- `total_price`

Displays a green success banner with reference number prominently shown.
