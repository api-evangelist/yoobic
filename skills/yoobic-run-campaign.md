---
name: Publish a YOOBIC campaign
description: Create a campaign, add questions, set its audience, and publish it to frontline stores/users via the YOOBIC Public API.
api: YOOBIC Public API
base_url: https://api.yoobic.com/public/api
operations:
  - POST /public/api/auth/login
  - POST /public/api/campaigns
  - POST /public/api/campaigns/{id}/questions
  - PUT /public/api/campaigns/{id}/stores
  - POST /public/api/campaigns/{id}/publish
  - GET /public/api/campaigns/{id}/export?type={type}&filter={filter}
generated: '2026-07-21'
method: generated
source: openapi/yoobic-openapi.json
---

# Publish a YOOBIC campaign

1. **Authenticate.** `POST /public/api/auth/login`; send `Authorization: Bearer <jwt>`.
2. **Create the campaign.** `POST /public/api/campaigns` and capture the returned campaign `id`.
3. **Add questions.** `POST /public/api/campaigns/{id}/questions` for each question (update with `PUT .../questions/{question_id}`).
4. **Set the audience.** `PUT /public/api/campaigns/{id}/stores` to import the target stores/audience.
5. **Publish.** `POST /public/api/campaigns/{id}/publish` — supports per-site/per-user mission creation and a `user_ids` parameter; pass `notify` to alert recipients.
6. **Collect results.** `GET /public/api/campaigns/{id}/export?type=csv|excel&filter={...}` returns a job id; poll `/public/api/jobs` and download when ready.

**Rules.** Publishing creates missions for the audience; a mission must be assigned before it can be booked. Respect the 10 req/s overall limit and the `{data, error}` error envelope.
