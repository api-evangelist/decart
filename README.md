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

Decart is an AI research lab and API platform building real-time world models — foundation models that
generate and transform video frame-by-frame as they are watched. The Decart API Platform exposes the Lucy
family of realtime and batch video/image models plus the Oasis promptable world model through three
surfaces: a Realtime API (WebRTC, LiveKit-managed) that edits a live camera or video stream with text
prompts and reference images, a Queue API that submits asynchronous video jobs and polls them to
completion, and a Process API for synchronous image editing.

- Website — https://decart.ai/
- Developer platform — https://platform.decart.ai/
- Documentation — https://docs.platform.decart.ai/
- Status — https://status.decart.ai/
- GitHub — https://github.com/DecartAI

## What is captured here

| Artifact | Where | Method |
|---|---|---|
| OpenAPI 3.1 (API host, 55 ops) | `openapi/decart-api-openapi-original.json` | searched — `https://api.decart.ai/openapi.json` |
| OpenAPI 3.1 (curated, 20 ops) | `openapi/decart-platform-openapi-original.json` | searched — `https://docs.platform.decart.ai/openapi.json` |
| A2A Agent Card (near-conformant) | `a2a/` | probed — `/.well-known/agent-card.json` |
| MCP server (3 tools, unauthenticated) | `mcp/` | searched — live `tools/list` |
| Tool crosswalk | `mcp/decart-tool-crosswalk.yml` | derived |
| Provider-published Agent Skill + 5 generated | `skills/` | searched + generated |
| gRPC proto3 (Oasis action-to-video) | `grpc/` | searched — `decart-oasis` sdist |
| llms.txt | `llms/` | searched |
| Packages / SDKs (8 first-party) | `packages/` | searched |
| Pricing plans, rate limits | `plans/`, `rate-limits/` | searched / derived |
| Authentication, conventions, errors, lifecycle, changelog | `authentication/`, `conventions/`, `errors/`, `lifecycle/`, `changelog/` | searched / derived |
| Conformance, data model, examples, sandbox, overlay, well-known | `conformance/`, `data-model/`, `examples/`, `sandbox/`, `overlays/`, `well-known/` | derived / searched |
| Domain security, agentic access | `security/`, `agentic-access/` | probed / generated |

## Notable findings

- **The real spec is on the API host.** `https://api.decart.ai/openapi.json` serves a 55-operation
  FastAPI-generated document — including model aliases and preview routes — that is roughly three times
  the curated 20-operation spec on the docs host. Both are captured.
- **The MCP server is a documentation server, not an API wrapper.** All three tools search or query the
  docs; none calls `api.decart.ai`. The tool crosswalk records a complete surface divergence: 0 of 20
  REST operations has a tool.
- **Decart publishes its own Agent Skill** at `/.well-known/agent-skills/decart/skill.md`, linked from
  its agent card — a genuinely rare provider-authored agent surface. Saved verbatim.
- **No idempotency contract, no webhooks, no RFC 9457.** Job completion is discovered only by polling,
  and a retried submit is a second billable job.
- **Model retirement is real but ungoverned.** Two production model families were retired in 2026 with a
  named migration target, announced in the changelog — but there is no deprecation policy page, no
  Sunset header, and retired routes are removed rather than flagged `deprecated` in the spec.
- **No security.txt, no trust centre, no named certifications.** Probed across four hosts; all 404.
