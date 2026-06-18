# Request / Response Examples — Rent A Car API

---

## GET /api/v1/vehicles

**Request:**
```
GET /api/v1/vehicles?category_slug=suv&page=1&limit=10
```

**Response 200:**
```json
{
  "success": true,
  "data": [
    {
      "id": 3,
      "name": "Ford Kuga 2023",
      "slug": "ford-kuga-2023",
      "daily_price": 1800.00,
      "status": "available",
      "fuel_type": "diesel",
      "transmission": "automatic",
      "seat_count": 5,
      "year": 2023,
      "category": {
        "id": 3,
        "name": "SUV",
        "slug": "suv",
        "image_url": null
      },
      "primary_image_url": "http://localhost:3001/uploads/ford-kuga-001.jpg"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 1,
    "total_pages": 1
  }
}
```

---

## GET /api/v1/vehicles/:slug

**Request:**
```
GET /api/v1/vehicles/ford-kuga-2023
```

**Response 200:**
```json
{
  "success": true,
  "data": {
    "id": 3,
    "name": "Ford Kuga 2023",
    "slug": "ford-kuga-2023",
    "description": "Güçlü dizel motoruyla uzun yolculuklar için ideal...",
    "daily_price": 1800.00,
    "status": "available",
    "fuel_type": "diesel",
    "transmission": "automatic",
    "seat_count": 5,
    "year": 2023,
    "category": {
      "id": 3,
      "name": "SUV",
      "slug": "suv",
      "image_url": null
    },
    "primary_image_url": "http://localhost:3001/uploads/ford-kuga-001.jpg",
    "media": [
      { "id": 1, "url": "http://localhost:3001/uploads/ford-kuga-001.jpg", "display_order": 0 },
      { "id": 2, "url": "http://localhost:3001/uploads/ford-kuga-002.jpg", "display_order": 1 }
    ]
  }
}
```

**Response 404:**
```json
{
  "success": false,
  "error": {
    "code": "NOT_FOUND",
    "message": "Vehicle not found"
  }
}
```

---

## POST /api/v1/reservations

**Request:**
```json
{
  "vehicle_id": 3,
  "first_name": "Ahmet",
  "last_name": "Yılmaz",
  "email": "ahmet@example.com",
  "phone": "+905001234567",
  "pickup_location_id": 1,
  "return_location_id": 1,
  "pickup_date": "2026-07-01",
  "return_date": "2026-07-05",
  "notes": "Çocuk koltuğu gerekiyor"
}
```

**Response 201:**
```json
{
  "success": true,
  "data": {
    "id": 42,
    "reference_number": "RAC-20260618-0042",
    "status": "pending",
    "rental_days": 4,
    "daily_price_snapshot": 1800.00,
    "total_price": 7200.00
  }
}
```

**Response 422 (validation error):**
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      { "field": "pickup_date", "message": "Pickup date must be today or in the future" },
      { "field": "email", "message": "Must be a valid email address" }
    ]
  }
}
```

---

## POST /api/v1/admin/login

**Request:**
```json
{
  "username": "admin",
  "password": "Admin123!"
}
```

**Response 200:**
```json
{
  "success": true,
  "message": "Login successful"
}
```
Set-Cookie: connect.sid=s%3A...; Path=/; HttpOnly

**Response 401:**
```json
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Invalid credentials"
  }
}
```

---

## POST /api/v1/admin/vehicles (create)

**Request:**
```json
{
  "name": "Renault Megane 2024",
  "category_id": 2,
  "description": "Konforlu sedan...",
  "daily_price": 1100.00,
  "fuel_type": "petrol",
  "transmission": "automatic",
  "seat_count": 5,
  "year": 2024,
  "status": "available"
}
```

**Response 201:**
```json
{
  "success": true,
  "data": {
    "id": 6,
    "name": "Renault Megane 2024",
    "slug": "renault-megane-2024",
    "daily_price": 1100.00,
    "status": "available",
    "fuel_type": "petrol",
    "transmission": "automatic",
    "seat_count": 5,
    "year": 2024,
    "description": "Konforlu sedan...",
    "category": { "id": 2, "name": "Sedan", "slug": "sedan" },
    "primary_image_url": null,
    "media": []
  }
}
```

---

## PUT /api/v1/admin/reservations/:id (update status)

**Request:**
```json
{
  "status": "confirmed",
  "admin_notes": "Müşteri ile telefonda görüşüldü, onaylandı."
}
```

**Response 200:**
```json
{
  "success": true,
  "data": {
    "id": 42,
    "reference_number": "RAC-20260618-0042",
    "status": "confirmed",
    "admin_notes": "Müşteri ile telefonda görüşüldü, onaylandı.",
    "updated_at": "2026-06-18T10:30:00.000Z"
  }
}
```
