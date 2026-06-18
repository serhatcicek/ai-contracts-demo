# API Change Template

Copy this file to `docs/api-changes/api-change-{YYYYMMDD}-{short-name}.md` and fill in all sections.

Also see `workflows/api-change-workflow.md` for the full process.

---

# API Change: {Short Title}

**Date:** {YYYY-MM-DD}  
**Author:** {Role / Agent name}  
**Breaking change:** {Yes | No}  
**Status:** {Draft | Approved | Implemented | Verified}

---

## Summary

{One paragraph describing what is changing and why.}

---

## Change details

### Affected endpoint(s)

| Method | Path | Type of change |
|---|---|---|
| {GET/POST/...} | `/api/v1/{path}` | {New / Modified / Removed} |

### Before (current contract)

```yaml
# Paste relevant section from openapi.yaml
```

### After (proposed contract)

```yaml
# Paste updated section
```

---

## Breaking change analysis

| Consumer | Impact | Action required |
|---|---|---|
| Frontend — {page name} | {Describe impact} | {What must change} |
| {Other consumer} | {Describe impact} | {What must change} |

---

## Implementation checklist

- [ ] `api/openapi.yaml` updated
- [ ] `api/endpoints.md` updated
- [ ] `api/request-response-examples.md` updated (if helpful)
- [ ] Backend implementation complete
- [ ] Frontend consumer updated
- [ ] QA validation complete

---

## Rollback plan

{How to revert this change if it causes issues.}

---

## Notes

{Any additional context, open questions, or dependencies.}
