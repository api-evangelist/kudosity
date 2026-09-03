---
name: Choose between the v1 and v2 Kudosity APIs
description: Decide which Kudosity API to call for a given task, and which credential to present, before writing any integration code.
api: openapi/_original/kudosity-transmit-message-openapi-original.yml
operations: []
---

# Choose between the v1 and v2 Kudosity APIs

Kudosity runs two live APIs on two hosts with two different credentials. Neither is a superset. Getting this wrong is the most common integration mistake, and Kudosity's own MCP server ships a dedicated `route-kudosity-operations` tool for exactly this decision.

## The split

| Task | API | Host | Auth |
|---|---|---|---|
| Send SMS | either | v2 preferred | `x-api-key` (v2) |
| Send MMS, WhatsApp, RCS | **v2 only** | `api.transmitmessage.com` | `x-api-key` |
| Manage webhooks via API | **v2 only** | `api.transmitmessage.com` | `x-api-key` |
| Sender registration + verification | **v2 only** | `api.transmitmessage.com` | `x-api-key` |
| Multi-recipient send in one request | **v1 only** | `api.transmitsms.com` | HTTP Basic |
| Contacts, lists, custom fields, bulk import | **v1 only** | `api.transmitsms.com` | HTTP Basic |
| Virtual numbers, keywords, email-to-SMS | **v1 only** | `api.transmitsms.com` | HTTP Basic |
| Reporting and campaign stats | **v1 only** | `api.transmitsms.com` | HTTP Basic |
| Custom tracked-link domain | **v1 only** | `api.transmitsms.com` | HTTP Basic |
| XML responses | **v1 only** | `api.transmitsms.com` | HTTP Basic |

## Rules

- Start new work on **v2**. It is the API that gets new channels.
- Anything list-driven, number-leasing, or reporting-shaped needs **v1** as well. Plan to hold both credentials from the start rather than discovering it mid-build.
- v1 is not deprecated and carries no published sunset date — but it also gets no new channels.
- Both APIs share one account: same senders, same billing, same reporting UI. A contact list built on v1 is addressable by a v2 send.

## Error shapes differ

v2 returns RFC 9457 `application/problem+json` with `type`/`title`/`status`/`detail`. v1 returns `{"error": {"code": "AUTH_FAILED", "description": "..."}}`. Write two handlers.
