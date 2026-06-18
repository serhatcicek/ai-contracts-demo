# Frontend Architecture — Rent A Car System

---

## Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js 20+ |
| Server framework | Express 4 |
| Template engine | EJS (public pages — SSR for SEO) |
| Admin panel | Vanilla JS or Alpine.js (lightweight SPA) |
| CSS | Tailwind CSS |
| Build tool | Vite (admin assets) |
| HTTP client | fetch (browser) / axios (server-side proxy) |
| Testing | Playwright (E2E) |

---

## Directory structure (target)

```
demo-frontend/
├── src/
│   ├── server.js            ← Express entry point
│   ├── routes/
│   │   ├── public.js        ← Public page routes
│   │   └── admin.js         ← Admin panel routes
│   ├── views/               ← EJS templates
│   │   ├── layout.ejs
│   │   ├── vehicles/
│   │   │   ├── listing.ejs
│   │   │   └── detail.ejs
│   │   ├── reservation/
│   │   │   ├── form.ejs
│   │   │   └── confirm.ejs
│   │   └── admin/
│   │       ├── login.ejs
│   │       ├── dashboard.ejs
│   │       ├── vehicles/
│   │       └── reservations/
│   ├── public/
│   │   ├── css/
│   │   ├── js/
│   │   └── images/
│   └── services/
│       └── apiClient.js     ← Server-side fetch wrapper for backend
├── package.json
└── vite.config.js
```

---

## Rendering strategy

| Page type | Strategy | Reason |
|---|---|---|
| Vehicle listing | SSR (EJS) | SEO — Google must index vehicle list |
| Vehicle detail | SSR (EJS) | SEO — each vehicle page is individually indexed |
| Reservation form | SSR (EJS) | Simplicity; form submits to backend |
| Reservation confirmation | SSR (EJS) | No JS required |
| Admin panel | Client-side SPA | Admin pages are not indexed; interactivity more important |

---

## API proxy pattern

The frontend server proxies all `/api/*` requests to the backend. This:
- Avoids CORS issues in the browser.
- Keeps the backend URL out of the browser.
- Allows the frontend to add auth cookies transparently.

```
Browser → GET /api/v1/vehicles
  → frontend Express proxy
      → GET http://localhost:3001/api/v1/vehicles
      ← JSON
  ← JSON (forwarded to browser)
```

---

## SEO requirements

See `design/frontend-rules.md` and `domain/business-rules.md` (SR-01 to SR-06).

Every public EJS template must include:
```html
<title><%= pageTitle %> | Rent A Car</title>
<meta name="description" content="<%= metaDescription %>">
```

Vehicle detail pages additionally:
```html
<meta property="og:title" content="<%= vehicle.name %>">
<meta property="og:description" content="<%= vehicle.description %>">
<meta property="og:image" content="<%= vehicle.primary_image_url %>">
```

---

## WhatsApp CTA

The WhatsApp CTA button links to:
```
https://wa.me/{WHATSAPP_NUMBER}?text={encoded_message}
```

`WHATSAPP_NUMBER` is set via environment variable `WHATSAPP_NUMBER`.

The message pre-fills the vehicle name and a prompt to inquire about availability.

---

## Page map

See `design/page-map.md` for the full list of routes and their templates.
