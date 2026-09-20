---
name: clix-so-send-push-notification
description: Send a one-off push notification to one or more targets through the Clix REST API, with the target, auth, batch, retry and idempotency rules the contract states. Use for transactional or time-sensitive sends outside a campaign; for marketer-owned templates use campaigns:trigger instead.
api: clix-so:clix-api
method: generated
source: openapi/clix-so-openapi.yml; https://docs.clix.so/api-reference/endpoint/messages:send; https://docs.clix.so/api-reference/rate-limits
operations:
  - ClixExternalService_SendPushNotifications
  - ClixExternalService_CreateUser
  - ClixExternalService_TriggerCampaign
---

# Send a push notification (Clix REST)

Grounded in `ClixExternalService_SendPushNotifications` — `POST https://api.clix.so/api/v1/messages:send`.

## Before you send

1. **Use a SECRET key.** Every request carries two headers: `X-Clix-Project-ID` and `X-Clix-API-Key`.
   Sending is a server-side operation; the docs reserve it for the secret key. Never put the secret key
   in a client.
2. **Know your target.** `push_notifications[].target` is a `oneOf`: exactly one of `project_user_id`
   (your own user id), `device_id` (a Clix device id) or `user_id` (the Clix user id). The spec says
   "Only one of project_user_id, device_id, or user_id should be present."
3. **Make sure the user exists** if you target by `project_user_id`. `ClixExternalService_CreateUser`
   (`POST /api/v1/users`) upserts — repeating it is safe.
4. **Decide: ad-hoc send or campaign?** If content and audience should be owned in the console, use
   `ClixExternalService_TriggerCampaign` (`POST /api/v1/campaigns/{campaign_id}:trigger`) instead and pass
   `properties` that become `{{ trigger.* }}`.

## The request

```json
POST /api/v1/messages:send
{
  "push_notifications": [
    {
      "target": { "project_user_id": "user_123" },
      "title": "Your order shipped",
      "body": "Tap to track it.",
      "image_url": "https://example.com/box.png",
      "landing_url": "myapp://orders/123"
    }
  ]
}
```

- `title` and `body` are strings; `image_url` and `landing_url` are optional.
- The body is a LIST. The schema says: "We recommend sending up to 500 push notifications." Batch, do not loop.
- JSON only (`Content-Type: application/json`); requests over 10 MB are rejected; a request is terminated after 100 seconds.

## The response

`200` returns `{ "delivery_results": [ { "message_id", "status", "additional_params": { "device_id", "fcm_message_id", "failure_reason" } } ] }`.
`status` is `DELIVERY_RESULT_STATUS_SUCCEED` or `DELIVERY_RESULT_STATUS_FAILED` — check every element; a 200 does not mean every push succeeded. Keep `message_id`: it is the key webhook events (`PUSH_SENT` / `PUSH_FAILED`) will carry.

## Errors

- `400` text/plain `Invalid push notification parameters` — fix the body; do not retry unchanged.
- `401` `Missing project id` / invalid key — check both headers and that the key is a secret key.
- `429` `{"error":"Too Many Requests"}` — 1,000 requests/second/project token bucket. Read `X-RateLimit-Remaining` and `Retry-After` (usually `1`), then retry.
- `5xx` — retry with exponential backoff (1s, 2s, 4s), maximum three attempts.

## Idempotency and reversibility (read before retrying)

- **There is no idempotency key on this operation.** A retried `messages:send` delivers twice. Only retry a request you know did not reach Clix (connection failure before a response), or use the A2A `send-push-notification` skill, whose `SendMessage` accepts `X-Clix-Idempotency-Key`.
- **A sent push cannot be recalled.** No reversal operation exists. Validate content and target first; the console's "Send Test" is the only rehearsal surface.

## Rules from conventions/

See `conventions/clix-so-conventions.yml` (idempotency coverage: partial; reversibility: documented) and
`errors/clix-so-problem-types.yml`.
