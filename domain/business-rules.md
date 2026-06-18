# Business Rules — Anar Rent A Car System

These rules are enforced by the backend. Frontend must reflect them in validation UX but the backend is the authority.

**Company:** Anar Rent A Car  
**Address:** ARTUKLU APARTMANI, 13 Mart, MEHMET REMZİ YERSEL CADDESİ NO:5 D:6, 47100 Artuklu/Mardin  
**Phone:** 0544 289 60 55  
**Email:** info@anarrentacar.com  
**Language:** Turkish (tr-TR)  
**Currency:** TRY (Turkish Lira)  
**Primary Location:** Mardin, Turkey

---

## 1. Reservation rules

| # | Rule |
|---|---|
| BR-01 | Pickup date must be today or in the future. |
| BR-02 | Return date must be strictly after pickup date. |
| BR-03 | Minimum rental duration is 1 day. |
| BR-04 | Maximum rental duration is 90 days. |
| BR-05 | A vehicle with status `rented` or `maintenance` cannot be reserved. |
| BR-06 | A vehicle with status `inactive` must not appear on public pages. |
| BR-07 | Customer phone number is required for reservation submission. |
| BR-08 | Customer email must be a valid email format. |
| BR-09 | A reservation reference number is generated server-side in the format `RAC-YYYYMMDD-NNNN`. |
| BR-10 | Duplicate reservations (same customer email + same vehicle + overlapping dates) should warn but not hard-block in v1. |

---

## 2. Pricing rules

| # | Rule |
|---|---|
| PR-01 | Daily price is set per vehicle and stored in the primary currency (TRY). |
| PR-02 | Total price = `daily_price × rental_duration_days`. |
| PR-03 | Rental duration is calculated as `return_date − pickup_date` in full calendar days. |
| PR-04 | Prices are displayed without VAT in v1. |
| PR-05 | Price changes do not retroactively affect existing confirmed reservations. |

---

## 3. Vehicle rules

| # | Rule |
|---|---|
| VR-01 | A vehicle must belong to exactly one category. |
| VR-02 | A vehicle must have at least one image before it can be set to `available`. |
| VR-03 | The first image in order is treated as the primary/thumbnail image. |
| VR-04 | Vehicle slug must be unique and URL-safe. |
| VR-05 | Deleting a vehicle is a soft-delete; it sets status to `inactive`. |
| VR-06 | Seat count must be between 2 and 9. |

---

## 4. Category rules

| # | Rule |
|---|---|
| CR-01 | Category name must be unique. |
| CR-02 | A category cannot be deleted if it has associated vehicles. |
| CR-03 | Category names are displayed in Turkish for public pages in v1. |

---

## 5. Location rules

| # | Rule |
|---|---|
| LR-01 | A reservation must have a pickup location. |
| LR-02 | Return location defaults to pickup location if not specified. |
| LR-03 | Locations are managed by Admin only. |

---

## 6. Admin rules

| # | Rule |
|---|---|
| AR-01 | All admin endpoints require authentication. |
| AR-02 | There is a single admin role in v1 (no permission tiers). |
| AR-03 | Admin can change reservation status to any value. |
| AR-04 | Customers cannot change reservation status themselves. |

---

## 7. SEO / public page rules

| # | Rule |
|---|---|
| SR-01 | Every public page must have a unique `<title>` tag. |
| SR-02 | Every public page must have a `<meta name="description">` tag. |
| SR-03 | Vehicle detail pages must include Open Graph `og:title`, `og:description`, `og:image`. |
| SR-04 | The vehicle listing URL is `/vehicles`. |
| SR-05 | Vehicle detail URL pattern is `/vehicles/{slug}`. |
| SR-06 | Pages must return HTTP 200 with full HTML content (no JS-only render for critical content). |
| SR-07 | Site tagline: "Güvenilir Kiralama Çözümleri" (Reliable Rental Solutions). |
| SR-08 | Company contact: 0544 289 60 55 | info@anarrentacar.com |
