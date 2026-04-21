---
title: "Managed Identity"
tags:
  - az-204
  - azure
  - authentication
  - microsoft-entra
  - managed-identity
---

# Managed Identity

Managed identities provide an identity for applications to use when connecting to resources that support Microsoft Entra authentication. Azure manages the credentials; you do not put secrets for that identity in application code or configuration.

Typical uses include access from [[Azure App Service]], Azure Functions, virtual machines, and other Azure resources to services such as [[Azure Storage]], Key Vault, and SQL Database using Microsoft Entra token-based auth.

In the directory, a managed identity is represented by a [[Service Principal]] of type **Managed identity**; you grant that principal access like any other service principal.
