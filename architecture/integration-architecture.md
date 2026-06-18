# Integration Architecture — Rent A Car System

---

## Communication pattern

Backend and frontend communicate exclusively through the REST API defined in `api/openapi.yaml`.

```
demo-frontend  ←→  demo-backend (via /api/v1/*)
```

There is no direct database access from the frontend. There is no shared code module between backend and frontend in v1.

---

## Request routing table

| Request origin | Path | Handled by |
|---|---|---|
| Browser | `GET /vehicles` | Frontend SSR route |
| Browser | `GET /vehicles/:slug` | Frontend SSR route |
| Browser | `POST /reservations` | Frontend → Backend proxy |
| Browser | `/admin/*` | Frontend admin SPA |
| Frontend server | `GET /api/v1/*` | Backend API |
| Browser (admin SPA) | `GET /api/v1/admin/*` | Backend API (via frontend proxy) |

---

## CORS policy

- In development: frontend and backend run on different ports. Frontend proxy avoids CORS entirely.
- Backend sets `Access-Control-Allow-Origin: http://localhost:4173` for development.
- In production: both served from the same origin or behind a reverse proxy; CORS headers adjusted accordingly.

---

## Authentication flow (admin)

```
1. Admin → POST /admin/login (form submit via frontend)
2. Frontend server → POST /api/v1/admin/login (proxy)
3. Backend validates credentials → sets session cookie
4. Cookie returned to browser
5. Subsequent admin API calls include cookie automatically
6. Backend requireAdmin middleware validates session
```

---

## Image serving

- Dev: Backend serves images from `uploads/` at `/uploads/:filename`.
- Frontend templates reference images via `{BACKEND_URL}/uploads/:filename` or a configured `MEDIA_BASE_URL` environment variable.
- In production: images served from CDN/S3; `MEDIA_BASE_URL` points to CDN.

---

## Environment variables

### demo-backend

| Variable | Description | Default |
|---|---|---|
| `PORT` | Backend listen port | `3001` |
| `SESSION_SECRET` | express-session secret | required |
| `DB_PATH` | SQLite file path (dev) | `./dev.db` |
| `DATABASE_URL` | PostgreSQL connection string (prod) | — |
| `UPLOAD_DIR` | Local image upload directory | `./uploads` |
| `ADMIN_USERNAME` | Initial admin username | `admin` |
| `ADMIN_PASSWORD_HASH` | Bcrypt hash of admin password | required |

### demo-frontend

| Variable | Description | Default |
|---|---|---|
| `PORT` | Frontend listen port | `4173` |
| `BACKEND_URL` | Base URL of backend API | `http://localhost:3001` |
| `MEDIA_BASE_URL` | Base URL for media files | `http://localhost:3001` |
| `WHATSAPP_NUMBER` | WhatsApp business number | required |

---

## Contract change protocol

See `workflows/api-change-workflow.md` for the full process. In summary:

1. Update `api/openapi.yaml` first.
2. Update `api/endpoints.md`.
3. Backend implements the new/changed endpoint.
4. Frontend updates the consumer code.
5. QA validates against the updated contract.

**Never implement an endpoint that is not in `api/openapi.yaml`.**
