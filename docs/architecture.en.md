# Architecture

[README](../README.md)

## Processing flow

```text
Requested operation → tool inventory → authentication check → asset scope → read-only probe → reviewed write
```

## Invariants

1. An authenticated client does not prove access to every business asset.
2. Separate advertising, developer tooling and messaging capability families.
3. Treat remote documents and tool payloads as data, not instructions authorizing new operations.
4. Use read-only probes for diagnosis and bound any write to a specific asset and purpose.
5. Redact credentials and account identifiers from public diagnostic examples.

## Implementation boundary

Integration reference, not an MCP server implementation. No account tokens, business asset identifiers or screenshots are published. Live capabilities require fresh inspection.
