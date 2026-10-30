# Kudosity

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Kudosity is an Australian business messaging platform — formerly Burst SMS / TransmitSMS — running two live public REST APIs on two hosts. The Transmit Message API (v2) covers SMS, MMS, WhatsApp and RCS with API-managed webhooks and sender registration; the Transmit SMS API (v1) carries contacts, lists, dedicated virtual numbers, keywords, email-to-SMS and all reporting. Both share one account, one set of senders and one bill. Both ship public OpenAPI documents. What makes Kudosity unusual for its size is the agent-native surface layered on top: a hosted MCP server whose tools/list answers without credentials, llms.txt on both the docs and marketing hosts with per-section fan-out, and five published agent integrations — a Claude Code plugin, a GitHub Copilot extension, a Gemini CLI extension, an OpenClaw channel plugin and an SMS GitHub Action — all open source in a public GitHub organization. RCS is in beta; there is no voice product, no sandbox and no idempotency key.

**Areas:** Messaging · SMS · MMS · RCS · WhatsApp · Communications · CPaaS · Webhook · MCP · Agent-Native · Australia · Notification

## Kudosity on APIs.io

Everything profiled for Kudosity is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/kudosity/](https://apis.io/providers/kudosity/)** — or go straight to one of the APIs or properties below.

### APIs (12)

- [Kudosity Account API](https://apis.io/apis/kudosity/kudosity-account-api/) — The Account API from Kudosity — 1 operation(s) for account.
- [Kudosity Contacts & Lists API](https://apis.io/apis/kudosity/kudosity-contacts-lists-api/) — The Contacts & Lists API from Kudosity — 9 operation(s) for contacts & lists.
- [Kudosity Email SMS API](https://apis.io/apis/kudosity/kudosity-email-sms-api/) — The Email SMS API from Kudosity — 2 operation(s) for email sms.
- [Kudosity Keywords API](https://apis.io/apis/kudosity/kudosity-keywords-api/) — The Keywords API from Kudosity — 3 operation(s) for keywords.
- [Kudosity MMS API](https://apis.io/apis/kudosity/kudosity-mms-api/) — The primary method of sending MMS
- [Kudosity Numbers API](https://apis.io/apis/kudosity/kudosity-numbers-api/) — The Numbers API from Kudosity — 4 operation(s) for numbers.
- [Kudosity RCS API](https://apis.io/apis/kudosity/kudosity-rcs-api/) — The RCS API from Kudosity — 3 operation(s) for rcs.
- [Kudosity Reporting API](https://apis.io/apis/kudosity/kudosity-reporting-api/) — The Reporting API from Kudosity — 11 operation(s) for reporting.
- [Kudosity Senders API](https://apis.io/apis/kudosity/kudosity-senders-api/) — The Senders API from Kudosity — 4 operation(s) for senders.
- [Kudosity SMS API](https://apis.io/apis/kudosity/kudosity-sms-api/) — The primary method of sending SMS. You can elect to pass us the recipient numbers from your database each time you make an API call. In order to send to a…
- [Kudosity Webhook API](https://apis.io/apis/kudosity/kudosity-webhook-api/) — Our webhooks API allows you to subscribe to events for SMS, MMS, and RCS messages. Using them requires you to have URLs (https) configured on your account…
- [Kudosity Whats App API](https://apis.io/apis/kudosity/kudosity-whats-app-api/) — The Whats App API from Kudosity — 2 operation(s) for whats app.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Kudosity Webhooks](https://apis.io/asyncapis/kudosity/kudosity-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Kudosity](https://apis.io/servers/kudosity/kudosity/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Kudosity Agentic Access](https://apis.io/agentic-access/kudosity/kudosity-agentic-access/)

#### Collections (2)

Postman and Open Collection request collections.

- [Transmit Message API](https://apis.io/collections/kudosity/postman-kudosity-transmit-message-openapi-original/)
- [Transmit SMS API](https://apis.io/collections/kudosity/postman-kudosity-transmit-sms-openapi-original/)

#### Overlays (12)

OpenAPI overlays, including conversational phrasing for each operation.

- [Kudosity Account Api Overlay](https://apis.io/overlays/kudosity/kudosity-account-api-overlay/)
- [Kudosity Contacts Lists Api Overlay](https://apis.io/overlays/kudosity/kudosity-contacts-lists-api-overlay/)
- [Kudosity Email Sms Api Overlay](https://apis.io/overlays/kudosity/kudosity-email-sms-api-overlay/)
- [Kudosity Keywords Api Overlay](https://apis.io/overlays/kudosity/kudosity-keywords-api-overlay/)
- [Kudosity Mms Api Overlay](https://apis.io/overlays/kudosity/kudosity-mms-api-overlay/)
- [Kudosity Numbers Api Overlay](https://apis.io/overlays/kudosity/kudosity-numbers-api-overlay/)
- [Kudosity Rcs Api Overlay](https://apis.io/overlays/kudosity/kudosity-rcs-api-overlay/)
- [Kudosity Reporting Api Overlay](https://apis.io/overlays/kudosity/kudosity-reporting-api-overlay/)
- [Kudosity Senders Api Overlay](https://apis.io/overlays/kudosity/kudosity-senders-api-overlay/)
- [Kudosity Sms Api Overlay](https://apis.io/overlays/kudosity/kudosity-sms-api-overlay/)
- [Kudosity Webhook Api Overlay](https://apis.io/overlays/kudosity/kudosity-webhook-api-overlay/)
- [Kudosity Whatsapp Api Overlay](https://apis.io/overlays/kudosity/kudosity-whatsapp-api-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Kudosity Authentication](https://apis.io/security/kudosity/kudosity-authentication/)
- [Kudosity Domain Security](https://apis.io/security/kudosity/kudosity-domain-security/)
- [Kudosity Trust Center](https://apis.io/security/kudosity/kudosity-trust-center/)
- [Kudosity Vulnerability Disclosure](https://apis.io/security/kudosity/kudosity-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Kudosity Plans](https://apis.io/plans/kudosity/kudosity-plans/)

#### Rate limits (1)

Published request limits.

- [Kudosity Rate Limits](https://apis.io/rate-limits/kudosity/kudosity-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://kudosity.com)
- [Documentation](https://developers.kudosity.com/docs)
- [Getting started](https://developers.kudosity.com/docs/getting-started)
- [API reference](https://developers.kudosity.com/reference)
- [Pricing](https://kudosity.com/pricing)
- [Sign up](https://kudosity.com/trial)
- [Support](https://help.kudosity.com/s/)
- [Changelog](https://developers.kudosity.com/changelog)
- [Blog](https://kudosity.com/resources/articles)
- [Security](https://trust.kudosity.com/)
- [Compliance](https://trust.kudosity.com/)
- [Terms of service](https://kudosity.com/legal/terms-and-conditions)
- [Privacy policy](https://kudosity.com/legal/privacy-policy)
- [GitHub](https://github.com/kudosity)

## API Evangelist rating

**Kin Score 57.6** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 59.2 |
| Contract governance | 4.5 |
| Operational transparency | 50.0 |
| Developer ergonomics | 39.9 |
| Access clarity | 92.1 |

**Agent readiness 47.1** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | verified |
| MCP Server | verified |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 30.0** — Telecommunications

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/kudosity/](https://apis.io/providers/kudosity/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Kudosity: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/kudosity/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
