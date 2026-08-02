---
name: Run a virtual try-on job with Decart Lucy VTON
description: Dress a person in a video with a garment image or a text prompt using the Lucy VTON 3 batch job, then poll and download the result.
api: openapi/decart-platform-openapi-original.json
operations:
  - lucy_vton_3_job
  - lucy_vton_2_job
  - get_job_v1_jobs__job_id__get
  - get_job_content_v1_jobs__job_id__content_get
generated: '2026-08-01'
method: generated
source: openapi/decart-platform-openapi-original.json + https://docs.platform.decart.ai/models/realtime/virtual-try-on
---

# Run a virtual try-on job with Decart Lucy VTON

Virtual try-on is Decart's marquee commerce flow: put a shopper's video in, put a
garment reference in, get the shopper wearing it out. It runs on both the realtime
surface and the batch Queue API; this skill covers the batch path.

## Before you start

- Base URL `https://api.decart.ai`, `x-api-key` header with a `dct_` key.
- `lucy-vton-3` is the current generation, billed at $0.04 per generated second at
  720p on the batch surface.

## Steps

1. **Submit** with `lucy_vton_3_job` (`POST /v1/jobs/lucy-vton-3`), a
   `multipart/form-data` body carrying the source video as `data` plus a garment
   reference image and/or a text prompt.

2. **Poll** `get_job_v1_jobs__job_id__get` until `status` is `completed`, no faster
   than every 2 seconds.

3. **Download** with `get_job_content_v1_jobs__job_id__content_get`.

## Version pinning matters more here than anywhere else in the API

The VTON family has already retired a generation in production. In June 2026 Decart
stopped serving `lucy-2.1-vton` and its `lucy-vton` alias outright, and repointed
`lucy-vton-latest` from `lucy-vton-2` to `lucy-vton-3`. Retirement is announced in
the monthly changelog; there is **no published deprecation window and no Sunset
header**, and retired routes are removed rather than flagged `deprecated: true` in
the spec.

Practical consequences:

- Submit against `lucy_vton_3_job` (`/v1/jobs/lucy-vton-3`) explicitly. Do not build
  on `lucy_vton_latest_job` unless you actively want to be moved.
- `lucy_vton_2_job` (`/v1/jobs/lucy-vton-2`) is still served for pinned integrations,
  but it is the previous generation — treat it as a migration target, not a default.
- Subscribe a human to https://docs.platform.decart.ai/changelog. Since retirement is
  announced only there, that page is your entire early-warning system.

## Error handling

- `422` returns a `HTTPValidationError`; read `detail[].loc`.
- A `404` on a submit path you previously used successfully most likely means that
  model was retired. Check the changelog before assuming an outage.
- No idempotency key exists — a retried submit is a second billable job.

## Related

- `lifecycle/decart-lifecycle.yml` — the observed retirement record
- `changelog/decart-changelog.yml` — dated model launches and retirements
