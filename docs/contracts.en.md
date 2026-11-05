# Data contracts

[README](../README.md)

[Synthetic example](../examples/contract.json)

| Field | Illustrative JSON value type |
| --- | --- |
| `connector_family` | `str` |
| `operation` | `str` |
| `mode` | `str` |
| `asset_ref` | `str` |
| `authentication` | `str` |
| `capability_checked` | `bool` |

The example is intentionally synthetic and is a documentation fixture, not a production schema. Empty, absent and unknown values must remain distinguishable. Validate structure at ingestion, normalize only after preserving the original meaning, and retain version and collection context for derived records. Error messages must not echo raw credentials or personal data.
