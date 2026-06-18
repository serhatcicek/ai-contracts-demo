# Model: Media

**Table:** `media`  
**Source of truth for schema:** `database/entities.md`

---

## Fields

| Field | Type | Notes |
|---|---|---|
| `id` | integer | Auto-increment primary key |
| `vehicle_id` | integer | FK → vehicles (CASCADE DELETE) |
| `filename` | string | Server-stored filename (UUID-based) |
| `original_name` | string\|null | Original filename from upload |
| `mime_type` | string | `image/jpeg` \| `image/png` \| `image/webp` |
| `size_bytes` | integer\|null | File size in bytes |
| `display_order` | integer | Lower value = displayed first. 0 = primary/thumbnail. |
| `created_at` | timestamp | |

---

## URL construction

The API returns a `url` field constructed as:

```
{MEDIA_BASE_URL}/uploads/{filename}
```

`MEDIA_BASE_URL` is set via environment variable (see `architecture/integration-architecture.md`).

In the database, only `filename` is stored, not the full URL. This allows the URL prefix to change without a database migration.

---

## Primary image

The image with the lowest `display_order` value is treated as the primary/thumbnail image.

In list endpoints, only `primary_image_url` is returned (the single primary image URL, not the full array).

In detail endpoints, the full `media` array is returned ordered by `display_order ASC`.

---

## Upload constraints

| Constraint | Value |
|---|---|
| Accepted types | `image/jpeg`, `image/png`, `image/webp` |
| Max file size | 5 MB per file |
| Max images per vehicle | 20 (soft limit) |

---

## Business rules

- VR-02: A vehicle must have at least one image before it can be set to `available`.
- VR-03: The first image (lowest `display_order`) is the primary/thumbnail.
- When a vehicle is hard-deleted (which should not happen in v1 — use soft-delete), media records cascade delete.
- Reordering: `display_order` can be updated by Admin via a bulk-update endpoint (v2 stretch).

---

## API endpoints

See `api/endpoints.md` — Media section.
