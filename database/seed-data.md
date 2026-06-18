# Seed Data — Rent A Car System

Seed data is used for development and demo environments. Files live in `demo-backend/src/seeds/`.

---

## Categories (seed)

| id | name | slug |
|---|---|---|
| 1 | Economy | economy |
| 2 | Sedan | sedan |
| 3 | SUV | suv |
| 4 | Van | van |
| 5 | Luxury | luxury |
| 6 | Convertible | convertible |

---

## Locations (seed)

| id | name | city | address |
|---|---|---|---|
| 1 | İstanbul Havalimanı Şubesi | İstanbul | İstanbul Havalimanı, Terminal A, Zemin Kat |
| 2 | Sabiha Gökçen Şubesi | İstanbul | SAW Terminal, Araç Kiralama Bölümü |
| 3 | Ankara Merkez | Ankara | Kızılay Meydanı No:1, Çankaya |

---

## Sample vehicles (seed)

| id | name | category | daily_price | status | fuel | transmission | seats |
|---|---|---|---|---|---|---|---|
| 1 | Renault Clio 2023 | Economy | 850.00 | available | petrol | manual | 5 |
| 2 | Toyota Corolla 2024 | Sedan | 1200.00 | available | hybrid | automatic | 5 |
| 3 | Ford Kuga 2023 | SUV | 1800.00 | available | diesel | automatic | 5 |
| 4 | Volkswagen Caravelle 2022 | Van | 2500.00 | available | diesel | automatic | 9 |
| 5 | Mercedes C180 2024 | Luxury | 3200.00 | available | petrol | automatic | 5 |

---

## Admin user (seed)

| username | password (plain, dev only) |
|---|---|
| admin | Admin123! |

**Note:** The seed stores a bcrypt hash of `Admin123!`. This password is for development only. Change before any production deployment.

---

## Seed file order

```
01_categories.js
02_locations.js
03_vehicles.js
04_media.js     ← placeholder images only in dev
05_admin.js
```
