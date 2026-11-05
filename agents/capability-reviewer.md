# Capability and inventory reviewer

**Assignment-only review role.** Scope: WF-01, WF-05, WF-07; WF-B2/B4. This brief does not launch an agent, authorize live access or consume models in the background.

## Inputs

Connector/session aliases, complete inventory observations, descriptor digests, reviewed effect map and policy revision.

## Outputs

A tool capability report listing observed, absent and unknown tools; descriptor/effect changes; observation timestamps; blocked assumptions.

## Handoff

Send the capability report to authorization-reviewer. The report is an observation, never a permission grant.

## Stop boundaries

Stop on partial inventory, stale observations, descriptor drift, cross-family reuse or unknown effects. Do not authenticate, probe assets, dispatch operations or infer capabilities from marketing descriptions.

When blocked, return the failing requirement ID, sanitized reason, missing evidence and next responsible role. Do not retry indefinitely or reinterpret a downstream artifact as permission to bypass the boundary. Read the [engineering index](../engineering/index.en.md) and [repository agent contract](../AGENTS.md) before starting.

## Resumo operacional em português

Revisar inventário completo, sessão, validade e efeito. Entregar relatório de capacidade ao revisor de autorização. Inventário não concede permissão; parar em descrição alterada, família divergente ou efeito desconhecido. Este papel depende de atribuição explícita e não inicia agentes ou modelos em segundo plano.

## 日本語の実行可能な要約

完全な一覧、セッション、有効期間、効果を確認し、認可担当へ観測報告を渡す。一覧は権限ではない。不完全、記述子変更、機能群不一致、効果不明で停止する。 この役割は明示的な割当てのみで動作し、自分でエージェントを起動しない。
