---
name: Register a YOOBIC webhook subscription
description: Create and manage webhook subscriptions so YOOBIC posts events to your endpoint via the Public API.
api: YOOBIC Public API
base_url: https://api.yoobic.com/public/api
operations:
  - POST /public/api/auth/login
  - POST /public/api/webhooks
  - GET /public/api/webhooks?filter={filter}
  - GET /public/api/webhooks/{id}
  - PATCH /public/api/webhooks/{id}
generated: '2026-07-21'
method: generated
source: openapi/yoobic-openapi.json
---

# Register a YOOBIC webhook subscription

1. **Authenticate.** `POST /public/api/auth/login`; send `Authorization: Bearer <jwt>`.
2. **Create the subscription.** `POST /public/api/webhooks` with your callback URL and the matching criteria; set `trigger_on_every_match` if you want the hook to fire on every match rather than once.
3. **Verify.** `GET /public/api/webhooks?filter={filter}` or `GET /public/api/webhooks/{id}` to confirm the subscription is registered.
4. **Update.** `PATCH /public/api/webhooks/{id}` to change the URL or match rules.
5. **Receive events.** Accept the HTTP POST at your endpoint and respond 2xx quickly; process asynchronously.

**Rules.** YOOBIC does not publish a machine-readable event-type catalog — confirm available triggers with support@yoobic.com. Honor the `{data, error}` error envelope and the per-organization rate limits.
