# Delivery backlog and acceptance gates

**Planning artifacts. None of these items is asserted complete.** Build in dependency order and keep the evaluator independent of any vendor adapter so synthetic verification is possible without accounts.

| Item | Deliverable and dependency | Acceptance criterion |
|---|---|---|
| WF-B1 | Versioned envelope parser and canonicalizer. | Valid fixtures parse; unknown fields and malformed hashes reject; duplicate keys reject; equivalent supported object orderings produce the same digest. |
| WF-B2 | Inventory/authentication observers after B1. | Partial, stale and session-mismatched observations block; credential material never reaches recorded receipts. |
| WF-B3 | Asset grant resolver and evaluator after B2. | An authenticated principal with a denied or unknown asset grant causes zero dispatches. Family, operation and principal mismatch each reject independently. |
| WF-B4 | Trusted effect map and approval ledger after B3. | Unknown tools block; expired, reused and mismatched approvals block; a write cannot bypass ledger consumption. |
| WF-B5 | Dispatcher, audit acknowledgment and reconciliation after B4. | Simulated timeout after remote effect creates an indeterminate receipt; restart does not replay. A read reconciliation can close the case without rewriting history. |
| WF-B6 | Redacted diagnostics and adapter qualification after B5. | Secret canaries do not appear in diagnostics; every supported tool has an observed descriptor, mapped effect and tested authorization boundary. |

For each item, submit a design change, contract examples, case IDs and measured evidence separately. A screenshot of “connected” is not acceptance evidence. Vendor-specific adapters must document their actual authentication mechanism, observed inventory method and grant evidence source during qualification; do not infer them from these generic names.

## Review checkpoints

The capability reviewer owns tool identity and effect classification. The authorization reviewer owns principal, grant and approval equality checks. The operation reviewer owns once-only dispatch and reconciliation boundaries. The evidence reviewer owns redaction and reproducibility. Each reviewer can stop a handoff with an unresolved assumption. Roles are described in `agents/`; they do not launch themselves or authorize account operations.

Before a real connector pilot, resolve the trusted clock source, observation expiry policy, approval identity verification and durable audit storage. Before any write pilot, demonstrate all approval negatives in the synthetic adapter and document a reconciliation read for that operation. If reconciliation is unavailable, keep write support disabled and expose a precise unsupported status.

## Change control

Adding a tool means reviewing its descriptor and effect map, adding a denied-asset case, and deciding whether existing approvals must be invalidated. Changing digest canonicalization increments the contract version and invalidates pending approvals. Schema widening requires negative tests for the new ambiguity; merely accepting more JSON is not backward compatibility evidence.

Release readiness requires measured cases, not a percentage inferred from document coverage. The public edition may remain a useful engineering reference without a runnable adapter. Keep any implementation gap visible in the evidence matrix and never fill it with private operational material.
