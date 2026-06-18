# QA Workflow — Rent A Car System

This is the required workflow for QA Testers and Bug Verifiers.

---

## Before testing

1. Read `ai-contracts-demo/README.md`.
2. Read `ai-contracts-demo/domain/business-rules.md` — these are the rules you are testing against.
3. Read `ai-contracts-demo/api/openapi.yaml` — API responses must match this contract.
4. Read `ai-contracts-demo/design/frontend-rules.md` — frontend behaviour rules.

---

## Test categories

### 1. API contract tests

For each endpoint in `api/openapi.yaml`:
- Does the response match the documented schema?
- Are the correct HTTP status codes returned?
- Is the error envelope format correct (see `api/error-format.md`)?
- Are business rule violations rejected with the correct error code?

### 2. Business rule tests

For each rule in `domain/business-rules.md`:
- Test the happy path.
- Test the boundary condition.
- Test the violation case.

Key rules to always test:
- BR-01: Pickup date in past → 422.
- BR-02: Return date before pickup → 422.
- BR-05: Vehicle not available → 422.
- BR-09: Reference number format `RAC-YYYYMMDD-NNNN`.

### 3. Public page tests

For each page in `design/page-map.md` (public section):
- Page loads without JS errors.
- `<title>` is present and unique.
- `<meta name="description">` is present.
- Vehicle detail: OG tags present.
- Links navigate correctly.
- Category filter works.
- Reservation form validates and submits.
- Confirmation page shows reference number.

### 4. Admin panel tests

- Login with invalid credentials → error shown.
- Login with valid credentials → redirect to dashboard.
- Unauthenticated access to admin routes → redirect to login.
- Vehicle CRUD operations work.
- Image upload works.
- Reservation status update persists.

### 5. Mobile / responsive tests

- Vehicle listing readable on 375px viewport.
- Category filter scrollable on mobile.
- Reservation form usable on mobile.
- Admin panel usable on tablet (768px+).

---

## Bug reporting

If a test fails:
1. Create a bug report in `docs/bugs/bug-{date}-{name}.md` using `templates/bug-template.md`.
2. Include: steps to reproduce, expected behaviour (from contract/business rules), actual behaviour.
3. Reference the specific contract rule or spec line being violated.

---

## Definition of Done (DoD)

A feature is complete when:
- [ ] All API responses match `api/openapi.yaml`.
- [ ] All business rules in `domain/business-rules.md` pass.
- [ ] All public pages have SEO tags.
- [ ] No console errors on any page.
- [ ] Reservation flow works end-to-end (submit → reference number shown).
- [ ] Admin can update reservation status.
- [ ] No 500 errors for expected user inputs.
