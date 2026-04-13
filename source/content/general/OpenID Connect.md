---
title: "OpenID Connect"
tags:
  - security
  - identity
  - authentication
  - oauth
  - openid-connect
  - protocols
aliases:
  - OIDC
---

This page explains **OpenID Connect (OIDC)**: an identity and authentication layer that extends [[OAuth 2.0]]. It is aimed at anyone integrating sign-in with a standards-based provider or reading architecture docs that mention **OpenID Providers** and **Relying Parties**.

## Summary

- **OpenID Connect 1.0** is defined as an identity layer **on top of OAuth 2.0**; it lets a **client** verify **who** signed in and obtain **claims** about the end-user in a consistent, HTTP-friendly way.
- **OAuth 2.0** (RFC 6749) covers **authorization** and **access tokens** for APIs; it does **not** by itself standardize **end-user authentication** or identity payloads—OIDC fills that gap.
- A client requests OIDC by including the **`openid` scope** in the OAuth authorization request; the authorization server that implements OIDC is called an **OpenID Provider (OP)** and the client is a **Relying Party (RP)**.
- The primary artifact for authentication is the **ID Token**: a **JWT** carrying claims about the **authentication event** (and optionally the user); it is separate from the **access token** used for resource access.
- After tokens are issued, the RP may call the **UserInfo** endpoint with the access token to retrieve additional **claims** about the end-user.
- The core specification defines several **OAuth 2.0-based flows** (including **Authorization Code**, **Implicit**, and **Hybrid**); which flows are allowed in practice is often constrained by product documentation or security profiles.
- OP metadata such as endpoint URLs is usually discovered with **OpenID Connect Discovery** (well-known URL under the issuer), or supplied by static configuration.
- Clients are often registered with the OP using **Dynamic Client Registration** or equivalent admin tooling, depending on the platform.

## Details

### Roles

| Term | Meaning |
|------|---------|
| **OpenID Provider (OP)** | OAuth 2.0 **authorization server** that can authenticate the end-user and return OIDC tokens and claims. |
| **Relying Party (RP)** | OAuth 2.0 **client** that needs authenticated identity information from an OP. |
| **End-user** | The human signing in. |

### Tokens and endpoints

- **ID Token** (JWT): proves **authentication** to the RP; validate it per the OP’s keys and the rules in the core specification (issuer, audience, lifetime, signature, and so on).
- **Access token**: used to access **protected resources**; in OIDC, one important resource is often the **UserInfo** endpoint.
- **UserInfo endpoint**: returns claims for the end-user associated with the grant, when presented with a suitable access token.

### Claims

**Claims** are name/value assertions about the end-user or the authentication (for example subject identifier, issuer, and timestamps). OIDC defines standard claim names and allows profiles and extensions for richer directory-style attributes.

### Relationship to OAuth 2.0

OIDC **reuses** OAuth 2.0 endpoints and messages and adds parameters, scopes, and token types so sign-in is interoperable across vendors. For API-only delegation without identity assertions, plain OAuth 2.0 may suffice; for **login** and portable identity metadata, OIDC is the common choice.

## Related

- [[OAuth 2.0]]
- [[Azure App Service Authentication and Authorization]]

## Sources

- [OpenID Connect Core 1.0 incorporating errata set 2](https://openid.net/specs/openid-connect-core-1_0.html) — abstract, terminology, flows, ID Token and UserInfo (primary normative reference for core behavior).
- [OpenID Connect Discovery 1.0](https://openid.net/specs/openid-connect-discovery-1_0.html) — OpenID Provider metadata and discovery using a well-known URL.
- [OpenID Connect Dynamic Client Registration 1.0](https://openid.net/specs/openid-connect-registration-1_0.html) — registering client identifiers and related metadata with an OP.
- [The OAuth 2.0 Authorization Framework (RFC 6749)](https://www.rfc-editor.org/rfc/rfc6749.html) — underlying authorization grants, tokens, and endpoints OIDC extends.
- [JSON Web Token (JWT) (RFC 7519)](https://www.rfc-editor.org/rfc/rfc7519.html) — JWT structure referenced by the ID Token format.
- [AB/Connect Working Group – Specifications](https://openid.net/wg/connect/specifications) — index of OpenID Connect family specifications maintained by the OpenID Foundation.
