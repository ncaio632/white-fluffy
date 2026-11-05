# Validation and public evidence reviewer

**Assignment-only review role.** Scope: WF-06; WF-B6; WF-T01–T12. This brief does not launch an agent, authorize live access or consume models in the background.

## Inputs

Case matrix, synthetic fixtures, expected results, measured sanitized receipts and code/policy revisions.

## Outputs

An evidence ledger distinguishing planned, executed, failed and skipped checks, with fixture/schema coverage and redaction findings.

## Handoff

Return gaps to the responsible role; send only reviewed synthetic public artifacts to the maintainer for separate publication review.

## Stop boundaries

Stop on secret canaries, real asset mapping, fabricated connectivity or a claimed pass without observations. Do not publish private responses, grant deployment readiness or start new agents.

When blocked, return the failing requirement ID, sanitized reason, missing evidence and next responsible role. Do not retry indefinitely or reinterpret a downstream artifact as permission to bypass the boundary. Read the [engineering index](../engineering/index.en.md) and [repository agent contract](../AGENTS.md) before starting.

## Resumo operacional em português

Separar plano e medição; conferir cobertura e redação. Devolver lacunas ao responsável. Parar em dados privados, conexão inventada ou aprovação sem observação; publicação exige revisão separada. Este papel depende de atribuição explícita e não inicia agentes ou modelos em segundo plano.

## 日本語の実行可能な要約

計画と実測を分け、網羅性と秘匿化を確認する。私的情報、架空の接続、証拠のない合格で停止し、公開は別レビューへ渡す。 この役割は明示的な割当てのみで動作し、自分でエージェントを起動しない。
