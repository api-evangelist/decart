---
name: Edit an image synchronously with the Decart Process API
description: Send an image plus a text prompt to Lucy Image 2 and get the edited image bytes back in the same response, with no job to poll.
api: openapi/decart-platform-openapi-original.json
operations:
  - lucy_image_2_generate
  - lucy_image_latest_generate
generated: '2026-08-01'
method: generated
source: openapi/decart-platform-openapi-original.json + conventions/decart-conventions.yml
---

# Edit an image synchronously with the Decart Process API

The Process API is the only synchronous generation surface Decart publishes. It
returns image bytes directly instead of a job id, so there is nothing to poll.

## Before you start

- Base URL is `https://api.decart.ai`.
- Send your `dct_` account key in an `x-api-key` header.
- Billing is per generation: $0.01 at 480p, $0.02 at 720p for `lucy-image-2`.

## Steps

1. **Call** `lucy_image_2_generate` (`POST /v1/generate/lucy-image-2`) with a
   `multipart/form-data` body containing the source image, the text prompt, and the
   target resolution.

2. **Read the response as bytes.** The 200 response media type is `image/png`, not
   JSON. Do not attempt to JSON-parse a successful response — a JSON body means you
   are looking at a `422`.

3. **Prefer the pinned id.** `lucy_image_latest_generate`
   (`POST /v1/generate/lucy-image-latest`) is the rolling alias and will move when a
   new image generation ships. Use `lucy-image-2` explicitly for stable output.

## Reusing a reference image

If you are editing many images against the same reference, upload the reference once
with `upload_file_v1_files_post` and pass the returned `file_` id instead of
re-encoding the asset on every call. See `decart-manage-reference-files.md`.

## Error handling

- `422` returns a `HTTPValidationError` in `application/json`. Inspect
  `detail[].loc` and `detail[].type`.
- Content that violates the Acceptable Use Policy is rejected at generation time;
  handle the rejection and surface it to the user rather than retrying.
- There is no idempotency key. A retry is a second billable generation.

## Related

- `conventions/decart-conventions.yml`
- `errors/decart-problem-types.yml`
- `plans/decart-plans-pricing.yml`
