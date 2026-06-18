# Frontend Workflow — Rent A Car System

This is the required workflow for all frontend agents and developers. Do not skip steps.

---

## Before writing any code

1. Read `ai-contracts-demo/README.md`.
2. Read `ai-contracts-demo/domain/rent-a-car-prd.md`.
3. Read `ai-contracts-demo/api/openapi.yaml` and `api/endpoints.md`.
4. Read `ai-contracts-demo/design/page-map.md`, `design/design-system.md`, and `design/components.md`.
5. Read `ai-contracts-demo/design/frontend-rules.md`.
6. Read `ai-contracts-demo/architecture/frontend-architecture.md`.
7. Read `ai-contracts-demo/governance/agent-boundaries.md`.

---

## Building a new page

1. Confirm the page exists in `design/page-map.md`. If not, raise it as a story first.
2. Check `api/openapi.yaml` — is the required endpoint available?
   - **Yes:** build the page against that contract.
   - **No:** create a story document in `docs/stories/` requesting the endpoint. Do not write backend code directly.
3. Implement the EJS template in `demo-frontend/src/views/`.
4. Add the route in the appropriate route file.
5. Add the backend API call in `demo-frontend/src/services/apiClient.js`.
6. Verify SEO requirements from `design/frontend-rules.md` are met (title, meta description, OG tags for detail pages).
7. Test in browser: desktop and mobile viewport.
8. Check: no JS errors in console, images load, form submits correctly.

---

## Adding or changing a UI component

1. Check `design/components.md` — does the component exist?
   - **Exists:** follow the spec.
   - **New component:** update `design/components.md` first, then implement.
2. Follow design tokens from `design/design-system.md`.
3. No inline styles — use Tailwind utility classes only.

---

## When you need a new backend endpoint

1. Do not modify `demo-backend/` source code.
2. Create a story document: `docs/stories/story-{date}-{name}.md` using `templates/story-template.md`.
3. Describe the needed endpoint, including request/response shape.
4. The Backend Developer or API Contract Owner will then update `api/openapi.yaml` and implement the endpoint.

---

## Code review checklist (self-review before done)

- [ ] Page exists in `design/page-map.md`.
- [ ] API calls only use endpoints defined in `api/openapi.yaml`.
- [ ] SEO: `<title>`, `<meta description>` present on all public pages.
- [ ] OG tags present on vehicle detail pages.
- [ ] Design tokens from `design-system.md` used (no hardcoded colours).
- [ ] Components match `design/components.md` specification.
- [ ] No backend source files modified.
- [ ] No console errors in browser.
- [ ] Accessible: `alt` on images, labels on form inputs.
- [ ] WhatsApp number from env var only.

---

## Forbidden actions

- Do not edit any file under `demo-backend/` without explicit approval.
- Do not call API endpoints that are not in `api/openapi.yaml`.
- Do not hardcode backend URLs, phone numbers, or secrets.
