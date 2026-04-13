---
title: "Certificate"
tags:
  - certificate
  - security
  - tls
  - pki
---

An **X.509 certificate** is a signed document that binds a **public key** to an identity (subject) and validity period, issued by a certificate authority (CA) you or the platform trusts.

Certificates are used with TLS and other protocols. The **public** key is distributed widely; the **private** key must stay secret—often stored with the cert in a [[PFX file]] or an HSM / managed secret store.
