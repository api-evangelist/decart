---
name: Mint a scoped client token for a Decart realtime session
description: Create a short-lived, model- and origin-scoped ek_ token on your backend so a browser or mobile client can open a Decart realtime WebRTC session without ever seeing the permanent account key.
api: openapi/decart-platform-openapi-original.json
operations:
  - create_client_token_v1_client_tokens_post
  - get_realtime_quota_v1_realtime_quota_get
generated: '2026-08-01'
method: generated
source: openapi/decart-platform-openapi-original.json + https://docs.platform.decart.ai/getting-started/client-tokens
---

# Mint a scoped client token for a Decart realtime session

Realtime sessions run in the browser or on a device, which means the credential
travels to an untrusted client. Decart's answer is a two-tier key model: the
permanent `dct_` account key never leaves your backend, and each client session gets
a short-lived `ek_` token minted for it.

## Steps

1. **Check headroom first.** Call `get_realtime_quota_v1_realtime_quota_get`
   (`GET /v1/realtime/quota`). It returns `limit`, `active` and `remaining`
   concurrent realtime sessions for the account. If `remaining` is 0, fail fast in
   your own UI rather than minting a token the client cannot use. These values are
   account-specific and are not published as fixed numbers — read them, do not
   hardcode them.

2. **Mint the token** with `create_client_token_v1_client_tokens_post`
   (`POST /v1/client/tokens`), sending your `dct_` key in `x-api-key` and a
   `ClientTokenRequest` body:
   - `expiresIn` — seconds until expiry. **Defaults to 60.** Set it to the shortest
     value that covers your connection handshake, not the length of the session.
   - `allowedModels` — restrict the token to the models this session actually needs.
     Maximum 20 entries.
   - `allowedOrigins` — pin the token to your canonical web origins. Mismatched
     browser `Origin` headers are rejected at the realtime gateway, which is what
     stops a leaked token being replayed from another site. Maximum 20 entries.
   - `constraints.realtime.maxSessionDuration` — cap a single session in seconds.
     This is your cost ceiling per session.
   - `metadata` — an arbitrary object you can use to correlate the token with your
     own user or session record.

3. **Return only `apiKey` (and `expiresAt`) to the client.** The response is a
   `ClientTokenResponse` carrying `apiKey`, `expiresAt`, and the granted
   `permissions` and `constraints`. Ship the token, not your account key.

4. **Let it expire; do not try to revoke it.** There is no read, list, or revoke
   operation for client tokens — expiry is the only lifecycle. Expiry blocks *new*
   connections; an already-active realtime session keeps running until it
   disconnects. Size `maxSessionDuration` accordingly.

## Guardrails

- A client token cannot mint another client token. Attempting it returns `403 Cannot
  create client token from a client token`.
- `401` means the `x-api-key` header was missing or invalid.
- Never ship a `dct_` key in a frontend bundle, a mobile binary, or a public repo.
- Always set both `allowedModels` and `allowedOrigins`. An unscoped token is a full
  account credential with a 60-second fuse.

## Related

- `authentication/decart-authentication.yml` — the full two-tier auth profile
- `rate-limits/decart-rate-limits.yml` — concurrency quota and token limits
