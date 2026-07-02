---
name: api-standards
description: Atlas REST/HTTP API design conventions for AI coding agents. Use when designing, implementing, or changing an HTTP endpoint, request/response schema, or error format in an Atlas service. Covers resource naming, versioning, status codes, pagination, and error envelopes. Don't use for gRPC/event schemas or for non-Atlas services.
license: MIT
metadata:
  author: Atlas Platform Engineering
  version: "1.0"
---

# Atlas API Design Standards

Consistency is the feature. New and changed HTTP APIs follow these conventions.

## Resources and naming
- Nouns, plural, lowercase, kebab-case: `/purchase-orders`, `/purchase-orders/{id}/line-items`.
- Use HTTP methods for verbs (GET, POST, PATCH, DELETE). No verbs in paths.

## Versioning and compatibility
- Version in the path: `/v1/...`. Additive changes only within a version.
- Never repurpose or remove a field in a released version; add a new one and deprecate the old.

## Status codes
- `200/201/204` for success, `400` invalid input, `401/403` auth, `404` missing, `409` conflict, `422` semantic validation, `429` rate limit, `5xx` server.

## Pagination and filtering
- Cursor-based pagination: `?limit=` + `?cursor=`, return `next_cursor`. Do not expose raw offsets.
- Filtering and sorting via explicit query params; never accept arbitrary query expressions.

## Error envelope
Return a consistent JSON error body:

```json
{ "error": { "code": "invalid_argument", "message": "human-readable", "details": [] } }
```

- `code` is a stable machine string; `message` is for humans; never leak stack traces or SQL.
