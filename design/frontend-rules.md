# Frontend Rules — Rent A Car System

These rules are mandatory for all frontend implementations. They cover SEO, accessibility, performance, and code conventions.

---

## SEO rules

Refer to `domain/business-rules.md` SR-01 to SR-06. Summary:

1. Every public page must have a unique `<title>` tag (format: `{Page Title} | Rent A Car`).
2. Every public page must have `<meta name="description">`.
3. Vehicle detail pages must include Open Graph tags: `og:title`, `og:description`, `og:image`.
4. Public pages must return full HTML in the initial HTTP response (SSR). Do not rely on client-side JS for indexable content.
5. Vehicle listing URL: `/vehicles`. Vehicle detail URL: `/vehicles/:slug`.
6. Use `<link rel="canonical">` on all pages to prevent duplicate content.

---

## Accessibility rules

1. All images must have meaningful `alt` attributes. Vehicle images: `alt="{vehicle.name}"`.
2. Form inputs must have associated `<label>` elements (use `for` + `id`).
3. Buttons must have descriptive text or `aria-label`.
4. Color contrast ratio must meet WCAG AA (4.5:1 for normal text, 3:1 for large text).
5. Interactive elements must be keyboard-navigable.
6. Use semantic HTML: `<nav>`, `<main>`, `<header>`, `<footer>`, `<section>`, `<article>`.

---

## Performance rules

1. Largest Contentful Paint (LCP) target: < 2.5 s on a 3G connection.
2. Vehicle listing images: use `loading="lazy"` for images below the fold. Above-the-fold primary image: `loading="eager"`.
3. Compress uploaded images on upload (backend responsibility) or use `srcset` / WebP.
4. Tailwind must be purged in production build (no unused CSS).
5. Do not load heavy JS libraries on public pages. Admin panel may use more JS.

---

## Form rules

1. Show inline validation errors next to each field (not just a top-level error summary).
2. Disable submit button while form is submitting (prevent double-submit).
3. After successful reservation submission, redirect to `/reservations/confirm?ref={reference_number}`.
4. Form fields must retain their values on validation failure (do not clear the form).
5. Server-side validation errors returned in the API response must be displayed to the user.

---

## Naming and code conventions

1. EJS template files use kebab-case: `vehicle-detail.ejs`.
2. CSS class names follow Tailwind utility classes; custom classes use BEM where needed.
3. JavaScript files use camelCase.
4. All user-facing text strings in Turkish (tr-TR) for v1.
5. Currency formatting: `Intl.NumberFormat('tr-TR', { style: 'currency', currency: 'TRY' })`.
6. Date formatting: `Intl.DateTimeFormat('tr-TR', { day: '2-digit', month: 'long', year: 'numeric' })`.

---

## Security rules

1. Never expose the backend URL or session secrets in public page HTML.
2. Sanitise all user input before rendering in templates (EJS auto-escapes by default with `<%= %>`; never use `<%- %>` for user-provided data).
3. CSRF protection: include a CSRF token on all POST forms (use `csurf` or equivalent).
4. Admin panel routes must redirect to `/admin/login` if session is missing.

---

## WhatsApp CTA rules

1. The WhatsApp number must come from the `WHATSAPP_NUMBER` environment variable — never hardcoded.
2. The pre-filled message must include the vehicle name and a prompt.
3. The CTA must open in a new tab (`target="_blank" rel="noopener"`).
