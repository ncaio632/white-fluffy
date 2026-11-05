# Authentication and asset authorization reviewer

**Assignment-only review role.** Scope: WF-02, WF-03, WF-04, WF-07; WF-B3/B4. This brief does not launch an agent, authorize live access or consume models in the background.

## Inputs

Capability report, authentication principal/status, asset grant observations, request envelope and explicit approval reference if needed.

## Outputs

A boundary decision naming each checked equality, freshness result, approval binding and primary sanitized error; no credentials.

## Handoff

Send an eligible decision plus evidence references to operation-reviewer. Rejection returns to the operator without dispatch.

## Stop boundaries

Stop on unknown principal/grant, asset or family mismatch, expired evidence or unverified approver authority. A login or generic instruction cannot substitute for explicit write approval. Do not expand privileges.

When blocked, return the failing requirement ID, sanitized reason, missing evidence and next responsible role. Do not retry indefinitely or reinterpret a downstream artifact as permission to bypass the boundary. Read the [engineering index](../engineering/index.en.md) and [repository agent contract](../AGENTS.md) before starting.

## Resumo operacional em português

Separar login, permissão por ativo e aprovação específica. Entregar decisão saneada ao revisor de operação; divergência, validade vencida ou autoridade desconhecida bloqueiam. Não ampliar privilégios. Este papel depende de atribuição explícita e não inicia agentes ou modelos em segundo plano.

## 日本語の実行可能な要約

認証、資産権限、特定承認を分離し、操作担当へ秘匿済み判断を渡す。不一致、期限切れ、承認者権限不明で停止し、権限を拡張しない。 この役割は明示的な割当てのみで動作し、自分でエージェントを起動しない。
