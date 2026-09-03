---
name: Send a WhatsApp message with SMS fallback
description: Send a templated or free-form WhatsApp message through the Kudosity v2 API and fall back to SMS when WhatsApp cannot deliver.
api: openapi/_original/kudosity-transmit-message-openapi-original.yml
operations:
  - POST /v2/whatsapp/messages
  - GET /v2/whatsapp/messages
  - GET /v2/whatsapp/messages/{id}
  - POST /v2/webhook
---

# Send a WhatsApp message with SMS fallback

## Before you start

WhatsApp requires a registered and verified sender on a Meta Business Portfolio — that onboarding is a separate, days-long process outside the API. Confirm the sender is live before automating anything. Free-form messages are only allowed inside an open customer service window; outside it you must send an approved **template**.

## Steps

1. **Pick the content type.** `WhatsappContentType` is one of text, template, or custom. Template sends carry the template name plus variable mappings.
2. **Configure fallback.** The request accepts an `SMSFallback` block. When set, a WhatsApp message that cannot be delivered is re-sent as SMS — which bills as SMS and arrives from your SMS sender, not your WhatsApp identity. Say so in any user-facing confirmation.
3. **Send.** `POST /v2/whatsapp/messages`.
4. **Track.** Subscribe a webhook to `WHATSAPP_STATUS` (lifecycle `SENT` → `DELIVERED` → `READ`, or `FAILED`) and `WHATSAPP_INBOUND` for replies. Or poll `GET /v2/whatsapp/messages/{id}`.

## Failure handling

- `429` on send — WhatsApp-specific throttling on top of the account's 15 rps limit.
- `400` — most often a template that is not approved, or variables that do not match the approved template's placeholders. Fix the template mapping; do not retry unchanged.
- A `FAILED` event with fallback configured does not mean the customer was not contacted. Check for the fallback SMS before escalating.

## RCS is the same shape, with a caveat

`POST /v2/rcs/messages` mirrors this flow and also supports SMS fallback, plus `POST /v2/rcs/capabilities` to check whether a set of numbers can receive RCS at all — call it first and batch accordingly. **The RCS API is in beta**: expect the surface to move, and do not build unattended production flows on it yet.
