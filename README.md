# Scro Orphan Desk

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

Scro Orphan Desk is a machine-only "Intent Echo resurrection desk" served from dualregistry.dev and operated, by its own account, as an AI agent desk for an individual (the operator named in its agent card); the legacy host orphan-desk-echo.vercel.app serves the same bytes. It indexes expired zero-fill on-chain swap intents (CoW Protocol orders and Across deposits on Ethereum, Arbitrum and Base) as "Resurrection Echoes", publishes the open book free as JSON (index.json, stats.json, fill_hint.json, PROMO.json, ORPHANDUST.json) with the executable legs sealed, and sells the unsealed echo to agents through an x402 v1 HTTP 402 paywall — a finder's fee in basis points settled in USDC on Base (USDT on BSC and both on Ethereum accepted at settlement) to one published receive wallet, or a flat $0.50 "OrphanDust" unlock credit. A small OBO fee-negotiation API (quote, counter, settle, structured feedback) sits beside it. Every surface is machine-first: a served OpenAPI 3.0.3 stub (7 operations), an A2A 0.3.0 agent card at the canonical well-known path (conformant in shape, though it advertises no JSON-RPC A2A endpoint), ai-plugin.json, llms.txt, an x402 discovery document, a JSON Schema for fee quotes, and an "mcp.json" that is a tool manifest rather than an MCP server. There is no signup, no OAuth, no SDK, no terms or privacy page, and — by design — no human support channel.

**Areas:** AI Agents · x402 · A2A · DeFi · Cryptocurrency · Stablecoins · Payments · Intent Trading · Machine Economy · Agent-Native

## Scro Orphan Desk on APIs.io

Everything profiled for Scro Orphan Desk is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/dualregistry-dev/](https://apis.io/providers/dualregistry-dev/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [Scro Orphan Desk A2A agent card](https://apis.io/apis/dualregistry-dev/a2a-agent/) — An A2A 0.3.0 agent card served at https://dualregistry.dev/.well-known/agent-card.json (and byte-identical at /agent-card.json, on www. and on the legacy…
- [Scro Orphan Desk Echo API](https://apis.io/apis/dualregistry-dev/dualregistry-dev-echo-api/) — The Echo API from Scro Orphan Desk — 1 operation(s) for echo.
- [Scro Orphan Desk Index.json API](https://apis.io/apis/dualregistry-dev/dualregistry-dev-index-json-api/) — The Index.json API from Scro Orphan Desk — 1 operation(s) for index.json.
- [Scro Orphan Desk Orphandust API](https://apis.io/apis/dualregistry-dev/dualregistry-dev-orphandust-api/) — The Orphandust API from Scro Orphan Desk — 1 operation(s) for orphandust.
- [Scro Orphan Desk Quote Fee API](https://apis.io/apis/dualregistry-dev/dualregistry-dev-quote-fee-api/) — The Quote Fee API from Scro Orphan Desk — 1 operation(s) for quote fee.
- [Scro Orphan Desk Settle Fee API](https://apis.io/apis/dualregistry-dev/dualregistry-dev-settle-fee-api/) — The Settle Fee API from Scro Orphan Desk — 1 operation(s) for settle fee.
- [Scro Orphan Desk Stats.json API](https://apis.io/apis/dualregistry-dev/dualregistry-dev-stats-json-api/) — The Stats.json API from Scro Orphan Desk — 1 operation(s) for stats.json.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [orphan_desk_intent_echo](https://apis.io/servers/dualregistry-dev/orphan-desk-intent-echo/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Dualregistry Dev Agentic Access](https://apis.io/agentic-access/dualregistry-dev/dualregistry-dev-agentic-access/)

#### JSON Schema (1)

The data models the API reads and writes.

- [Orphan Desk OBO fee quote / counter](https://apis.io/schemas/dualregistry-dev/dualregistry-dev-fee-quote.schema/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Dualregistry Dev Openapi Overlay](https://apis.io/overlays/dualregistry-dev/dualregistry-dev-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Dualregistry Dev Authentication](https://apis.io/security/dualregistry-dev/dualregistry-dev-authentication/)
- [Dualregistry Dev Domain Security](https://apis.io/security/dualregistry-dev/dualregistry-dev-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Dualregistry Dev Plans Pricing](https://apis.io/plans/dualregistry-dev/dualregistry-dev-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Dualregistry Dev Rate Limits](https://apis.io/rate-limits/dualregistry-dev/dualregistry-dev-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://dualregistry.dev/)
- [Documentation](https://dualregistry.dev/llms.txt)
- [Getting started](https://dualregistry.dev/AGENT.md)
- [API reference](https://dualregistry.dev/openapi.json)
- [Pricing](https://dualregistry.dev/PROMO.json)
- [GitHub](https://github.com/manhatton31-svg)

## API Evangelist rating

**Kin Score 33.6** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 60.7 |
| Contract quality | 45.1 |
| Contract governance | 18.2 |
| Operational transparency | 5.3 |
| Developer ergonomics | 42.3 |
| Access clarity | 31.6 |

**Agent readiness 30.6** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 15.2** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/dualregistry-dev/](https://apis.io/providers/dualregistry-dev/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Scro Orphan Desk: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/dualregistry-dev/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
