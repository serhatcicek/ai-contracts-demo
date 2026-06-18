# Backend Architecture — Rent A Car System

---

## Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js 20+ |
| Framework | Express 4 |
| Database (dev) | SQLite 3 via better-sqlite3 |
| Database (prod) | PostgreSQL 15+ via pg |
| Query builder | Knex.js |
| Auth | express-session + bcrypt |
| File uploads | multer |
| Validation | joi or zod |
| Testing | Jest + supertest |

---

## Directory structure (target)

```
demo-backend/
├── src/
│   ├── app.js               ← Express app factory
│   ├── server.js            ← HTTP server entry point
│   ├── config/
│   │   └── db.js            ← Knex connection config
│   ├── routes/
│   │   ├── vehicles.js
│   │   ├── categories.js
│   │   ├── reservations.js
│   │   ├── locations.js
│   │   ├── media.js
│   │   └── admin/
│   │       └── auth.js
│   ├── controllers/
│   │   ├── vehicleController.js
│   │   ├── categoryController.js
│   │   ├── reservationController.js
│   │   ├── locationController.js
│   │   └── mediaController.js
│   ├── middleware/
│   │   ├── auth.js          ← requireAdmin middleware
│   │   ├── errorHandler.js
│   │   └── validate.js      ← Joi/Zod request validation
│   ├── models/              ← Knex query helpers (not ORM models)
│   │   ├── Vehicle.js
│   │   ├── Category.js
│   │   ├── Reservation.js
│   │   ├── Location.js
│   │   └── Media.js
│   ├── migrations/          ← Knex migration files
│   └── seeds/               ← Knex seed files
├── uploads/                 ← Local image storage (dev)
├── knexfile.js
└── package.json
```

---

## API routing convention

All API routes are prefixed `/api/v1/`.

Public routes (no auth required):
- `GET /api/v1/vehicles`
- `GET /api/v1/vehicles/:slug`
- `GET /api/v1/categories`
- `GET /api/v1/locations`
- `POST /api/v1/reservations`

Admin routes (require auth):
- `POST /api/v1/admin/login`
- `DELETE /api/v1/admin/logout`
- `GET|POST|PUT|DELETE /api/v1/admin/vehicles`
- `GET|POST|PUT|DELETE /api/v1/admin/categories`
- `GET|PUT /api/v1/admin/reservations`
- `GET|POST|PUT|DELETE /api/v1/admin/locations`
- `POST|DELETE /api/v1/admin/vehicles/:id/media`

See `api/openapi.yaml` for full contract.

---

## Error format

See `api/error-format.md`. All errors return the standard envelope.

---

## Authentication

Session-based. Admin logs in with username/password. Session stored server-side. Cookie sent to browser.

- `POST /api/v1/admin/login` → sets session cookie.
- All `/api/v1/admin/*` routes check `req.session.adminId`.
- `requireAdmin` middleware returns `401` if not authenticated.

---

## Image upload

- `multer` handles multipart form data.
- Files stored in `uploads/` locally; path stored in `media` table.
- In production, swap multer storage to S3-compatible provider.
- Maximum file size: 5 MB per image.
- Accepted MIME types: `image/jpeg`, `image/png`, `image/webp`.

---

## Reference number generation

Format: `RAC-YYYYMMDD-NNNN` where `NNNN` is a zero-padded daily sequence.

Generated server-side in the reservation controller.
