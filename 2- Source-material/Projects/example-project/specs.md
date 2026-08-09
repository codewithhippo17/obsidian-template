---
title: "{{title}} — Specs"
project: "{{project}}"
created: {{date}}
updated: {{date}}
tags:
  - specs
---

Tags: [[specs]]

# {{title}} — Technical Specs

## Domain Model

```
Entity: {{EntityName}}
├── field_1: type
├── field_2: type
└── field_3: type
```

## Database Schema

```sql
CREATE TABLE {{table_name}} (
  id          SERIAL PRIMARY KEY,
  field_1     VARCHAR(255) NOT NULL,
  field_2     INTEGER,
  created_at  TIMESTAMP DEFAULT NOW()
);
```

## API Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/api/{{resource}}` | List all | Yes |
| POST | `/api/{{resource}}` | Create | Yes |
| GET | `/api/{{resource}}/:id` | Get one | Yes |
| PUT | `/api/{{resource}}/:id` | Update | Yes |
| DELETE | `/api/{{resource}}/:id` | Delete | Yes |

## Agent Instructions

**Agent:** `{{agent}}`  
**Skills:** `{{skills}}`  
**Context:** Symlinked from vault via `{{symlink-path}}`

### Constraints
- Must follow the domain model above exactly.
- No hallucination — agent must only use symlinked docs as context.
- Fail fast on invalid state.

## Acceptance Criteria

- [ ] Criteria 1
- [ ] Criteria 2
- [ ] Criteria 3
