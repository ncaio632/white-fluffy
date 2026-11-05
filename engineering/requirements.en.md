# Requirements and trust boundaries

**Design specification; implementation and live connectivity are not demonstrated by this document.** The existing public edition is a reference structure. These requirements refine that structure into a buildable integration boundary without asserting any vendor's current endpoints, scopes or supported tools. All identifiers in fixtures are synthetic aliases.

## Outcome and scope

An operator should learn whether a requested operation is possible, authenticated, authorized for one asset, and explicitly approved when it changes state. The system must explain the first failed boundary without attempting the operation. “Connected” is never a sufficient decision. Tool discovery is an observation about a particular session and time; it cannot grant access or turn unknown permissions into permission.

The reference supports three conceptual families: advertising, developer tooling and business messaging. Their names describe isolation boundaries, not a claim of installed connectors. A connector adapter must map an observed tool to exactly one configured family. Credentials, permission grants and approvals must not silently cross families.

## Normative requirements

| ID | Required behavior | Failure observable by operator |
|---|---|---|
| WF-01 | Bind a requested tool to a fresh, complete inventory observation and descriptor digest for the selected connector session. | `INVENTORY_UNKNOWN`, `TOOL_UNAVAILABLE` or `EVIDENCE_STALE`; zero dispatches. |
| WF-02 | Resolve authentication through an opaque credential reference; report authenticated, unauthenticated and unknown separately. | `AUTH_REQUIRED` or `AUTH_UNKNOWN`; credentials absent from logs. |
| WF-03 | Verify the same principal, connector, family, asset and operation against an authoritative grant observation. | `ASSET_DENIED` or `GRANT_UNKNOWN`; login success is retained separately. |
| WF-04 | Reads require all preceding boundaries; writes also require explicit approval bound to the canonical action digest, asset, purpose and expiry. | `APPROVAL_REQUIRED`, `APPROVAL_MISMATCH` or `APPROVAL_EXPIRED`. |
| WF-05 | Treat descriptions, documents and returned text as untrusted data. Unknown effect classifications default to blocked. | `EFFECT_UNKNOWN`; instruction-like output causes no second action. |
| WF-06 | Record a redacted decision receipt and distinguish successful, failed and indeterminate effects. | `DISPATCH_UNKNOWN` when a timeout could follow a committed write. |
| WF-07 | Invalidate evidence on session change, principal change, grant change or descriptor change; consume an approval once. | A fresh evaluation is required; prior approval is not transferable. |
| WF-08 | Bound requests by deadline, result size and retry count; never automatically replay an uncertain write. | A terminal receipt with a stable error code, not an unbounded loop. |

## Constraints and decisions left to implementers

Inventory and authorization evidence have a proposed maximum age of five minutes for the synthetic profile. Production owners must choose and document a shorter or longer bound based on the connector's revocation behavior; this number is a design default, not a service guarantee. Compare timestamps using a trusted clock and reject future observations outside a documented skew allowance. The approval expiry must be no later than the earliest evidence expiry.

A request carries aliases and references, never raw tokens. A private credential broker resolves a reference immediately before transport. Public diagnostics contain no account mapping. A transport must enforce timeouts even if a remote tool ignores cancellation. Grant lookup failure stays unknown; it is not converted to an explicit denial or success.

Payload canonicalization, approval identity and adapter-specific permission proofs must be specified before implementation acceptance. Canonical action bytes are UTF-8 JSON with lexicographically sorted object keys, no insignificant whitespace, no duplicate keys and no non-finite numbers. Reject ambiguous numeric encodings; the proposed profile accepts integer payload numbers only. Hash these bytes with SHA-256 and bind the resulting digest to the request envelope. JSON Schema validates shape, not authority, time, digest recomputation or signature authenticity.

Completion means the planned matrix has measured evidence in an isolated test adapter and, separately, in any explicitly authorized connector environment. This edition does not supply either execution environment. It is not a campaign controller, messaging sender or universal MCP client.
