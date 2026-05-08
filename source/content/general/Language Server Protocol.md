---
title: "Language Server Protocol"
tags:
  - developer-tools
  - language-server
  - lsp
  - editor-integration
  - json-rpc
  - protocol
aliases:
  - LSP
  - Language Server
---

This note captures the core ideas behind the Language Server Protocol (LSP): why it exists, how client and server exchange messages during editing, and what "capabilities" mean in practice.

## Summary

- LSP standardizes communication between development tools and language-specific servers so the same language intelligence can be reused across editors.
- A language server runs as a separate process and communicates with the client over JSON-RPC.
- After a file is opened, document state is treated as in-memory editor state and synchronized through protocol notifications.
- Typical flow includes open, change, diagnostics publication, definition lookup, and close notifications.
- LSP exchanges simple, language-neutral data like document URIs and cursor positions instead of language-specific compiler symbols.
- Capabilities allow each client and server to declare what requests and notifications they support, instead of assuming full protocol coverage.
- Integration details inside each editor are intentionally out of scope for the protocol and left to tool implementers.

## Details

### Why LSP exists

Without LSP, language teams and tool vendors often re-implement the same features (autocomplete, go to definition, hover docs) for each editor integration. LSP separates responsibilities:

- Language logic stays in the language server.
- Editor integration speaks a shared protocol.

This reduces duplicated implementation effort and improves portability of language features.

### Message flow in a normal editing session

A simplified request/notification flow:

1. Client sends `textDocument/didOpen`.
2. Client sends `textDocument/didChange` as edits happen.
3. Server publishes diagnostics through `textDocument/publishDiagnostics`.
4. Client requests symbol navigation with `textDocument/definition`.
5. Client sends `textDocument/didClose` when the document is closed.

The protocol example for "Go to Definition" uses a document URI and a position (`line`, `character`) as input and returns a URI plus range for the definition location.

### Why URIs and positions (not AST-level standardization)

LSP deliberately standardizes on text-document references and positions because those are language-neutral and easier to keep consistent across ecosystems. Standardizing compiler-domain concepts (for example AST nodes or resolved symbols) across many languages would be substantially harder and less interoperable.

### Capabilities and feature negotiation

Capabilities let each side declare support for specific features. For example:

- A server may support `textDocument/definition` but not `workspace/symbol`.
- A client may support "about to save" notifications, enabling servers to provide edits before save.

This negotiation model makes partial implementations practical and avoids requiring every server to support every feature.

### Benefits for both sides

- **Language providers:** implement language intelligence once and expose it across many tools.
- **Tool vendors:** add language support with less custom per-language work by integrating against one protocol.

## Related

- [[Model Context Protocol]]

## Sources

- [Language Server Protocol Overview](https://microsoft.github.io/language-server-protocol/overviews/lsp/overview/)
