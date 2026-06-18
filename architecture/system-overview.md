# System Overview — Rent A Car System

---

## High-level architecture

```
┌─────────────────────────────────────────────────────────┐
│                      Browser / Client                    │
│                                                         │
│   Public pages           Admin panel                   │
│   (SSR / static)         (SPA, auth-gated)             │
└─────────────────┬──────────────────┬────────────────────┘
                  │  HTTP/REST        │  HTTP/REST
                  ▼                  ▼
┌─────────────────────────────────────────────────────────┐
│                    demo-frontend                         │
│               Node.js / Express server                   │
│  Renders public pages (SSR), proxies API calls          │
│  Serves admin SPA assets                                │
└─────────────────────────┬───────────────────────────────┘
                          │  HTTP/REST JSON
                          ▼
┌─────────────────────────────────────────────────────────┐
│                    demo-backend                          │
│               Node.js / Express API server               │
│  /api/v1/* — vehicles, categories, reservations,        │
│              locations, media, admin/auth               │
└─────────────────────────┬───────────────────────────────┘
                          │  SQL
                          ▼
┌─────────────────────────────────────────────────────────┐
│                    Database                              │
│               SQLite (dev) / PostgreSQL (prod)           │
└─────────────────────────────────────────────────────────┘
```

---

## Component responsibilities

| Component | Responsibility |
|---|---|
| **demo-frontend** | Render public pages (vehicle listing, detail, reservation form); serve admin panel SPA; proxy `/api/*` to backend. |
| **demo-backend** | Expose REST API; enforce business rules; manage database; handle image uploads; admin authentication. |
| **Database** | Persist all domain data: vehicles, categories, reservations, customers, locations, media. |
| **ai-contracts-demo** | Contract and documentation layer only. No runtime code. |

---

## Technology choices (v1)

| Layer | Technology | Reason |
|---|---|---|
| Backend runtime | Node.js + Express | Matches existing demo-backend skeleton |
| Frontend server | Node.js + Express | Matches existing demo-frontend skeleton |
| Database (dev) | SQLite | Zero-config local development |
| Database (prod) | PostgreSQL | Production-ready, migrated from SQLite schema |
| ORM | Knex.js | Lightweight, supports both SQLite and PostgreSQL |
| Image storage | Local filesystem (dev) / S3-compatible (prod) | Progressive enhancement |
| Auth | Session-based (express-session + bcrypt) | Simple admin-only auth for v1 |
| Frontend rendering | Handlebars / EJS SSR (public) + Vanilla JS or lightweight framework (admin) | SEO requirement for public pages |

---

## Environments

| Environment | Frontend URL | Backend URL | Database |
|---|---|---|---|
| Local dev | http://localhost:4173 | http://localhost:3001 | SQLite (`dev.db`) |
| Production | TBD | TBD | PostgreSQL |

---

## Data flow: public vehicle listing

```
Browser → GET /vehicles
  → frontend server renders HTML (SSR)
      → GET http://backend/api/v1/vehicles?status=available
          ← JSON array of vehicles
      ← HTML page with vehicles embedded
  ← Rendered HTML returned to browser
```

## Data flow: reservation submission

```
Browser → POST /reservations (form submit)
  → frontend server
      → POST http://backend/api/v1/reservations
          ← { reference_number, status: "pending" }
      ← Redirect to /reservations/confirm?ref=RAC-...
  ← Confirmation page
```
