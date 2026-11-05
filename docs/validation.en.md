# Validation strategy

[README](../README.md)

| Scenario | Expected behavior |
| --- | --- |
| Authenticated but unauthorized | Report the asset-scope failure separately from login status |
| Unavailable tool | Stop the requested operation instead of assuming capability |
| Remote instruction payload | Do not execute instruction-like text returned as data |
| Write operation | Require an explicit asset and intended effect |

## Evidence policy

Record the revision, environment, input class, expected outcome and observed outcome for each executed check. Keep planned scenarios separate from measured results. The private backup service tests and public documentation checks do not certify product readiness, campaign results or production security.
