# ADR 001 — MCP integration boundaries and diagnostics

[README](../README.md)

## Context

A technical reference structure for separating connector capability, authentication, asset scope and business operations.

## Decision

Model connection state and asset authorization as separate checks.

## Consequences

Diagnosis has more states to report, but failures become attributable to capability, credentials or scope.

## Evidence boundary

Integration reference, not an MCP server implementation. No account tokens, business asset identifiers or screenshots are published. Live capabilities require fresh inspection.
