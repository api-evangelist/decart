# Decart

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

Decart is an AI research lab and API platform building real-time world models — foundation models that generate and transform video frame-by-frame as they are watched. Its Decart API Platform (platform.decart.ai) exposes the Lucy family of realtime and batch video/image models plus the Oasis promptable world model through three surfaces: a Realtime API that edits a live WebRTC camera or video stream with text prompts and reference images, a Queue API that submits asynchronous video jobs and polls them to completion, and a Process API for synchronous image editing. The platform ships first-party JavaScript, Python, Swift and Android SDKs, ephemeral client tokens for browser and mobile apps, a Files API for reusable reference images, and a gRPC action-to-video session protocol for Oasis 3 Preview. Pricing is pay-as-you-go and metered per generated second (video and realtime) or per generation (images).

**Areas:** Artificial Intelligence · Machine Learning · Video · Video Generation · Video Editing · Image Editing · Real-Time · Generative AI · World Models · Streaming · WebRTC · Media

## Decart on APIs.io

Everything profiled for Decart is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/decart/](https://apis.io/providers/decart/)** — or go straight to one of the APIs or properties below.

### APIs (10)

- [Decart Oasis Action-to-Video (gRPC)](https://apis.io/apis/decart/decart-oasis-a2v/) — A gRPC session protocol for Oasis 3 Preview, Decart's promptable real-time world model. A client initializes a session, sets a scene with a text prompt,…
- [Decart Documentation MCP Server](https://apis.io/apis/decart/decart-docs-mcp/) — A hosted, unauthenticated Model Context Protocol server at docs.platform.decart.ai/mcp that exposes the Decart API Platform documentation to agents. Three…
- [Decart Client API](https://apis.io/apis/decart/decart-client-api/) — The Client API from Decart — 1 operation(s) for client.
- [Decart Files API](https://apis.io/apis/decart/decart-files-api/) — The Files API from Decart — 2 operation(s) for files.
- [Decart Generate API](https://apis.io/apis/decart/decart-generate-api/) — The Generate API from Decart — 4 operation(s) for generate.
- [Decart Jobs API](https://apis.io/apis/decart/decart-jobs-api/) — The Jobs API from Decart — 43 operation(s) for jobs.
- [Decart Models API](https://apis.io/apis/decart/decart-models-api/) — The Models API from Decart — 1 operation(s) for models.
- [Decart Realtime API](https://apis.io/apis/decart/decart-realtime-api/) — The realtime video transformation surface. A client opens a WebRTC session (LiveKit-managed transport) against a Lucy realtime model and streams camera or…
- [Decart Verify API](https://apis.io/apis/decart/decart-verify-api/) — The Verify API from Decart — 1 operation(s) for verify.
- [Decart Watch Stream API](https://apis.io/apis/decart/decart-watch-stream-api/) — The Watch Stream API from Decart — 1 operation(s) for watch stream.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [decart-api-platform-docs](https://apis.io/servers/decart/decart-api-platform-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Decart Agentic Access](https://apis.io/agentic-access/decart/decart-agentic-access/)

#### Collections (2)

Postman and Open Collection request collections.

- [Decart API](https://apis.io/collections/decart/open-decart-api-openapi-original/)
- [Decart API](https://apis.io/collections/decart/open-decart-platform-openapi-original/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Decart Api Overlay](https://apis.io/overlays/decart/decart-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Decart Authentication](https://apis.io/security/decart/decart-authentication/)
- [Decart Domain Security](https://apis.io/security/decart/decart-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Decart Plans Pricing](https://apis.io/plans/decart/decart-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Decart Rate Limits](https://apis.io/rate-limits/decart/decart-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://decart.ai/)
- [Documentation](https://docs.platform.decart.ai/)
- [Getting started](https://docs.platform.decart.ai/getting-started/quickstart)
- [API reference](https://docs.platform.decart.ai/api-reference/lucy-25)
- [Pricing](https://docs.platform.decart.ai/getting-started/pricing)
- [Sign up](https://platform.decart.ai/sign-in)
- [Changelog](https://docs.platform.decart.ai/changelog)
- [Blog](https://decart.ai/blog)
- [Terms of service](https://docs.platform.decart.ai/resources/terms-of-service)
- [Privacy policy](https://docs.platform.decart.ai/resources/privacy-policy)
- [GitHub](https://github.com/DecartAI)
- [Status](https://status.decart.ai/)

## API Evangelist rating

**Kin Score 54.5** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 44.0 |
| Contract governance | 4.5 |
| Operational transparency | 42.1 |
| Developer ergonomics | 75.0 |
| Access clarity | 76.3 |

**Agent readiness 34.7** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | derived (partial credit) |
| Event Surface Described | — |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | near-conformant (partial credit) |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | — |

**Regulatory alignment 22.7** — AI & Biometrics

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/decart/](https://apis.io/providers/decart/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Decart: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/decart/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
