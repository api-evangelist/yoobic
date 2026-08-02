---
name: Provision YOOBIC users
description: Authenticate and create, update, or archive users in the YOOBIC frontline platform via the Public API.
api: YOOBIC Public API
base_url: https://api.yoobic.com/public/api
operations:
  - POST /public/api/auth/login
  - GET /public/api/users?filter={filter}
  - POST /public/api/users
  - PATCH /public/api/users/{id}
  - POST /public/api/users/{id}/archive
  - POST /public/api/users/import?type={type}
generated: '2026-07-21'
method: generated
source: openapi/yoobic-openapi.json
---

# Provision YOOBIC users

1. **Authenticate.** `POST /public/api/auth/login` with issued credentials; keep the returned JWT (note `expires_in`) and send `Authorization: Bearer <jwt>` on every call.
2. **Check for an existing user.** `GET /public/api/users?filter={"where":{"email":"..."}}` — the response `paging.total` tells you whether the user exists.
3. **Create or update.** New user: `POST /public/api/users`. Existing: `PATCH /public/api/users/{id}` (supports fields like position, department, division, company, skills).
4. **Bulk load.** For many users use `POST /public/api/users/import?type=csv|excel|json`; it returns a job id — poll `/public/api/jobs` for completion.
5. **Deactivate.** Archive rather than delete: `POST /public/api/users/{id}/archive` (reverse with `/unarchive`).

**Rules.** Users-write operations are capped at 180/min (POST/PATCH/DELETE); send serially and honor `ratelimit-remaining`. On 429, wait for the one-minute window. Errors come back as `{data, error}`.
