---
title: "Azure App Service on Linux"
tags:
  - azure
  - cloud
  - az-204
  - linux
  - azure-app-service
  - containers
---

# Azure App Service on Linux

You can choose to host a web app on Linux for supported application stacks.

You can run _custom_ Linux containers using **Web App for Containers**.

Natively, App Service on Linux supports several frameworks, such as:

- .NET
- Node.js
- Java
- Go
- Python
- PHP
- Ruby

If a framework is missing, you can deploy a custom container.

To see which runtimes are supported, use:

[[Azure App Service Scripts#List the available runtimes]]

## Known limitations

App Service on Linux **isn't supported on Shared pricing tier**.

When deployed to built-in images, your code and content are allocated a storage volume for web content, backed by Azure Storage. _The disk latency of this volume is higher_ and more variable than the latency of the container filesystem. Apps that require heavy read-only access to content files may benefit from the custom container option, which places files in the container filesystem instead of on the content volume.

Built-in authentication runs in a **separate sidecar container** on Linux; see [[Azure App Service Authentication and Authorization]].

## See also

- [[Azure App Service]]
- [[Azure App Service Plan]]
- [[Azure App Services Deployment Slots]] (auto-swap limitations on Linux)
