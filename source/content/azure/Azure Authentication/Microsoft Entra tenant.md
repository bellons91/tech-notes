---
tags:
  - az-204
  - azure
  - MicrosoftEntra
---

To delegate Identity and Access Management functions to Microsoft Entra ID, an application must be registered with a #MicrosoftEntra tenant.

When you register an app in the Azure portal, you choose whether it is **Single tenant** (only accessible in your tenant) or **Multi-tenant** (accessible in other tenants).

If you register an application in the portal, an [[Application Object]] (the globally unique instance of the app) and a [[Service Principal]] object are automatically created in your home tenant.

You also have a globally unique ID for your app (the app or **client ID**). In the portal, you can then add secrets or certificates and scopes to make your app work, customize the branding of your app in the sign-in dialog, and more.
