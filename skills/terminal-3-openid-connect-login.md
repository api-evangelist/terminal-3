---
name: Authenticate a user with OpenID Connect
description: Run the Terminal 3 OpenID Connect flow — authorize, exchange a token, and read the userinfo and social connections.
api: openapi/terminal-3-openapi.yml
operations: [openidcAuthorize, createOpenidcToken, getOpenidcUser, getOpenidcUserSocialConnections]
x-provenance:
  method: generated
  source: openapi/terminal-3-openapi.yml
  generated: '2026-07-21'
---

# Authenticate a user with OpenID Connect (Terminal 3 OpenID Connect V1)

Operating instructions for the Terminal 3 OpenID Connect authentication flow. Every
operationId is verified against `openapi/terminal-3-openapi.yml`. A v2 token/userinfo pair
also exists (`createOpenidcTokenV2`, `getOpenidcUserV2`).

## Auth
- Base server: `https://staging.terminal3.io`.
- The token and userinfo endpoints follow OpenID Connect semantics; protected calls use a
  bearer access token. See `authentication/terminal-3-authentication.yml`.

## Steps
1. **Authorize** — `GET /v1/openidc/authorize` (`openidcAuthorize`). Begins the OIDC
   authorization flow and returns/redirects with an authorization response.
2. **Exchange for a token** — `POST /v1/openidc/token` (`createOpenidcToken`). Trade the
   authorization result for access/ID tokens. (Use `POST /v2/openidc/token`
   `createOpenidcTokenV2` for the v2 surface.)
3. **Read userinfo** — `GET /v1/openidc/user` (`getOpenidcUser`).
4. **Read social connections** — `GET /v1/openidc/user/social_connections`
   (`getOpenidcUserSocialConnections`).

## Error handling
- `400` on the token endpoint → malformed token request (see `errors/terminal-3-problem-types.yml`).
- `401` on userinfo → missing/invalid access token.
