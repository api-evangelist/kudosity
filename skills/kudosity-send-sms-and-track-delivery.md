---
name: Send an SMS and track its delivery
description: Send a single SMS through the Kudosity Transmit Message (v2) API and follow it to a delivery outcome, either by polling or by subscribing to a webhook.
api: openapi/kudosity-transmit-message-openapi-original.yml
operations:
  - POST /v2/sms
  - GET /v2/sms/{id}
  - POST /v2/webhook
---

# Send an SMS and track its delivery

## Before you start

- Authentication is an API key in the `x-api-key` header. Get it from the Kudosity dashboard under **Developers → API Settings**. There is no OAuth, no scopes, and no token exchange — the key carries full account access.
- Base URL is `https://api.transmitmessage.com`.
- **There is no sandbox.** Every send is a real, billable message to a real handset. Do not send to a number you do not control while testing.
- **There is no idempotency key.** A retried `POST /v2/sms` sends a second message and bills a second time. Never retry a send on a timeout without first checking `GET /v2/sms` for the message.
- The account is rate limited to 15 requests/second. Over the limit you get `429` with error code `OVER_LIMIT` and the message request is **dropped, not queued**.

## Steps

1. **Send.** `POST /v2/sms` with `message`, `sender` and `recipient`. Include `message_ref` — your own reference string — so you can reconcile the send later without depending on the Kudosity id.
2. **Capture the id.** The response carries the Kudosity message id. Store it alongside your `message_ref`.
3. **Track the outcome.** Two options:
   - **Poll:** `GET /v2/sms/{id}`.
   - **Subscribe (preferred):** `POST /v2/webhook` with a `filter.event_type` of `SMS_STATUS`. You can narrow further on `sender`, `status`, `message_ref` or `campaign_id`. Use `filter.event_type`, not the deprecated top-level `event_type`.
4. **Verify the callback.** Kudosity signs callbacks with an `x-transmitsms-signature` header — an HMAC-SHA256 over the JSON-encoded callback parameters keyed by your account API secret. The parameters must be hashed **in the order they arrive**. Reject unsigned or mismatched callbacks.

## Status values you will see

`sent`, `failed`, `delivered`, `undelivered`, `soft_bounce`, `hard_bounce`. Multiple `SMS_STATUS` events can fire for one message, so make your handler idempotent on `(message_id, status)`.

## Failure handling

- `401` — RFC 9457 problem, `title: API Authentication Failed`. The key is missing, wrong or lacks permission. Do not retry.
- `429` — back off. The request was dropped; the message was not sent.
- `4xx` validation — v2 returns `422` with an `issues[]` array naming the offending field. Fix and resend; this is safe because nothing was sent.
- `5xx` — the send state is unknown. Do **not** blind-retry. Query `GET /v2/sms` filtered by your `message_ref` first.
