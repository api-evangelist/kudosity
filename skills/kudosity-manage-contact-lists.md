---
name: Manage contact lists and bulk imports
description: Create lists, add and update contacts, handle opt-outs, and run a bulk CSV import through the Kudosity Transmit SMS (v1) API.
api: openapi/_original/kudosity-transmit-sms-openapi-original.yml
operations:
  - POST /add-list.json
  - POST /add-field-to-list.json
  - POST /add-to-list.json
  - POST /edit-list-member.json
  - POST /optout-list-member.json
  - POST /delete-from-list.json
  - POST /add-contacts-bulk.json
  - POST /add-contacts-bulk-progress.json
  - GET /get-lists.json
---

# Manage contact lists and bulk imports

## Which API

Contacts and lists live **only on v1** (`https://api.transmitsms.com`), authenticated with HTTP Basic — `Authorization: Basic base64(api_key:api_secret)`. The v2 API has no contacts surface. If you are already holding a v2 API key for sending, you need the v1 key **and** secret as well for this flow.

v1 responses are `{"error": {"code": "...", "description": "..."}}` — string constants, not RFC 9457. Do not reuse a v2 problem-details parser here.

## Steps

1. **Create the list.** `POST /add-list.json`. Add custom fields with `POST /add-field-to-list.json` — up to 10, and they must exist before an import that populates them.
2. **Add contacts.**
   - One at a time: `POST /add-to-list.json`.
   - In bulk: `POST /add-contacts-bulk.json` with a CSV, then poll `POST /add-contacts-bulk-progress.json` until the import completes. Do not assume the import is finished when the upload call returns.
3. **Update.** `POST /edit-list-member.json`.
4. **Handle opt-outs.** `POST /optout-list-member.json` marks a contact opted out. This is not the same as `POST /delete-from-list.json`, which removes them entirely — **an opted-out contact must stay suppressed, so opt out, do not delete.** Under Australian anti-spam obligations, deleting the record loses the suppression.
5. **React to inbound opt-outs.** A recipient replying STOP or hitting an opt-out link raises an `OPT_OUT` webhook event on **v2**, and a `is_optout=yes` flag on the v1 reply callback. Whichever you consume, write it back to the list.

## Pagination

List-returning calls take `page` (default 1) and `max` (default 10, maximum 100), and return a `page: {count, number}` block. Walk `number` up to `count`.

## Reporting

Campaign and message reporting is also v1-only: `get-sms-stats.json`, `get-message-report.json`, `get-user-sms-sent.json`, `get-sms-delivery-status.json`.
