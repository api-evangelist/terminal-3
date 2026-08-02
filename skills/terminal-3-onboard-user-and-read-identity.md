---
name: Onboard a user and read their identity data
description: Create a Terminal 3 user, then read their wallet addresses and social data.
api: openapi/terminal-3-openapi.yml
operations: [createUser, getUserWalletAddresses, getUserSocialData]
x-provenance:
  method: generated
  source: openapi/terminal-3-openapi.yml
  generated: '2026-07-21'
---

# Onboard a user and read their identity data (Terminal 3 User V1)

Operating instructions for an agent that creates a Terminal 3 user and reads their
identity data. Every operationId is verified against `openapi/terminal-3-openapi.yml`.

## Auth
- `createUser` requires **both** the default bearer JWT **and** the `x-api-token` header
  (`x-api-token: <YOUR_KEY>`). Request a key from `enterprise@terminal3.io` or the self-serve
  claim page in the docs. See `authentication/terminal-3-authentication.yml`.
- Base server: `https://staging.terminal3.io`.

## Steps
1. **Create the user** — `POST /v1/user/create` (`createUser`). Include the `x-api-token`
   header. Keep the returned `user_id`.
2. **Read wallet addresses** — `GET /v1/user/{user_id}/wallet_addresses`
   (`getUserWalletAddresses`), substituting the `user_id` from step 1.
3. **Read social data** — `GET /v1/user/{user_id}/social_data` (`getUserSocialData`).

## Error handling
- `401` → missing/invalid bearer token or `x-api-token` (see `errors/terminal-3-problem-types.yml`).
- `404` → the `user_id` does not exist; do not construct it, use the value returned by `createUser`.
