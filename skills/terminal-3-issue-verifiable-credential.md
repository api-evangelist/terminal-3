---
name: Issue and store a verifiable credential
description: Use the Terminal 3 VC issuer API to create a credential proof, store an issued verifiable credential, and list issuer credentials.
api: openapi/terminal-3-openapi.yml
operations: [createIssuerCredentialsProof, storeIssuerCredential, getIssuerCredentials]
x-provenance:
  method: generated
  source: openapi/terminal-3-openapi.yml
  generated: '2026-07-21'
---

# Issue and store a verifiable credential (Terminal 3 VC V1)

Operating instructions for an agent issuing a W3C Verifiable Credential (VC) through the
Terminal 3 API. Every operationId below is verified against `openapi/terminal-3-openapi.yml`.

## Auth
- Default authentication is a **bearer JWT** (`Authorization: Bearer <token>`) — see
  `authentication/terminal-3-authentication.yml`.
- Base server: `https://staging.terminal3.io`.

## Steps
1. **Create the credential proof** — `POST /v1/vc/issuer/credentials/proof`
   (`createIssuerCredentialsProof`). Produces the cryptographic proof for the credential
   you intend to issue.
2. **Store the issued credential** — `POST /v1/vc/issuer/store` (`storeIssuerCredential`).
   Persists the issued verifiable credential on the issuer.
3. **Confirm / list issuer credentials** — `GET /v1/vc/issuer/credentials`
   (`getIssuerCredentials`) to verify the credential is present.

## Error handling
- On `401` re-check the bearer token (see `errors/terminal-3-problem-types.yml`).
- Terminal 3 supports multiple VC formats (SD-JWT VC, mDoc/ISO 18013-5, BBS+, ECDSA) via its
  `@terminal3/*` credential SDKs — match the format you request to the verifier's expectations.
