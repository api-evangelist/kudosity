---
name: Register and verify a sender number
description: Register a personal sender with Kudosity and complete the verification-code round trip before sending from it.
api: openapi/kudosity-transmit-message-openapi-original.yml
operations:
  - POST /v2/senders/registrations
  - GET /v2/senders/registrations
  - POST /v2/senders/registrations/{registration_id}/verifications
  - POST /v2/senders/registrations/{registration_id}/verifications/confirmation
  - DELETE /v2/senders/phone-numbers/{phone_number}
---

# Register and verify a sender number

A sender must exist and be verified before it can appear in the `sender` field of a send. This flow is human-in-the-loop by construction: the verification code goes to the phone's owner, not to the API caller.

## Steps

1. **Register.** `POST /v2/senders/registrations` with the phone number and registration type. Returns `201` with a `registration_id`. A `409` means the number is already registered — call `GET /v2/senders/registrations` and use the existing record rather than registering again.
2. **Request a code.** `POST /v2/senders/registrations/{registration_id}/verifications`. Returns `201`. The code is delivered to the number being registered.
3. **Pause for a human.** The agent cannot read the code. Surface the request to a person and wait. Do not loop on step 2 — it is rate limited (`429`) and each call sends another message.
4. **Confirm.** `POST /v2/senders/registrations/{registration_id}/verifications/confirmation` with the code the human supplied. `200` on success; `409` if the registration is in the wrong state; `422` if the code is malformed.
5. **Clean up if needed.** `DELETE /v2/senders/phone-numbers/{phone_number}` returns `204`. This is destructive and unrecoverable — require explicit confirmation from a human before calling it.

## Notes

- Sender registration semantics vary by country (Australia and New Zealand are the primary markets). Alphanumeric sender IDs and dedicated virtual numbers follow different paths; virtual number leasing lives on the **v1** API (`lease-number.json`), not v2.
- No idempotency key exists here either. Steps 1 and 2 both have real-world side effects on repeat.
