---
name: Edit a video with the Decart Queue API
description: Submit a video to a Lucy model with a text prompt and optional reference image, poll the job to completion, and download the rendered result.
api: openapi/decart-platform-openapi-original.json
operations:
  - lucy_2_5_job
  - get_job_v1_jobs__job_id__get
  - get_job_content_v1_jobs__job_id__content_get
  - resolve_model_aliases
generated: '2026-08-01'
method: generated
source: openapi/decart-platform-openapi-original.json + conventions/decart-conventions.yml
---

# Edit a video with the Decart Queue API

The Queue API is submit-and-poll. There are no webhooks and no callbacks — polling
`get_job_v1_jobs__job_id__get` is the only completion signal Decart publishes.

## Before you start

- Base URL is `https://api.decart.ai`.
- Authenticate every call with an `x-api-key` header carrying your permanent `dct_`
  account key. Never send a `dct_` key from a browser or mobile client — those use
  ephemeral `ek_` client tokens instead (see `decart-mint-client-token.md`).
- Video work is billed per generated second. `lucy-2.5` at 720p is $0.04/sec. Check
  `plans/decart-plans-pricing.yml` before running long inputs.

## Steps

1. **Pick and pin a model.** Submit against an explicit model id (`lucy-2.5`), not the
   rolling `lucy-latest` alias — aliases are repointed when a new generation ships.
   If you must accept an alias from configuration, resolve it first with
   `resolve_model_aliases` (`POST /v1/models/resolve`) so you log the canonical id you
   actually ran against.

2. **Submit the job** with `lucy_2_5_job` (`POST /v1/jobs/lucy-2.5`). The body is
   `multipart/form-data`:
   - `data` (required) — the video file to process.
   - `prompt` — the text instruction. Defaults to an empty string.
   - `reference_image` — optional character or style reference.
   - `seed` — integer 0 to 4294967295, for reproducibility.
   - `resolution` — `720p` (the only accepted value on this model).
   - `enhance_prompt` — defaults to `true`; leave it on unless you need literal prompt
     control.
   - `self_anchor` — defaults to `true` on `lucy-2.5`; re-anchors on the model's own
     latent.

   Keep the returned job id. **There is no idempotency key on this API** — a retried
   POST creates a second job and bills twice. Record the job id before any retry
   logic can fire, and never blind-retry a submission on a timeout.

3. **Poll** `get_job_v1_jobs__job_id__get` (`GET /v1/jobs/{job_id}`) until `status`
   is `completed`. Poll no faster than every 2 seconds.

4. **Download** the result with `get_job_content_v1_jobs__job_id__content_get`
   (`GET /v1/jobs/{job_id}/content`), which returns the rendered media bytes.

## Error handling

- `422` is the only error the spec declares on submission. The body is a
  `HTTPValidationError`: read `detail[].loc` for the offending field and
  `detail[].type` for the rule that failed.
- `401` means the `x-api-key` header was missing or invalid.
- No `429` and no `5xx` responses are declared. Treat anything outside `2xx`/`422`
  as an undocumented transport failure and back off exponentially — but do **not**
  resubmit the job unless you have confirmed via polling that the first submission
  never produced a job id.
- Job *failure* (as opposed to request failure) surfaces in the polled `status`
  field, not as an HTTP error. The published spec types the job response as an empty
  schema, so parse `status` defensively.

## Related

- `conventions/decart-conventions.yml` — the full submit/poll/fetch contract
- `errors/decart-problem-types.yml` — the error envelope
- `rate-limits/decart-rate-limits.yml` — quota mechanics
