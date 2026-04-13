---
title: "PFX Files"
tags:
  - certificate
  - pfx
  - security
  - pkcs12
---

A **PFX** file (often PKCS#12, `.pfx`/`.p12`) is a password-protected container that can hold a [[Certificate]] and its **private key** (and sometimes the full chain), used for TLS identities, code signing, and client authentication.

It identifies the **subject** bound to the certificate and is imported into keystores or app services to terminate TLS or authenticate callers.

A PFX file can be generated from other certificate formats, such as .pvk, .spc, or .cer, using tools like Pvk2Pfx or Advanced Installer. 

A PFX file is password protected and can be imported or exported to different devices or platforms.
