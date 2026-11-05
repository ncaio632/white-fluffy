# End-to-end operator runbook

**Manual integration procedure for a future adapter; no live tools are assumed.** Run the synthetic path first. A deployment owner supplies approved connector configuration, credential broker, asset mapping, clock and audit destination. Stop if any of those are missing; do not substitute fixture aliases into a real account.

## Preparation

1. Record the implementation revision, policy revision, environment alias and test case ID. Use an isolated adapter with an inspectable dispatch counter. Load the request schema and a supported draft 2020-12 validator. Reject unknown fields and duplicate JSON keys before evaluation.
2. Select the connector family and exact intended operation. Identify whether an effect is known to be a read or write from the trusted mapping. If the mapping is missing, stop with `EFFECT_UNKNOWN`.
3. Gather a complete inventory observation for the selected session. Record collection time and descriptor digest. A tool absent from a complete inventory is unavailable; an incomplete inventory yields unknown. Reconnect and re-enumerate after a session change.
4. Resolve the credential reference privately. Record only the authentication status, principal alias and observation time. Unknown authentication requires fixing the observer, while unauthenticated requires the normal login flow. Neither permits probing arbitrary assets.
5. Ask the grant resolver about the exact family, asset and operation. An unavailable resolver yields `GRANT_UNKNOWN`. An authoritative rejection yields `ASSET_DENIED`. Never broaden permission just to make the diagnostic pass.

## Read and controlled write paths

6. Evaluate the valid read fixture with a synthetic clock preceding all expiry times. Expect a ready decision in a future implementation and exactly one dispatch after audit acknowledgment. Repeat with the invalid fixtures; expect zero dispatches and the documented primary codes. These are expected outcomes until measured.
7. For a real read, use a minimum-size probe only after the intended asset is authorized. Limit returned fields and redact the receipt. Compare the probe's principal/session to the evaluated evidence. If either changed, discard the decision and start discovery again.
8. For a write, render a review record containing family, operation, target asset alias, purpose, canonical payload digest and expiry. Obtain the specific approval through an approved human or organizational authorization workflow. A generic “continue” or approval for a different asset does not satisfy this record.
9. Revalidate immediately before dispatch. Verify the approver's authority, match the digest, check expiry, consume approval atomically and persist intent. Do not allow an operator to edit the payload after approval; any edit creates a new request and requires a new bound approval.
10. Dispatch once with a deadline. Record success only when the adapter has evidence of the intended effect. For a timeout after sending, mark `INDETERMINATE` with `DISPATCH_UNKNOWN`; do not retry the write automatically. Use a separately authorized read to reconcile.

## Recovery and escalation

If inventory becomes stale, refresh inventory and restart all dependent checks. If credentials rotate, authenticate and resolve grants again. If grants change, invalidate queued decisions and unconsumed approvals. If audit storage fails before a write, keep the request blocked; if it fails after dispatch, retain the local sanitized intent and escalate reconciliation. Never log credentials to diagnose the audit failure.

When reconciliation cannot establish whether an effect occurred, preserve the intent ID, request digest and sanitized transport timing, then hand control to the designated operator. A fresh approval is required for any replacement write. Do not erase an uncertain receipt or relabel a timeout as a failed operation.

Close the run with observed versus expected results, dispatch counts and evidence references. Public reports may contain synthetic traces only. No scheduled model calls or autonomous background operation are part of this runbook; any ordinary scheduler is an implementation choice subject to the same gates.
