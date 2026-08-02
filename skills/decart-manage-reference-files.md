---
name: Upload and reuse a Decart reference image by file id
description: Upload a character or style reference once through the Files API, pass the returned file_ id by reference across generations and realtime sessions, and delete it before its TTL expires.
api: openapi/decart-platform-openapi-original.json
operations:
  - upload_file_v1_files_post
  - get_file_metadata_v1_files__file_id__get
  - delete_file_v1_files__file_id__delete
generated: '2026-08-01'
method: generated
source: openapi/decart-platform-openapi-original.json + https://docs.platform.decart.ai/changelog
---

# Upload and reuse a Decart reference image by file id

Re-encoding the same reference image on every call wastes bandwidth and latency,
which matters most in realtime sessions where the reference can be swapped mid-stream.
The Files API exists to upload it once and address it by id afterwards.

## Steps

1. **Upload** with `upload_file_v1_files_post` (`POST /v1/files`), a
   `multipart/form-data` body:
   - `file` (required) — the asset.
   - `ttl_seconds` — either a number of seconds between 60 and 2,592,000 (30 days),
     or the literal string `"persistent"` for no expiry. Omit it to get the platform
     default of 24 hours.

   The response is a `FileReferenceResponse` with `id` (a `file_` prefixed string),
   `filename`, `mime_type`, `size_bytes`, `created_at`, and `expires_at`.

2. **Reuse the id.** Pass the `file_` id by reference wherever a reference image is
   accepted — job submission and realtime `connect()` / `set()` / `setImage()` —
   instead of re-uploading the bytes.

3. **Check it is still alive** with `get_file_metadata_v1_files__file_id__get`
   (`GET /v1/files/{file_id}`) before relying on a long-lived id. `expires_at` is
   nullable: null means persistent.

4. **Delete early** with `delete_file_v1_files__file_id__delete`
   (`DELETE /v1/files/{file_id}`) when the reference is user-supplied and the user
   revokes it, or when you no longer need it. This returns `204` with no body — do
   not try to parse a response. Do not wait for the TTL when handling a deletion
   request.

## Choosing a TTL

- **Per-session user uploads** (a selfie a user just took): short TTL, and delete
  explicitly when the session ends. Storing a user's face longer than the session
  needs it is a privacy decision, not a performance one.
- **Your own brand or style assets**: `"persistent"`, uploaded once at deploy time.
- **Anything in between**: pick a TTL, don't rely on the 24-hour default by accident.

## Error handling

- `422` returns a `HTTPValidationError`. Check `detail[].loc`.
- There is no list operation — files are addressable only by the id you were
  handed. Persist the id yourself; if you lose it, the asset is unreachable until
  its TTL expires.

## Related

- `data-model/decart-data-model.yml` — the File entity and its relationships
- `conventions/decart-conventions.yml` — file reference semantics
