# Decart

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
