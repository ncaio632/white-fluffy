# Traceability, fixture oracle and evidence policy

**All execution scenarios below are planned.** JSON syntax and local artifact-link checks may be performed during document production; those checks do not establish connector behavior, grant enforcement or live security. A future implementer records observations against the exact revision under test.

| Case | Requirement / backlog | Setup and expected result |
|---|---|---|
| WF-T01 | WF-01 / B2 | Complete inventory lacks the tool → `TOOL_UNAVAILABLE`, zero dispatches. |
| WF-T02 | WF-01, WF-07 / B2 | Stale inventory or changed session → `EVIDENCE_STALE`, zero dispatches. |
| WF-T03 | WF-02 / B2 | Unknown auth → `AUTH_UNKNOWN`; unauthenticated → `AUTH_REQUIRED`. |
| WF-T04 | WF-03 / B3 | Auth succeeds, asset denied → `ASSET_DENIED`, zero dispatches. |
| WF-T05 | WF-03 / B3 | Principal, family or operation differs → `GRANT_UNKNOWN`, zero dispatches. |
| WF-T06 | WF-04 / B4 | Missing write approval → `APPROVAL_REQUIRED`; mismatched asset/digest → `APPROVAL_MISMATCH`. |
| WF-T07 | WF-04, WF-07 / B4 | Expired or consumed approval → `APPROVAL_EXPIRED` or `APPROVAL_REUSED`. |
| WF-T08 | WF-05 / B4 | Tool payload contains instructions to broaden scope → no new authority or dispatch. |
| WF-T09 | WF-06, WF-08 / B5 | Timeout after simulated write effect → `DISPATCH_UNKNOWN`; restart performs no replay. |
| WF-T10 | WF-06 / B6 | Credential canary in transport exception → absent from decision, receipt and public export. |
| WF-T11 | WF-04 / B1 | Reordered object keys hash identically; changed payload hashes differently. |
| WF-T12 | WF-08 / B5 | Oversized result, expired deadline or exhausted read retry budget → bounded terminal result. |

## Fixture expectations

`examples/engineering/valid-read.json` and `valid-write.json` satisfy the envelope's structural contract. The latter contains a synthetic digest and approval reference, so it is not executable proof of a valid approval or payload hash. `invalid-missing-asset.json` fails schema validation (`SCHEMA_INVALID`). `invalid-approval-binding.json` passes shape validation but must fail semantic evaluation (`APPROVAL_MISMATCH`). `invalid-asset-denied.json` also passes shape validation and must stop at `ASSET_DENIED`. `valid-receipt.json` demonstrates an indeterminate write, not successful connectivity. Use the synthetic test clock `2030-01-01T00:01:00Z`; fixture timestamps are examples, never current evidence.

## Evidence record and acceptance

For every executed case capture case ID, code revision, policy revision, environment alias, clock, input digest, expected state, actual state, dispatch count, sanitized receipt and reviewer. Include the validator name/version and whether timestamp format checking was enabled. Failed and skipped cases remain visible; a skipped live test is not a pass. Record adverse results and the exact failing predicate without including raw credentials or private asset identifiers.

A draft 2020-12 validator checks schema syntax and instance shape. An evaluator test suite checks cross-field equality, expiry, digest recomputation, approval authority and atomic consumption. An integration suite checks observed inventory, actual grant semantics and transport uncertainty in a separately approved environment. These are three different evidence layers. A valid JSON fixture cannot substitute for any missing layer.

Keep a bounded archive of redacted results according to deployment policy; do not publish account responses to make the tests look realistic. A release may claim only the cases actually measured against its implementation revision. The design intentionally makes no claim of exact compatibility with a private operational system.
