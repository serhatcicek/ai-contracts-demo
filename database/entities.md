# Database Entities — Rent A Car System

All table definitions are authoritative. Schema changes must be reflected here before implementing migrations.

---

## Table: categories

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | INTEGER | PK, AUTOINCREMENT | |
| name | VARCHAR(100) | NOT NULL, UNIQUE | Display name (e.g. "SUV") |
| slug | VARCHAR(100) | NOT NULL, UNIQUE | URL-safe identifier |
| image_url | VARCHAR(500) | NULLABLE | Optional category image |
| created_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |

---

## Table: locations

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | INTEGER | PK, AUTOINCREMENT | |
| name | VARCHAR(200) | NOT NULL | Branch/location name |
| address | TEXT | NOT NULL | Full street address |
| city | VARCHAR(100) | NOT NULL | City |
| phone | VARCHAR(30) | NULLABLE | Contact phone |
| latitude | DECIMAL(10,8) | NULLABLE | GPS coordinate |
| longitude | DECIMAL(11,8) | NULLABLE | GPS coordinate |
| is_active | BOOLEAN | NOT NULL, DEFAULT TRUE | |
| created_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |

---

## Table: vehicles

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | INTEGER | PK, AUTOINCREMENT | |
| category_id | INTEGER | FK → categories.id, NOT NULL | |
| name | VARCHAR(200) | NOT NULL | Display name (e.g. "Ford Focus 2023") |
| slug | VARCHAR(200) | NOT NULL, UNIQUE | URL-safe identifier |
| description | TEXT | NULLABLE | Full description |
| daily_price | DECIMAL(10,2) | NOT NULL | Price per day in TRY |
| fuel_type | VARCHAR(50) | NOT NULL | petrol / diesel / hybrid / electric |
| transmission | VARCHAR(50) | NOT NULL | manual / automatic |
| seat_count | INTEGER | NOT NULL | 2–9 |
| year | INTEGER | NULLABLE | Manufacturing year |
| status | VARCHAR(50) | NOT NULL, DEFAULT 'available' | available / rented / maintenance / inactive |
| created_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |

---

## Table: media

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | INTEGER | PK, AUTOINCREMENT | |
| vehicle_id | INTEGER | FK → vehicles.id, NOT NULL | |
| filename | VARCHAR(500) | NOT NULL | Stored filename |
| original_name | VARCHAR(500) | NULLABLE | Original upload filename |
| mime_type | VARCHAR(100) | NOT NULL | image/jpeg, image/png, image/webp |
| size_bytes | INTEGER | NULLABLE | File size |
| display_order | INTEGER | NOT NULL, DEFAULT 0 | Lower = shown first |
| created_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |

---

## Table: customers

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | INTEGER | PK, AUTOINCREMENT | |
| first_name | VARCHAR(100) | NOT NULL | |
| last_name | VARCHAR(100) | NOT NULL | |
| email | VARCHAR(200) | NOT NULL | |
| phone | VARCHAR(30) | NOT NULL | |
| created_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |

Index: `(email, phone)` — not unique, allows repeat customers.

---

## Table: reservations

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | INTEGER | PK, AUTOINCREMENT | |
| reference_number | VARCHAR(30) | NOT NULL, UNIQUE | RAC-YYYYMMDD-NNNN |
| customer_id | INTEGER | FK → customers.id, NOT NULL | |
| vehicle_id | INTEGER | FK → vehicles.id, NOT NULL | |
| pickup_location_id | INTEGER | FK → locations.id, NOT NULL | |
| return_location_id | INTEGER | FK → locations.id, NOT NULL | |
| pickup_date | DATE | NOT NULL | |
| return_date | DATE | NOT NULL | |
| rental_days | INTEGER | NOT NULL | Computed: return - pickup |
| daily_price_snapshot | DECIMAL(10,2) | NOT NULL | Price at time of reservation |
| total_price | DECIMAL(10,2) | NOT NULL | daily_price_snapshot × rental_days |
| status | VARCHAR(50) | NOT NULL, DEFAULT 'pending' | pending / confirmed / cancelled / completed |
| notes | TEXT | NULLABLE | Customer notes |
| admin_notes | TEXT | NULLABLE | Internal admin notes |
| created_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |

---

## Table: admins

| Column | Type | Constraints | Description |
|---|---|---|---|
| id | INTEGER | PK, AUTOINCREMENT | |
| username | VARCHAR(100) | NOT NULL, UNIQUE | |
| password_hash | VARCHAR(255) | NOT NULL | bcrypt hash |
| created_at | TIMESTAMP | NOT NULL, DEFAULT NOW | |
| last_login_at | TIMESTAMP | NULLABLE | |
