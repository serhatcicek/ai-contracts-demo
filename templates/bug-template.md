# Bug Template

Copy this file to `docs/bugs/bug-{YYYYMMDD}-{short-name}.md` and fill in all sections.

---

# Bug: {Short Title}

**Date:** {YYYY-MM-DD}  
**Reporter:** {Role / Agent name}  
**Severity:** {Critical | High | Medium | Low}  
**Status:** {Open | In Progress | Fixed | Verified | Closed}  
**Assigned to:** {Backend Developer | Frontend Developer | ...}

---

## Environment

- **URL / Route:** {e.g. `POST /api/v1/reservations` or `/vehicles/ford-kuga-2023`}
- **Method:** {GET | POST | PUT | DELETE | — (browser)}
- **Browser / Client:** {e.g. Chrome 125, curl, Postman}

---

## Steps to reproduce

1. {Step 1}
2. {Step 2}
3. {Step 3}

---

## Expected behaviour

{What should happen according to the contract or business rule.}

**Reference:** {Link to the specific rule, e.g. `domain/business-rules.md BR-01` or `api/openapi.yaml /reservations POST`}

---

## Actual behaviour

{What actually happens. Include response body, status code, or screenshot description.}

```json
{
  "paste": "actual response here if applicable"
}
```

---

## Root cause (if known)

{Optional. Fill in after investigation.}

---

## Fix applied

{Optional. Fill in after fix. Include file path and brief description.}

---

## Verification steps

- [ ] {How to verify the fix is working}
- [ ] {Regression check: does the surrounding functionality still work?}
