# Architecture and execution state machine

**Proposed interfaces and transitions, not a deployed server.** The boundary evaluator is deterministic: it consumes observations and returns a decision. Only a separate dispatcher may contact a remote tool. Keep credentials out of evaluator memory where practical and never serialize them into its receipt.

## Modules and interfaces

| Module | Input → output | Responsibility and handoff |
|---|---|---|
| InventoryAdapter | connector/session alias → InventoryObservation | Enumerate the observed tool set, descriptor digests, collection time and completeness. A partial enumeration cannot establish absence. |
| CredentialBroker | credentialRef → ephemeral transport credential or error | Authenticate a principal; the reference itself proves nothing. Return principal alias and expiry to AuthenticationObserver. |
| GrantResolver | principal + family + asset + operation → GrantObservation | Use an authorized source of grants, return allowed/denied/unknown, never infer asset scope from tool visibility. |
| EffectClassifier | trusted mapping + descriptor digest → read/write/unknown | Treat remote read-only hints as input to review, never as the sole permission decision. |
| BoundaryEvaluator | OperationEnvelope + trusted clock + policy → Decision | Check freshness, equalities, action hash and approval binding; never execute. |
| ApprovalLedger | approval reference + action digest → consumed/rejected | Verify approver authority out of band, consume atomically immediately before dispatch. |
| Dispatcher | approved decision + ephemeral credential → EffectReceipt | Invoke once, enforce deadline and redact output. Unknown writes enter reconciliation. |
| AuditSink | sanitized Decision/EffectReceipt → durable acknowledgment | Persist correlation, reason, digests and observation references; failure before dispatch blocks writes. |

## State machine

```text
NEW -> INVENTORY_CHECKED -> AUTHENTICATED -> ASSET_AUTHORIZED -> CLASSIFIED
CLASSIFIED -- read --> READY
CLASSIFIED -- write --> AWAITING_APPROVAL -> APPROVED -> READY
READY -> AUDIT_RECORDED -> DISPATCHING -> SUCCEEDED | FAILED | INDETERMINATE
any pre-dispatch state -> BLOCKED
INDETERMINATE -> RECONCILED | NEEDS_OPERATOR
```

Every transition has one owner and a recorded predicate. Inventory completeness and freshness are required before tool availability is accepted. Authentication must identify the principal used by GrantResolver. An allowed grant must match every request dimension; wildcard grants require explicit policy expansion into the target asset, never implicit acceptance. Effect classification comes from a reviewed local mapping indexed by tool descriptor digest. A descriptor change blocks until reviewed.

At READY, recheck the session, times, principal and grant revision. Check the approval actionDigest against the canonical complete request and its principalRef against the authenticated principal. A write consumes its bound approval in a transaction with dispatch-intent persistence. A crash after intent but before a response is ambiguous; consuming approval does not prove the effect occurred. Restart must reconcile the intent through an authorized read, not reuse approval and send again. Transport-level idempotency may be added only when the adapter documents verified server semantics; this specification assumes none.

## Separation and threat handling

Connector configuration selects one family; a tool discovered under another connector cannot satisfy the inventory check. An inventory tool description saying “administrator access” is a string, not a grant. Authentication success for one principal cannot be reused after the broker rotates to another. An approved write to asset alpha cannot be rewritten to asset beta, even when the principal may access both.

The observation store is append-only at the logical level. New evidence supersedes an old observation without rewriting it; receipts retain the revision they evaluated. Public export replaces sensitive references with synthetic aliases and drops response bodies. Internal retention and encryption policy remain deployment decisions requiring review.

## Error ownership and consistency

Schema failures precede boundary evaluation and yield `SCHEMA_INVALID`. Evaluate gates in the state order so the primary error is stable; attach additional sanitized diagnostic codes only if collecting them does not invoke privileged operations. Unknown and denied are different outcomes. A dispatcher must reject a decision whose request digest differs from the current envelope. Network errors before send may allow one bounded read retry; errors after a write send are indeterminate unless the adapter can prove no side effect. Audit acknowledgments and remote success are separate facts.
