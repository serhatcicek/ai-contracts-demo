# Story Template

Copy this file to `docs/stories/story-{YYYYMMDD}-{short-name}.md` and fill in all sections.

---

# Story: {Short Title}

**Date:** {YYYY-MM-DD}  
**Author:** {Role / Agent name}  
**Target agent/role:** {Backend Developer | Frontend Developer | API Contract Owner | ...}  
**Priority:** {High | Medium | Low}  
**Status:** {Draft | Ready | In Progress | Done}

---

## Context

{Why is this needed? What problem does it solve? Reference the relevant PRD section or business rule if applicable.}

---

## User story

As a {role},  
I want {capability},  
so that {benefit}.

---

## Acceptance criteria

- [ ] {Specific, testable criterion 1}
- [ ] {Specific, testable criterion 2}
- [ ] {Specific, testable criterion 3}

---

## API requirements (if requesting a new/changed endpoint)

**Method:** {GET | POST | PUT | DELETE}  
**Path:** `/api/v1/{path}`

**Request body:**
```json
{
  "field": "value"
}
```

**Response body:**
```json
{
  "success": true,
  "data": {}
}
```

**Notes:** {Any specific validation, business rule, or edge case notes.}

---

## Design requirements (if requesting a UI change)

{Describe the UI change needed. Reference `design/page-map.md`, `design/components.md` if applicable.}

---

## Out of scope

{List anything explicitly excluded from this story.}

---

## Notes / open questions

{Any unresolved questions or dependencies.}
