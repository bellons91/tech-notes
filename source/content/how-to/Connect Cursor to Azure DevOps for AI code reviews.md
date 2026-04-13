---
tags:
  - cursor
  - azure-devops
  - mcp
  - code-review
  - ai
  - gino
title: Un Titolo
---

Connecting Cursor to Azure DevOps through an [[Model Context Protocol|MCP]] server gives the model structured access to work items, pull requests, and commits. That context helps the agent align suggestions with the intent behind each task instead of staying generic.

## Add the Azure DevOps MCP server

1. Open Cursor’s MCP server list in the docs: [MCP servers (Cursor documentation)](https://cursor.com/docs/context/mcp#servers).
2. Find the **Azure DevOps** entry and use **Add to Cursor** (or the equivalent control shown there).

Cursor installs a server with a large set of ADO-related tools. It appears under **Settings → Tools & MCP** (labels can vary slightly by version).

## Authenticate with a PAT

Edit the installed server’s configuration and supply a **Personal Access Token** with scopes that match what you need (for example repositories and pull requests, work items, or both—grant only what you trust the agent to use).

Create or rotate tokens in Azure DevOps from your profile → **Personal access tokens**.

![[Pasted image 20260223180026.png]]

## Example: PR design review

With this enabled, I helped another developer work through a design flaw in a pull request: the agent connected to Azure DevOps, located the PR by id, walked the commits, and summarized the issue plus reasonable ways to address it.
