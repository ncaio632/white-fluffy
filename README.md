![white-fluffy](assets/header.svg)

# white-fluffy

### MCP integration boundaries and diagnostics

[English](README.md) · [Português (Brasil)](README.pt-BR.md) · [日本語](README.ja.md)


A technical reference structure for separating connector capability, authentication, asset scope and business operations.

## Scope

Integration reference, not an MCP server implementation. No account tokens, business asset identifiers or screenshots are published. Live capabilities require fresh inspection.

## Engineering notes

- [Architecture and invariants](docs/architecture.en.md)
- [Data contracts](docs/contracts.en.md)
- [Design decision record](docs/decisions.en.md)
- [Validation strategy](docs/validation.en.md)
- [Synthetic contract example](examples/contract.json)

## Reading guide

Start with architecture, inspect the contract example, then read the decision trade-off and validation matrix. Validation scenarios document what must be checked; they are not a claim that a public executable implementation passed those checks.

## Publication boundary

This technical edition excludes private records, account exports, workstation paths, conversation logs and historical backup blobs. The original operational archive remains a separate private asset.
