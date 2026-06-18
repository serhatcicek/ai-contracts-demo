# Domain Glossary — Rent A Car System

All agents and developers must use these terms consistently across code, contracts, and documentation.

---

| Term | Definition |
|---|---|
| **Vehicle** | A car available for rent in the fleet. Has a category, daily price, status, and one or more images. |
| **Category** | A classification of vehicles (e.g. Economy, Sedan, SUV, Van, Luxury). |
| **Reservation** | A formal request by a customer to rent a specific vehicle for a date range. Also used interchangeably with "Inquiry" in v1. |
| **Inquiry** | A non-binding contact request about a vehicle. In v1, reservations and inquiries share the same data model. |
| **Customer** | A person who submits a reservation or inquiry. Does not require an account in v1. |
| **Admin** | A staff member who manages vehicles, categories, and reservations via the admin panel. |
| **Pickup Location** | The physical branch or address where the customer collects the vehicle. |
| **Return Location** | The physical branch or address where the customer returns the vehicle. |
| **Pickup Date** | The date (and optionally time) the customer collects the vehicle. |
| **Return Date** | The date (and optionally time) the customer returns the vehicle. |
| **Daily Price** | The rental cost per calendar day in the primary currency (TRY for v1). |
| **Rental Duration** | The number of days between pickup date and return date (inclusive). |
| **Total Price** | `daily_price × rental_duration`. Calculated server-side. |
| **Reference Number** | A unique, human-readable identifier for a reservation (e.g. `RAC-20260618-0042`). |
| **Vehicle Status** | One of: `available`, `rented`, `maintenance`, `inactive`. |
| **Reservation Status** | One of: `pending`, `confirmed`, `cancelled`, `completed`. |
| **Fleet** | The complete collection of vehicles owned or managed by the business. |
| **Location** | A physical branch of the rental company. Has a name, address, phone, and coordinates. |
| **Media** | An image or file attached to a vehicle. Has an order (primary image first). |
| **Slug** | A URL-safe identifier derived from the vehicle's name and year (e.g. `ford-focus-2023`). |
| **CTA** | Call to Action — a prominent button or link encouraging a user action (e.g. WhatsApp, Reserve Now). |
| **SEO** | Search Engine Optimisation — practices that improve organic search ranking. |
| **SSR** | Server-Side Rendering — pages whose initial HTML is generated on the server. |
| **Admin Panel** | The password-protected management interface used by Admins. |
| **Public Pages** | Pages visible to unauthenticated visitors (listing, detail). |
