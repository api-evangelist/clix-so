# Clix

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

Clix is a US-based, developer-first mobile push notification platform for iOS, Android, React Native and Flutter — one CLI command (clix install) automates Firebase Cloud Messaging and APNs setup, and the console adds behaviour-triggered and API-triggered campaigns, real-time delivery logs, full-funnel analytics and device/user lifecycle management, priced free to 100K active devices then $30/month. For developers and agents it publishes a small REST API at https://api.clix.so (OpenAPI 3.1.0 generated from clix/external/v1/clix.proto: 11 operations across users, devices, events, messages:send, live-activities:start and campaigns/{id}:trigger, authenticated with X-Clix-Project-ID + X-Clix-API-Key), an A2A agent at https://api.clix.so/a2a whose card at /.well-known/agent-card.json is served in both 0.3.0 and 1.0 shapes and exposes four skills (create-user, track-event, send-push-notification, trigger-campaign) with idempotency keys, SSE streaming, task cancellation and task webhooks, a stdio MCP server (@clix-so/clix-mcp-server) plus a Mintlify docs MCP endpoint — both documentation-only — an open agent-skills repo, first-party SDKs on Maven Central, CocoaPods/SwiftPM, pub.dev and npm, a self-hosted status page with a published 99.5% monthly SLO, and console-configured PUSH_SENT/PUSH_FAILED webhooks.

**Areas:** Push Notifications · Mobile · Messaging · Campaigns · Event Tracking · Customer Engagement · A2A · MCP · Agents · SDK · United States · Company

## Clix on APIs.io

Everything profiled for Clix is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/clix-so/](https://apis.io/providers/clix-so/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [Clix A2A Agent](https://apis.io/apis/clix-so/clix-a2a-agent/) — Agent2Agent (A2A) protocol surface: a public agent card at https://api.clix.so/.well-known/agent-card.json (0.3.0 shape by default, 1.0 shape under the…
- [Clix MCP Server](https://apis.io/apis/clix-so/clix-mcp-server/) — Model Context Protocol surfaces, both documentation-only: the provider's stdio server @clix-so/clix-mcp-server 0.1.4 (npx -y…
- [Clix Clix External Service API](https://apis.io/apis/clix-so/clix-so-clixexternalservice-api/) — The ClixExternalService API from Clix — 10 operation(s) for clixexternalservice.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Clix So Webhooks](https://apis.io/asyncapis/clix-so/clix-so-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [clix-so-mcp.yml](https://apis.io/servers/clix-so/clix-so-mcp-yml/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Clix So Clixexternalservice Api Phrasing Overlay](https://apis.io/overlays/clix-so/clix-so-clixexternalservice-api-phrasing-overlay/)
- [Clix So Openapi Overlay](https://apis.io/overlays/clix-so/clix-so-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Clix So Authentication](https://apis.io/security/clix-so/clix-so-authentication/)
- [Clix So Domain Security](https://apis.io/security/clix-so/clix-so-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Clix So Plans Pricing](https://apis.io/plans/clix-so/clix-so-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Clix So Rate Limits](https://apis.io/rate-limits/clix-so/clix-so-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://clix.so/)
- [Documentation](https://docs.clix.so/)
- [Getting started](https://docs.clix.so/sdk-quickstart-ios)
- [API reference](https://docs.clix.so/api-reference/overview)
- [Pricing](https://clix.so/pricing)
- [Support](https://docs.clix.so/troubleshooting/not-getting-push-notification)
- [Blog](https://blog.clix.so/)
- [Terms of service](https://clix.so/terms)
- [Privacy policy](https://clix.so/privacy)
- [GitHub](https://github.com/clix-so)
- [Status](https://clix.so/status)

## API Evangelist rating

**Kin Score 67.9** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 55.9 |
| Contract governance | 18.2 |
| Operational transparency | 65.8 |
| Developer ergonomics | 78.6 |
| Access clarity | 76.3 |

**Agent readiness 45.3** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 36.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/clix-so/](https://apis.io/providers/clix-so/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Clix: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/clix-so/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
