# Kudosity

Australian business messaging platform — formerly Burst SMS / TransmitSMS — selling SMS, MMS, WhatsApp and RCS to businesses across Australia and New Zealand. Two live public REST APIs, two public OpenAPI documents, a hosted MCP server, llms.txt on two hosts, and five published agent integrations.

- **Provider:** https://kudosity.com
- **Developer portal:** https://developers.kudosity.com
- **API reference:** https://developers.kudosity.com/reference
- **GitHub:** https://github.com/kudosity (9 public repos)
- **Trust centre:** https://trust.kudosity.com
- **Public API:** yes — self-service, published per-message pricing, 14-day free trial
- **Agent-native:** yes — MCP server, llms.txt, five agent plugins
- **Profiled:** 2026-07-11 · **Enriched:** 2026-07-27

> Enrichment on 2026-07-27 used canonical sources supplied directly by the provider (Rachel Harvey, Kudosity), then verified every one of them live. See [engagements/kudosity.md](https://github.com/kinlane/engagements) for the relationship record.

## The two APIs

Kudosity runs **two APIs on two hosts with two different credentials**, and neither is a superset of the other. This is the defining fact about integrating with them.

| | Transmit Message (v2) | Transmit SMS (v1) |
|---|---|---|
| Host | `api.transmitmessage.com` | `api.transmitsms.com` |
| Spec | OpenAPI 3.0.3 · 15 paths · 22 ops · 127 schemas | OpenAPI 3.0.0 · 35 paths · 35 ops · 0 schemas |
| Auth | API key, `x-api-key` header | HTTP Basic, `base64(key:secret)` |
| Channels | SMS, MMS, WhatsApp, RCS (beta) | SMS only |
| Webhooks | created and filtered through the API | configured in the UI or per send |
| Errors | RFC 9457 `application/problem+json` | `{"error": {"code", "description"}}` |
| Responses | JSON only | JSON or XML |
| Also carries | sender registration + verification | contacts, lists, custom fields, bulk CSV import, virtual numbers, keywords, email-to-SMS, **all reporting**, multi-recipient batch send, custom tracked-link domains |

Kudosity's guidance is to start new builds on v2 and keep v1 where you need multi-recipient sends or custom link domains. In practice most non-trivial integrations need **both**, because anything list-driven or reporting-shaped only exists on v1. Kudosity's own MCP server ships a `route-kudosity-operations` tool whose entire job is answering "which one do I call?" — a tell that the split is a real integration cost, not a footnote.

## Agent-native surface

This is where Kudosity punches above its weight. Very few providers this size have any of it, and Kudosity has all of it:

- **Hosted MCP server** at `https://developers.kudosity.com/mcp` — server name `Kudosity` v1.0, protocol `2025-06-18`, tools capability only. Its `tools/list` **answers without credentials**, which is rarer than it should be: an agent can discover the whole surface before it holds a key. Source is open at [github.com/kudosity/mcp](https://github.com/kudosity/mcp).
- **Shape:** it is a *spec navigator*, not one-tool-per-operation. Six live tools — `list-specs`, `list-endpoints`, `search-endpoints`, `get-endpoint`, `execute-request`, `route-kudosity-operations`. An agent discovers the endpoint from the OpenAPI, then calls the generic `execute-request` with a HAR object. Every one of the 57 REST operations is reachable; none has its own typed tool.
- **llms.txt** on both `developers.kudosity.com` and `kudosity.com`, with per-section and per-category fan-out — one of the better implementations in the catalog, not a token gesture.
- **Five agent integrations**, all open source: Claude Code plugin (`/plugin install kudosity-sms`), GitHub Copilot extension, Gemini CLI extension, OpenClaw channel plugin (ClawHub + npm), and an SMS GitHub Action on the Marketplace.
- **Five of the ten most recent changelog entries are agent surfaces**, not messaging features. The roadmap is visibly weighted toward agent-native distribution.

## What is strong

- Two real, parseable, published OpenAPI documents — reachable at stable URLs, no login, no shell page.
- RFC 9457 problem details on v2, with a written Error Registry, plus a documented error-constant table for v1.
- Cross-cutting conventions actually documented: authentication, rate limiting, pagination, timestamps, status codes, webhooks, content negotiation, and an error registry each get their own reference page.
- **Signed webhooks** — `x-transmitsms-signature`, HMAC-SHA256 keyed by the account secret, with a worked verification example.
- Ten typed webhook event types on v2 with server-side filtering on sender, status, `message_ref` and campaign.
- Real compliance posture: **ISO/IEC 27001:2022, SOC 2 Type 2, CSA STAR Level 1 (CAIQ v4)**, a pentest report and a published SLA, all behind a trust centre.
- Dated changelog, DNSSEC on the apex, HSTS on the docs host, TLS 1.3 everywhere.

## What is missing

Recorded as gaps, not guesses — each was probed:

- **No sandbox and no test mode.** No test/live key prefix, no magic test numbers, no simulator. Every send from a trial account is a real, billable message to a real handset. Combined with the MCP `execute-request` tool — annotated `destructiveHint: true` — an agent holding a key has **no non-billable way to rehearse a send**. This is the single largest agent-safety gap in the profile.
- **No idempotency key.** Not a header, not a parameter, not a mention. A retried send is a second message and a second charge. `message_ref` reconciles after the fact; it does not de-duplicate.
- **No operationIds** on any of the 57 operations in either spec. This is the cheapest high-value fix available: without them an agent cannot name an operation, code generators produce junk method names, and every workflow artifact has to be grounded on method + path instead.
- **No rate-limit response headers.** The 15 rps limit is documented in prose, but nothing on the wire tells a client its remaining budget before it trips a 429 — and a throttled message request is *dropped*, not queued.
- **No status page.** `status.kudosity.com` does not resolve; there is no uptime page on the site, the docs or the trust centre. An SLA exists with nothing to observe it against.
- **No deprecation or sunset policy.** v1 is described as "fully supported" with "no rush to migrate", but there is no dated end-of-life commitment, and no RFC 8594 `Sunset` support.
- **No `/.well-known/` surface at all** — no `security.txt` (RFC 9116), no `api-catalog`. Vulnerability reports route through the generic support ticket queue with no safe-harbour or timeline.
- **No first-party SDK** in any language. The agent plugins are excellent; there is no npm/PyPI/Maven/NuGet client library behind them. Integration is raw HTTP.
- **No AsyncAPI**, despite a rich, typed, filterable event surface that would map cleanly onto one.
- **Thin v1 contract.** The v1 OpenAPI declares zero component schemas and only `200` responses across all 35 operations — the error behaviour documented in prose is absent from the machine-readable contract.
- **Doc-vs-live drift on MCP.** The MCP page advertises ten capability names; the live server returns six, and exposes one (`route-kudosity-operations`) that the page does not mention.
- **Undeclared tags** in the v2 spec: operations are tagged `WhatsApp`, `RCS` and `Senders`, but only `SMS`, `MMS` and `Webhook` are declared in `tags[]`.

## Commercial

Published per-message SMS pricing in AUD ex GST: **Pay as you go 7.9¢, Growth 5.9¢, Scale 4.9¢, Enterprise on quote**. No monthly platform fee and no included volume is stated; rates are indicative and depend on volume and routing. MMS, WhatsApp and RCS pricing is not published. A **14-day free trial** is available at `kudosity.com/trial`. Self-service sign-up; the dashboard lives at `app.transmitsms.com`.

## Channel status (provider-confirmed 2026-07-27)

SMS, MMS and WhatsApp are **live**. RCS is in **beta** — the docs carry an explicit beta page, regional availability tracks Google's RBM rollout, and the surface is expected to move. There is **no voice product**. One open question: the marketing site publishes a **Viber** product page that the provider's channel list omits — either an unlisted live channel or a stale page.

## Artifacts in this repo

`openapi/` (both specs, verbatim) · `llms/` · `mcp/` (server manifest + tool crosswalk) · `skills/` (5 agent skills) · `agentic-access/` (57 classified operations) · `authentication/` · `conventions/` · `errors/` (problem types + v1 error codes) · `rate-limits/` · `asyncapi/` (webhook catalog) · `lifecycle/` · `changelog/` · `conformance/` · `plans/` · `packages/` · `data-model/` · `examples/` · `sandbox/` · `security/` (domain security, trust centre, vulnerability disclosure) · `well-known/` (recorded absence) · `screenshots/`

_Profiled and enriched by API Evangelist. Sources verified live 2026-07-27._
