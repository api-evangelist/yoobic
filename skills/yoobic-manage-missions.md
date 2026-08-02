---
name: Assign and validate YOOBIC missions
description: Assign frontline missions (tasks) to users, track completion, and validate submitted work via the YOOBIC Public API.
api: YOOBIC Public API
base_url: https://api.yoobic.com/public/api
operations:
  - POST /public/api/auth/login
  - GET /public/api/missions?filter={filter}
  - POST /public/api/missions/{id}/assign
  - POST /public/api/missions/{id}/book
  - POST /public/api/missions/{id}/finish
  - POST /public/api/missions/{id}/validate
generated: '2026-07-21'
method: generated
source: openapi/yoobic-openapi.json
---

# Assign and validate YOOBIC missions

1. **Authenticate.** `POST /public/api/auth/login`; send `Authorization: Bearer <jwt>`.
2. **Find missions.** `GET /public/api/missions?filter={"where":{...}}` to locate missions by store, campaign, or status.
3. **Assign.** `POST /public/api/missions/{id}/assign` to give the mission to a user (reverse with `/unassign`).
4. **Book.** `POST /public/api/missions/{id}/book` — a mission must be assigned before it can be booked.
5. **Finish and validate.** After the frontline user completes it, `POST /public/api/missions/{id}/finish`, then `POST /public/api/missions/{id}/validate` to approve; inspect `/missions/{id}/tasks` for detail.

**Rules.** Follow the assign -> book -> finish -> validate order. Send requests serially (10 req/s cap); errors return `{data, error}` with HTTP 4xx.
